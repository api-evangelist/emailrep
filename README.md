# EmailRep (emailrep)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

EmailRep is an email address reputation and threat-intelligence API operated by Sublime Security, Inc. It crawls and enriches data across social media profiles, professional networking sites, dark-web credential leaks, data breaches, phishing kits, phishing emails, spam lists, open mail relays, spam traps, domain age and reputation, and email-deliverability signals to predict the risk associated with any email address. The free, JSON-over-HTTP REST API returns a `reputation`, a `suspicious` flag, a `references` count, and a detailed signal block (blacklisted, malicious_activity, credentials_leaked, data_breach, domain_reputation, deliverable, spoofable, profiles, and more). A POST `/report` endpoint lets analysts contribute observations of malicious email behavior back into the reputation graph.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/emailrep/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/emailrep/refs/heads/main/apis.yml)

## Scope

- **Type:** Index

## Tags

- Security
- Email
- Email Reputation
- Threat Intelligence
- Phishing
- Fraud Prevention
- Anti-Abuse
- Deliverability
- Risk Scoring
- Public APIs

## Timestamps

- **Created:** 2026-05-28
- **Modified:** 2026-05-30

## APIs

### EmailRep API

Email reputation and threat-intelligence REST API. `GET /{email}` returns a reputation verdict (high/medium/low/none), a `suspicious` flag, a `references` count, and a detailed signal block covering blacklisting, malicious activity, credential leaks, data breaches, domain age and reputation, deliverability, MX validity, SPF/DMARC posture, spoofability, free-provider/disposable status, and known online profiles. `POST /report` lets authenticated callers report an email address as malicious (BEC, phishing, fraud, account takeover, maldoc, etc.) so the signal feeds the reputation graph. Authentication is via a `Key` header issued from emailrep.io/key. Free tier: 250 queries/month, 10/day; Commercial tier: 1,000 queries/month at $20/month with no daily limit; Enterprise: high-volume custom plans with SLA.

- **Human URL:** [https://emailrep.io](https://emailrep.io)
- **Base URL:** `https://emailrep.io`

#### Tags

- Email Reputation
- Threat Intelligence
- Phishing
- Fraud
- Deliverability

#### Properties

- [Documentation](https://docs.sublimesecurity.com/reference/emailrep-introduction)
- [API Reference](https://docs.sublimesecurity.com/reference/emailrep-introduction)
- [Getting Started](https://docs.sublimesecurity.com/reference/emailrep-quickstart)
- [OpenAPI](openapi/emailrep-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/emailrep-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/emailrep-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [SDK](https://github.com/sublime-security/emailrep.io-python)
- [SDK](https://pypi.org/project/emailrep/)
- [SDK](https://github.com/arnydo/PSEmailRep)
- [SDK](https://git.rud.is/hrbrmstr/emailrep)
- [SDK](https://github.com/WestDiscGolf/EmailRep.NET)
- [SDK](https://github.com/kaiiyer/emailrep)
- [SDK](https://github.com/vertoforce/go-emailrep)
- [C L I](https://github.com/sublime-security/emailrep.io-python)
- [Source Code](https://github.com/sublime-security/emailrep.io)

## Common Properties

- [Arazzo Workflows](arazzo/) — [Arazzo Specification](https://spec.openapis.org/arazzo/latest.html)
- [Website](https://emailrep.io)
- [Documentation](https://docs.sublimesecurity.com/reference/emailrep-introduction)
- [API Reference](https://docs.sublimesecurity.com/reference/emailrep-introduction)
- [Getting Started](https://docs.sublimesecurity.com/reference/emailrep-quickstart)
- [Sign Up](https://emailrep.io/key)
- [Pricing](https://emailrep.io/key)
- [Terms of Service](https://emailrep.io/terms)
- [Privacy Policy](https://emailrep.io/privacy)
- [Blog](https://emailrep.io/blog)
- [Support](https://sublimesecurity.com/contact)
- [GitHub Organization](https://github.com/sublime-security)
- [Source Code](https://github.com/sublime-security/emailrep.io)
- [Operator](https://sublimesecurity.com)
- [LinkedIn](https://www.linkedin.com/company/sublime-security)
- [Public APIs Listing](https://github.com/public-apis/public-apis)
- [Tools](https://github.com/sublime-security/sublime-platform)
- [Tools](https://github.com/sublime-security/sublime-rules)
- [Tools](https://github.com/sublime-security/sublime-cli)
- [Tools](https://github.com/sublime-security/connectors)
- [Tools](https://github.com/sublime-security/mql-vscode)
- [Tools](https://github.com/sublime-security/ics-phishing-toolkit)
- [Tools](https://github.com/sublime-security/strelka)
- [Tutorials](https://github.com/sublime-security/detection-workshop)
- [Plans](plans/emailrep-plans-pricing.yml)
- [Rate Limits](rate-limits/emailrep-rate-limits.yml)
- [Fin Ops](finops/emailrep-finops.yml)
- [Vocabulary](vocabulary/emailrep-vocabulary.yml)
- [Spectral Ruleset](rules/emailrep-spectral-rules.yml)
- [JSON Schema](json-schema/api-email-reputation-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/api-email-reputation-details-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/api-report-request-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/api-report-response-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](json-structure/api-email-reputation-structure.json)
- [JSON Structure](json-structure/api-email-reputation-details-structure.json)
- [JSON Structure](json-structure/api-report-request-structure.json)
- [JSON Structure](json-structure/api-report-response-structure.json)
- [JSON-LD](json-ld/emailrep-api-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Examples](examples/api-email-reputation-example.json)
- [Examples](examples/api-email-reputation-details-example.json)
- [Examples](examples/api-report-request-example.json)
- [Examples](examples/api-report-response-example.json)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
