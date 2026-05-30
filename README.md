# EmailRep (emailrep)

EmailRep is an email address reputation and threat-intelligence API operated by Sublime Security, Inc. It crawls and enriches data across social media profiles, professional networking sites, dark-web credential leaks, data breaches, phishing kits, phishing emails, spam lists, open mail relays, spam traps, domain age and reputation, and email-deliverability signals to predict the risk associated with any email address. The free, JSON-over-HTTP REST API returns a `reputation`, a `suspicious` flag, a `references` count, and a detailed signal block (blacklisted, malicious_activity, credentials_leaked, data_breach, domain_reputation, deliverable, spoofable, profiles, and more). A POST `/report` endpoint lets analysts contribute observations of malicious email behavior back into the reputation graph.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/emailrep/refs/heads/main/apis.yml)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags:

 - Security, Email, Email Reputation, Threat Intelligence, Phishing, Fraud Prevention, Anti-Abuse, Deliverability, Risk Scoring, Public APIs

## Timestamps

- **Created:** 2026-05-28
- **Modified:** 2026-05-30

## APIs

### EmailRep API

Email reputation and threat-intelligence REST API. `GET /{email}` returns a reputation verdict (high/medium/low/none), a `suspicious` flag, a `references` count, and a detailed signal block covering blacklisting, malicious activity, credential leaks, data breaches, domain age and reputation, deliverability, MX validity, SPF/DMARC posture, spoofability, free-provider/disposable status, and known online profiles. `POST /report` lets authenticated callers report an email address as malicious (BEC, phishing, fraud, account takeover, maldoc, etc.) so the signal feeds the reputation graph. Authentication is via a `Key` header issued from emailrep.io/key. Free tier: 250 queries/month, 10/day; Commercial tier: 1,000 queries/month at $20/month with no daily limit; Enterprise: high-volume custom plans with SLA.

