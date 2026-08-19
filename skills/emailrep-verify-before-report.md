---
name: Verify an address before reporting it to EmailRep
description: >-
  The safe write path — query an address first, decide whether a report adds signal, then submit.
  Mirrors arazzo/emailrep-verify-before-report-workflow.yml and exists because POST /report has
  no idempotency contract and no undo.
api: openapi/emailrep-reputation-api-openapi.yml
operations:
  - queryEmailReputation
  - reportEmail
generated: '2026-08-13'
method: generated
source: >-
  Grounded in openapi/emailrep-reputation-api-openapi.yml and
  openapi/emailrep-reports-api-openapi.yml (both operationIds verified), mirroring
  arazzo/emailrep-verify-before-report-workflow.yml.
---

# Verify an address before reporting it

EmailRep has no way to withdraw a report and no idempotency key. A duplicate or mistaken
submission changes what other organizations see. This is the sequence an agent should follow
whenever it is about to write.

## Step 1 — query first

Call `queryEmailReputation` on the address.

```
GET https://emailrep.io/{email}
Key: <your api key>
User-Agent: <your app name>
```

## Step 2 — decide whether the report adds signal

Stop and do **not** report when:

- `blacklisted: true` **and** `malicious_activity_recent: true` — the graph already knows, within
  the last 90 days. Your report adds nothing.
- Your evidence is a suspicion rather than an observation. `reputation: none` on its own is not
  evidence of malice; plenty of legitimate new addresses score `none`.
- The address belongs to your own users or customers. Reporting a compromised customer mailbox as
  `bec` rather than `account_takeover` leaves them permanently blacklisted to everyone else.

Proceed when:

- You observed the behavior yourself (a message, an attachment, a landing page), **and**
- The current reputation does not already reflect it — for example `suspicious: false` on an
  address that just sent you a credential-phishing message.

## Step 3 — report with the narrowest accurate tag

Call `reportEmail`. Choose from the twelve-tag vocabulary in
`data-model/emailrep-data-model.yml`, set `timestamp` to when you actually observed the activity,
and time-box `expires` when the mailbox is a compromised legitimate account rather than an
attacker-owned one.

## Step 4 — confirm rather than retry

If the POST fails or times out, **re-query** rather than re-post. Check whether `suspicious` and
`blacklisted` now reflect your submission. Only resubmit when the query shows the report did not
land.

## Budget note

This flow costs **two** calls per address. On the free tier (10/day, 250/month) that is five
verified reports a day. Batch your triage rather than running this per message.

## Related

- `arazzo/emailrep-verify-before-report-workflow.yml` — the runnable workflow
- `skills/emailrep-screen-inbound-sender.md`
- `skills/emailrep-report-malicious-sender.md`
