---
name: aclaimant-partner-loss-run
description: >-
  As a TPA, carrier or broker, acknowledge receipt of a claim Aclaimant submitted to you and post loss-run
  claim financials back into Aclaimant using the Partner / Third-party API.
api: Aclaimant Partner / Third-party API
base_url: https://api.aclaimant.com/partner
operations:
  - POST /claims/{claim-id}/receipt
  - PUT /claims/{claim-id}
generated: '2026-09-06'
method: generated
source: https://developer.aclaimant.com/partner/index.html
---

# Acknowledge a claim and post loss runs

This is the callback surface for partners working claims on behalf of an Aclaimant customer. It has **no
machine-readable contract** — the two endpoints below are documented in prose at
https://developer.aclaimant.com/partner/index.html (revised 2019-02-18).

## Authorization

`Authorization: Bearer <bearer-token>`. Aclaimant provisions the token; there is no self-service issuance,
no documented lifetime and no refresh flow.

## 1. Acknowledge receipt

`POST /claims/{claim-id}/receipt`

- `claim-id` (path) — Aclaimant's identifier, taken from the submission Aclaimant sent you.
- `claim-number` (required, string) — your own claim number. Must be unique for the policy within Aclaimant.
- `receipt-status` (required, string) — `pending`, `accepted` or `denied`.
- `receipt-status-date` (required, date-time) — when your system made that status change.

Success is `204` with no body.

## 2. Post claim updates with loss runs

`PUT /claims/{claim-id}`

- `status` (string) — `open` or `closed`.
- `closed-date` (date-time) — required or not depending on the Aclaimant policy configuration; policies decide.
- `new-report` (optional, `claim-report`) — the latest financials.

Success is `204`.

### The `claim-report` type

- `date-of-report` (required, date-time)
- `adjuster` (optional) — if omitted, the previous report's adjuster is carried forward when available
- `adjuster-notes` (optional)
- `target-close-date` (optional)
- `entries[]` (required, at least one `entry`), each entry:
  - `category` (required) — `medical`, `indemnity`, `expense`, `legal`, `vocational`, `recovery`, `general`,
    `property-damage`, `cargo-loss` or `cargo-damage`
  - `payment-amount` (required) — positive, two decimal places
  - `reserve-amount` (required) — positive, two decimal places

### Dates

ISO 8601: `YYYY-MM-DDTHH:mm:SSz`, e.g. `2019-02-07T21:12:49.935-00:00`.

## Errors

`400` invalid request · `401` wrong token · `404` unknown resource · `429` too frequent, slow down ·
`500` server error · `503` temporarily offline. No error body shape is documented.

## Rules that will bite you

- **Neither endpoint is idempotent** and there is no idempotency key. A repeated receipt POST is a second
  receipt; a repeated PUT with `new-report` is a second loss-run snapshot on the claim.
- **There is no reversal.** A wrong claim report cannot be voided through the API — only superseded by a
  later report.
- `claim-number` must be unique for the policy inside Aclaimant; a collision is a `400`.