**Human URL:** [https://emailrep.io](https://emailrep.io)

#### Tags:

 - Email Reputation, Threat Intelligence, Phishing, Fraud, Deliverability

#### Properties

- [Documentation](https://docs.sublimesecurity.com/reference/emailrep-introduction)
- [APIReference](https://docs.sublimesecurity.com/reference/emailrep-introduction)
- [GettingStarted](https://docs.sublimesecurity.com/reference/emailrep-quickstart)
- [OpenAPI](openapi/emailrep-api-openapi.yml)
- [Python SDK](https://github.com/sublime-security/emailrep.io-python)
- [Python Package](https://pypi.org/project/emailrep/)
- [PowerShell SDK (community)](https://github.com/arnydo/PSEmailRep)
- [R SDK (community)](https://git.rud.is/hrbrmstr/emailrep)
- [.NET SDK (community)](https://github.com/WestDiscGolf/EmailRep.NET)
- [Go SDK (community)](https://github.com/kaiiyer/emailrep)
- [Go SDK (community, vertoforce)](https://github.com/vertoforce/go-emailrep)
- [CLI](https://github.com/sublime-security/emailrep.io-python)
- [SourceCode](https://github.com/sublime-security/emailrep.io)
- [Naftiko Capability — Reputation](capabilities/emailrep-api-reputation.yaml)
- [Naftiko Capability — Reports](capabilities/emailrep-api-reports.yaml)

## Common Properties

- [Website](https://emailrep.io)
- [Documentation](https://docs.sublimesecurity.com/reference/emailrep-introduction)
- [APIReference](https://docs.sublimesecurity.com/reference/emailrep-introduction)
- [GettingStarted](https://docs.sublimesecurity.com/reference/emailrep-quickstart)
- [SignUp](https://emailrep.io/key)
- [Pricing](https://emailrep.io/key)
- [TermsOfService](https://emailrep.io/terms)
- [PrivacyPolicy](https://emailrep.io/privacy)
- [Blog](https://emailrep.io/blog)
- [Support](https://sublimesecurity.com/contact)
- [GitHubOrganization](https://github.com/sublime-security)
- [SourceCode](https://github.com/sublime-security/emailrep.io)
- [Operator](https://sublimesecurity.com)
- [LinkedIn](https://www.linkedin.com/company/sublime-security)
- [PublicAPIsListing](https://github.com/public-apis/public-apis)
- [Tools — Sublime Platform](https://github.com/sublime-security/sublime-platform)
- [Tools — Sublime Rules](https://github.com/sublime-security/sublime-rules)
- [Tools — Sublime CLI](https://github.com/sublime-security/sublime-cli)
- [Tools — OpenCTI Connectors](https://github.com/sublime-security/connectors)
- [Tools — MQL VS Code Extension](https://github.com/sublime-security/mql-vscode)
- [Tools — ICS Phishing Toolkit](https://github.com/sublime-security/ics-phishing-toolkit)
- [Tools — Strelka File Scanning](https://github.com/sublime-security/strelka)
- [Tutorials — Detection Engineering Workshop](https://github.com/sublime-security/detection-workshop)
- [Plans](plans/emailrep-plans-pricing.yml)
- [RateLimits](rate-limits/emailrep-rate-limits.yml)
- [FinOps](finops/emailrep-finops.yml)
- [Vocabulary](vocabulary/emailrep-vocabulary.yml)
- [SpectralRuleset](rules/emailrep-spectral-rules.yml)

## Features

| Name | Description |
|------|-------------|
| Reputation Verdict | Each email lookup returns a `reputation` of `high`, `medium`, `low`, or `none` summarizing the overall trust signal for the address. |
| Suspicious Flag | A boolean `suspicious` field indicates whether the email should be treated as risky based on combined positive and negative signals. |
| References Count | `references` is the total number of positive and negative reputation sources observed for the address or its associated domain. |
| Credential-Leak and Breach Signals | Detects whether the email has appeared in known data breaches, dark-web credential leaks, or pastes — historically and within the last 90 days. |
| Domain Reputation and Age | Reports `domain_exists`, `domain_reputation`, `new_domain`, and `days_since_domain_creation` so callers can weight reputation against domain freshness. |
| Deliverability and Mail-Server Posture | Reports `deliverable`, `accept_all`, `valid_mx`, `spoofable`, `spf_strict`, and `dmarc_enforced` for both fraud prevention and legitimate sender hygiene. |
| Provider Classification | Classifies the address as `free_provider`, `disposable`, `suspicious_tld`, or `spam` to expose throwaway or low-quality accounts. |
| Online Profile Discovery | Returns a `profiles` array enumerating social and professional networking sites where the email has been observed. |
| Crowd-Sourced Reporting | `POST /report` accepts community submissions of malicious email behavior (BEC, phishing, fraud, account takeover, maldoc) with tags, description, timestamp, and an expires window so signal feeds the reputation graph. |

## Use Cases

| Name | Description |
|------|-------------|
| Phishing and BEC Detection | Score inbound emails against EmailRep to identify suspicious senders, brand-spoofing attempts, and targeted Business Email Compromise. |
| Account-Signup Abuse Prevention | Block or step-up disposable, throwaway, or known-malicious email addresses during user registration to reduce fraud and abuse. |
| Marketing List Hygiene | Validate deliverability, catch-all status, and disposable-provider use on inbound or outbound marketing lists to protect sender reputation. |
| Threat-Intelligence Enrichment | Enrich SIEM, SOAR, and case-management workflows with email reputation signals alongside netflow, EDR, and email-gateway telemetry. |
| Sender-Reputation Self-Check | Marketing, sales, and outbound teams can verify their own addresses to ensure they aren't trapped on spam lists or blocklists. |
| Red-Team and Recon | Authorized offensive-security teams can profile target email addresses for credential brute forcing and targeted phishing-engagement design. |

## Integrations

| Name | Description |
|------|-------------|
| Sublime Platform | Native consumer of EmailRep signals inside the Sublime Security email detection-and-response platform for inbound email threat hunting and response. |
| Sublime Rules | Open-source MQL detection rules in github.com/sublime-security/sublime-rules can call EmailRep enrichment as part of email-attack detection. |
| OpenCTI Connectors | EmailRep enrichment is callable from threat-intel platforms via the Sublime-maintained OpenCTI connectors repo. |
| SOAR Playbooks | EmailRep is widely used as an enrichment node in SOAR products (Tines, Splunk SOAR, Cortex XSOAR, Torq) for phishing triage. |
| Python, PowerShell, R, .NET, Go SDKs | First-party Python SDK plus community-maintained PowerShell, R, .NET, and Go libraries make EmailRep callable from analyst tooling. |

## Solutions

| Name | Description |
|------|-------------|
| Email Threat Intelligence | Reputation, breach exposure, and online-profile signals on any email address, queryable in a single HTTP call. |
| Account-Takeover and Fraud Prevention | Disposable, free-provider, new-domain, and recent-credential-leak signals support sign-up abuse and ATO defenses. |
| Email Hygiene and Deliverability Insight | Deliverable, accept-all, MX, SPF, and DMARC signals support marketing, sales, and IT-ops list hygiene work. |

## Artifacts

Machine-readable API specifications organized by format.

### OpenAPI

- [EmailRep API](openapi/emailrep-api-openapi.yml)

### JSON Schema

- [EmailReputation](json-schema/api-email-reputation-schema.json)
- [EmailReputationDetails](json-schema/api-email-reputation-details-schema.json)
- [ReportRequest](json-schema/api-report-request-schema.json)
- [ReportResponse](json-schema/api-report-response-schema.json)

### JSON Structure

- [EmailReputation](json-structure/api-email-reputation-structure.json)
- [EmailReputationDetails](json-structure/api-email-reputation-details-structure.json)
- [ReportRequest](json-structure/api-report-request-structure.json)
- [ReportResponse](json-structure/api-report-response-structure.json)

### JSON-LD

- [EmailRep API Context](json-ld/emailrep-api-context.jsonld)

### Examples

- [EmailReputation](examples/api-email-reputation-example.json)
- [EmailReputationDetails](examples/api-email-reputation-details-example.json)
- [ReportRequest](examples/api-report-request-example.json)
- [ReportResponse](examples/api-report-response-example.json)

## Capabilities

Naftiko capabilities organized as self-contained per-tag definitions, each exposing the same operations as both REST and MCP adapters.

### EmailRep API

| Capability | Operations | Tools | Surface |
|----------|-----------|-------|---------|
| [EmailRep API — Reputation](capabilities/emailrep-api-reputation.yaml) | 1 | 1 | REST + MCP |
| [EmailRep API — Reports](capabilities/emailrep-api-reports.yaml) | 1 | 1 | REST + MCP |

## Vocabulary

- [EmailRep Vocabulary](vocabulary/emailrep-vocabulary.yml) — Unified taxonomy mapping 2 resources, 2 actions, 2 workflows, and 4 personas across operational (OpenAPI) and capability (Naftiko) dimensions.

## Rules

- [EmailRep Spectral Ruleset](rules/emailrep-spectral-rules.yml) — 43 rules across 13 categories enforcing EmailRep / Sublime Security API conventions.

## Plans, Rate Limits, FinOps

- [Plans & Pricing](plans/emailrep-plans-pricing.yml) — Free (250 queries/month, 10/day), Commercial ($20/month, 1,000/month, no daily cap), Enterprise (custom, SLA).
- [Rate Limits](rate-limits/emailrep-rate-limits.yml) — Per-API-key rate limits; 429 on quota exceeded.
- [FinOps](finops/emailrep-finops.yml) — FOCUS-aligned billing model: subscription + free tier, USD monthly billing, published by Sublime Security, Inc.

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
