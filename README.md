# EmailRep (emailrep)

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
