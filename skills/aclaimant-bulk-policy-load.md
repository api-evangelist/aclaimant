---
name: aclaimant-bulk-policy-load
description: >-
  Load or refresh policies, policy programs, exposures and exposure summations into Aclaimant at volume using
  the v2 bulk upsert jobs, and poll the job to completion.
api: Aclaimant Platform API
base_url: https://api.aclaimant.com/api
operations:
  - POST /v2/company
  - POST /v2/program
  - POST /v2/policy
  - POST /v2/bulk/programs
  - POST /v2/bulk/policies
  - POST /v2/bulk/exposures
  - POST /v2/bulk/exposure-summations
  - POST /v2/bulk/answers
  - POST /v1/bulk/answers
  - POST /v1/bulk/answer-updates
  - GET /v1/bulk/status/{id}
generated: '2026-09-06'
method: generated
source: openapi/aclaimant-platform-api-openapi.json
---

# Bulk-load policies, programs and exposures

Use this instead of looping single writes. Every bulk operation **enqueues a job and returns a status URL**;
`api.aclaimant.com/status` exposes a live `queued-artifacts-count`, so the queue is real and shared.

## Order of operations

1. `POST /v2/company` (`upsertCompany`) — create or update the company / collective, optionally porting
   configuration from a source company.
2. `POST /v2/bulk/programs` (`bulkUpsertPrograms`) — policy programs first; policies hang off them.
   Single-record equivalent: `POST /v2/program`.
3. `POST /v2/bulk/policies` (`bulkUpsertPolicies`) — policies, their periods, policy-period documents and
   lines of coverage. Single-record equivalent: `POST /v2/policy`.
   Line-of-coverage fields include `premium`, `deductible`, `coverage-limit-per-claim`,
   `total-coverage-limit` and an `extensions` object carrying `sir-amount`, `aggregate-deductible`,
   `retro-date`, `tail-date`, `net-premium`, `gross-premium-total`, `premium-adjustments`,
   `premium-invoice-total`, `taxes-and-fees` and bond fields.
4. `POST /v2/bulk/exposures` (`bulkUpsertExposures`) — exposures against assets and locations, with
   `start-date` / `end-date`.
5. `POST /v2/bulk/exposure-summations` (`bulkUpsertExposureSummations`) — the rolled-up figures.

Answer bundles have their own bulk jobs: `POST /v2/bulk/answers` (upsert),
`POST /v1/bulk/answers` (create-only) and `POST /v1/bulk/answer-updates` (update-only).

## Polling

Each call returns a status URL. Poll `GET /v1/bulk/status/{id}` (`getBulkJobStatus`) until the job settles.
Back off between polls — a `429` is documented with no published limit or `Retry-After`.

## Why v2 and not v1

The v2 operations are **upserts keyed on the `external-ident` you supply**, so re-running a failed load
converges on the same records instead of duplicating them. `POST /v1/bulk/answers` is create-only and is not
replay-safe. This is the entire idempotency story on this API — there is no `Idempotency-Key` header
anywhere. See `conventions/aclaimant-conventions.yml`.

## Rules that will bite you

- **An upsert overwrites; it does not version.** Re-upserting an `external-ident` with different values
  replaces the record's fields and the prior state is not recoverable through the API. There is no rollback,
  no delete and no restore window.
- Every record needs `company-ident`; a key is scoped to the company it was issued for.
- Dates are `YYYY-MM-DD`.
- 24 of 25 operations declare an empty `default` response, so treat any non-2xx body as opaque and log it.
