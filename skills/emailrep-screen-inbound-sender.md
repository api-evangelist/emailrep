---
name: Screen an inbound sender with EmailRep
description: >-
  Look up the reputation of an email address before trusting a message or a signup, and turn the
  21-field signal block into a defensible verdict. Covers the two headers EmailRep requires, the
  429 that is not a rate limit, and the fields that actually carry the risk decision.
api: openapi/emailrep-reputation-api-openapi.yml
operations:
  - queryEmailReputation
generated: '2026-08-13'
method: generated
source: >-
  Grounded in openapi/emailrep-reputation-api-openapi.yml (operationId verified),
  https://docs.sublime.security/reference/emailrep-introduction, and a live probe of
  https://emailrep.io/bill@microsoft.com on 2026-08-13.
---

# Screen an inbound sender with EmailRep

## Before the first call

Two things will make your first request fail, and neither is in the OpenAPI:

1. **Send a `User-Agent`.** It must name your application. Missing it returns **403**, before the
   key is even checked. A generic or misleading agent may be blocked outright.
2. **Send a `Key`.** The docs still say the key is optional. It is not. An anonymous request
   returns **429** with `{"status": "fail", "reason": "the unauthenticated API is currently
   disabled. please use an API key"}`. Get one at <https://emailrep.io/free>.

## Step 1 — query the address

Call `queryEmailReputation` — `GET https://emailrep.io/{email}`.

```
GET https://emailrep.io/attacker@example.com?summary=true
Key: <your api key>
User-Agent: <your app name>
```

`summary=true` adds a human-readable `summary` string. Ask for it when a human will read the
result; skip it when only your code will.

## Step 2 — read the verdict, not just the score

`reputation` is `high` / `medium` / `low` / `none` and `suspicious` is a boolean. Neither is
sufficient on its own:

- **`reputation: none` is not the same as bad.** It means the address has no trustworthy history
  anywhere — common for a brand-new legitimate address and for a throwaway. Combine it with
  `new_domain`, `disposable` and `free_provider` before acting.
- **`reputation: high` is not the same as safe.** A legitimate high-reputation account can be
  taken over or spoofed. Check `malicious_activity_recent`, `credentials_leaked_recent` and
  `spoofable` before you trust a message that asks for money or credentials.
- **`references`** counts positive *and* negative sources, and some of them describe the domain
  rather than the address. It is a confidence indicator, not a risk score.

## Step 3 — pick the fields your decision actually needs

Use `details` selectively rather than dumping all 21 fields into a model prompt:

| Decision | Fields that matter |
|---|---|
| Is this message a phishing attempt? | `blacklisted`, `malicious_activity`, `malicious_activity_recent`, `spoofable`, `dmarc_enforced`, `spf_strict` |
| Is this signup abuse? | `disposable`, `free_provider`, `new_domain`, `days_since_domain_creation`, `suspicious_tld` |
| Is this address worth emailing? | `deliverable`, `valid_mx`, `accept_all`, `domain_exists` |
| Has this person been breached? | `credentials_leaked`, `credentials_leaked_recent`, `data_breach`, `first_seen`, `last_seen` |

`accept_all: true` means the mail server accepts everything, so `deliverable` proves little for
that domain. `domain_reputation: n/a` is expected whenever the domain is a free provider or
disposable — it is not a failure.

## Step 4 — handle the failures correctly

| Status | What it means | What to do |
|---|---|---|
| 400 | Not a valid email address | Validate locally first. Do not retry. |
| 401 | Bad or missing `Key` | Fix the credential. Do not retry. |
| 403 | Missing/unacceptable `User-Agent` | Add a descriptive agent. Do not retry as-is. |
| 429 + `reason` mentioning rate limit | Quota exhausted | Back off exponentially. The window is **rolling 24 hours**, so waiting for midnight does not help. |
| 429 + `reason: the unauthenticated API is currently disabled` | You sent no key | **Not retryable.** Add a key. |

**Always read `reason`.** 429 carries two unrelated meanings and the status code alone cannot
tell them apart. Watch `X-Rate-Limit-Daily-Remaining` and `X-Rate-Limit-Monthly-Remaining` to
avoid hitting the wall at all.

## Budget awareness

The free tier is 250 queries/month with a 10/day ceiling; the $20/month Commercial tier is
1,000/month with no daily cap. Cache verdicts per address for the length of your triage window
rather than re-querying the same sender on every message.

## Related

- `conventions/emailrep-conventions.yml` — the full runtime contract
- `errors/emailrep-problem-types.yml` — every status this API returns
- `rate-limits/emailrep-rate-limits.yml` — quotas and headers
