---
name: Report a malicious sender to EmailRep
description: >-
  Submit an observation of malicious email behavior back into the EmailRep reputation graph,
  using the provider's own twelve-tag vocabulary, and handle the fact that this write has no
  idempotency contract.
api: openapi/emailrep-reports-api-openapi.yml
operations:
  - reportEmail
generated: '2026-08-13'
method: generated
source: >-
  Grounded in openapi/emailrep-reports-api-openapi.yml (operationId verified), the provider's own
  OpenAPI at openapi/_original/emailrep-alpha-api-openapi.json, and
  https://docs.sublime.security/reference/emailrep-introduction.
---

# Report a malicious sender to EmailRep

`POST /report` is a **write into a shared reputation graph**. Other people's fraud and phishing
decisions change because of what you submit. Treat it accordingly: report what you observed, not
what you suspect.

## Before you call

- The `Key` header is **required** for this operation — the provider's own spec applies security
  to `/report` and to nothing else. Anonymous reporting does not exist.
- The `User-Agent` header is required too. Missing it returns 403.

## Step 1 — build the report

Call `reportEmail` — `POST https://emailrep.io/report`.

```
POST https://emailrep.io/report
Key: <your api key>
User-Agent: <your app name>
Content-Type: application/json

{
  "email": "attacker@example.com",
  "tags": ["bec", "brand_impersonation"],
  "description": "Phishing email impersonating the CEO, sent to accounting",
  "timestamp": 1562171178,
  "expires": 168
}
```

`email` and `tags` are required. `timestamp` is UTC epoch seconds and defaults to now — set it
explicitly when you are reporting something you observed earlier, or the graph records the wrong
time.

## Step 2 — use the real tag vocabulary

The provider defines exactly twelve tags. Pick the most specific one that fits:

| Tag | Use it for |
|---|---|
| `account_takeover` | A legitimate address now controlled by an attacker |
| `bec` | Business email compromise, whaling, display-name spoofing |
| `brand_impersonation` | Posing as a known brand (PayPal, Microsoft, Google…) |
| `browser_exploit` | The linked site serves an exploit |
| `credential_phishing` | Trying to steal credentials |
| `generic_phishing` | Phishing where nothing more specific applies |
| `malware` | Malicious documents, droppers, malicious attachments or hosts |
| `scam` | Sextortion, payment, lottery, investment, fake-bank scams |
| `spam` | Unsolicited bulk or spammy behavior |
| `spoofed` | Envelope-from differs from header-from |
| `task_request` | "Buy gift cards", "update payroll", "send W-2s" |
| `threat_actor` | The operator of a phishing kit |

Do **not** invent tags. `maldoc` appears in the provider's own Python SDK README and in older
examples, but it is not in the current vocabulary — use `malware`.

## Step 3 — choose `expires` deliberately

`expires` is in **hours**. While a report is live, that address returns `suspicious: true` and
`blacklisted: true` to every other EmailRep caller.

- Omit it and the report has **no expiration** — permanent, unless you tagged
  `account_takeover`, which defaults to 14 days.
- A compromised-but-legitimate mailbox should be time-boxed. Use `account_takeover` and let the
  14-day default apply, or set a window you can justify.
- A throwaway attacker address can be reported without an expiry.

## Step 4 — handle the response, and do not double-report

Success is `{"status": "success"}`. Failure is `{"status": "fail", "reason": "..."}`.

| Status | Meaning | Action |
|---|---|---|
| 400 | Missing/invalid `email` or `tags` | Fix the body. Do not retry as-is. |
| 401 | Invalid or missing key | Fix the credential. |
| 403 | Missing `User-Agent` | Add one. |
| 429 | Quota exhausted, or you sent no key — read `reason` | Back off, or add a key. |

**There is no idempotency key.** If the call times out you cannot tell whether the report landed.
Do not blindly re-POST. Call `queryEmailReputation` on the same address and check whether
`blacklisted`/`suspicious` already reflect your report before submitting again.

## Related

- `conventions/emailrep-conventions.yml` — idempotency, headers, error envelope
- `data-model/emailrep-data-model.yml` — the full tag vocabulary and its provenance
- `skills/emailrep-screen-inbound-sender.md` — the read side
