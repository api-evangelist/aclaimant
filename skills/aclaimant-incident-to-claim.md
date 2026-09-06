---
name: aclaimant-incident-to-claim
description: >-
  Report an incident into an Aclaimant company workspace, attach the event and file records that document it,
  and open a claim against the governing policy using the Aclaimant Platform API.
api: Aclaimant Platform API
base_url: https://api.aclaimant.com/api
operations:
  - POST /v1/incidents
  - POST /v1/answers
  - POST /v2/answers
  - POST /v1/answers/prototype
  - POST /v1/events
  - POST /v1/files
  - POST /v1/claims
  - PATCH /v1/claims/{claim-id}
generated: '2026-09-06'
method: generated
source: openapi/aclaimant-platform-api-openapi.json
---

# Report an incident and open a claim

Aclaimant's upstream Swagger document declares **no operationId on any operation**, so every step below names
the HTTP method and path exactly as published. The stable operationIds in parentheses come from
`overlays/aclaimant-platform-api-overlay.yaml` in this repository, not from Aclaimant.

## Before you start

- Every request carries the header `x-aclaimant-api-key`. Keys are issued by Aclaimant during implementation;
  there is no developer signup.
- Every request body carries `company-ident` — the identifier of the company or collective you are writing to.
- Records are addressed by an `external-ident` **you** own. Choose it from your own system and keep it stable;
  it is the only thing that makes a retry safe.
- `Accept: application/json` unless you actually want `application/transit+json` or `application/edn`.

## 1. Rehearse the answer bundle (optional but recommended)

`POST /v1/answers/prototype` (`getAnswerBundlePrototype`) returns the specification for a given workflow and
input map without creating anything. This is the only rehearsal operation on the surface — use it to confirm
your input map matches the workflow before you write.

## 2. Create the incident

`POST /v1/incidents` (`createIncident`). Body: `{ "incident": { "incident-ident": "<your key>",
"company-ident": "<company>" }, "integration": "<keyword>" }` — `incident` is required, `integration` optional.

A `201` returns `{ "result": "pending" | "success" | "error", "incident-ident", "incident-id" }`.
**Read `result`, not just the status code** — a 201 whose `result` is `pending` or `error` has not finished.
A `400` returns `{ "error", "incident-ident" }`.

## 3. Record the answer bundle

`POST /v1/answers` (`createAnswerBundle`) creates a response to a workflow. Prefer
`POST /v2/answers` (`upsertAnswerBundle`) — it is create-or-update on your `external-ident`, so a retry
converges instead of duplicating. `PATCH /v1/answers` (`updateAnswerBundle`) updates an existing bundle.

## 4. Attach events and files

- `POST /v1/events` (`createEvent`) creates an event for an existing item: `type`, `category`, `sub-category`,
  `subject` (a `[title, subtitle]` tuple), `location`, `note`. Call
  `GET /v1/event-types/{company-ident}` (`listEventTypes`) first to see which types that company accepts.
- `POST /v1/files` (`createFiles`) registers files for existing items: `filename`, `content-type`,
  `content-length`, `tags`, `confidential?`.
- `PATCH /v1/events/{external-ident}` (`updateEvent`) corrects an event afterwards.

## 5. Open the claim

`POST /v1/claims` (`createClaim`) creates a claim for an existing item. Useful fields: `claim-number`,
`status` (`open`/`closed`), `status-date`, `submitted-date`, `coverage-type` (e.g. `workers-comp`),
`policy-external-ident`, `policy-period-effective-date`, `track-reserves?`, `default-adjuster`,
`default-adjuster-email`, `default-adjuster-phone`, `extended-fields`. Dates are `YYYY-MM-DD`.

Update it later with `PATCH /v1/claims/{claim-id}` (`updateClaimById`) or, if you only know the policy and the
carrier's claim number, `PATCH /v1/claims/{policy-external-ident}/{claim-number}` (`updateClaimByNumber`).

## Rules that will bite you

- **`POST /v1/incidents`, `POST /v1/claims`, `POST /v1/events` and `POST /v1/files` are NOT idempotent.**
  There is no `Idempotency-Key` header. If you do not know whether a call landed, do not blind-retry — look
  the record up or use the v2 upsert equivalent where one exists. See
  `conventions/aclaimant-conventions.yml`.
- **Nothing can be undone.** The API declares no DELETE, cancel, void or restore operation and publishes no
  restore window. A wrongly created incident or claim can only be edited, not withdrawn.
- **Errors are bespoke JSON, not RFC 9457**, and 24 of 25 operations declare an empty `default` response, so
  do not expect a documented error body. See `errors/aclaimant-problem-types.yml`.
- **429 means slow down** with no published limit, window or `Retry-After`. Back off exponentially.
