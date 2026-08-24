# Enterprise Product Readiness

A vendor-neutral checklist and maturity model for taking a software product from "it works" to "an enterprise will buy it, deploy it, and audit it."

> **Status:** early. The framework below is stable; the per-area content is being written. See the [roadmap](ROADMAP.md).

---

## The problem this solves

Most products ship to production successfully and then stall the first time a large customer runs a real evaluation.

What shows up in that evaluation is rarely the feature set. It's SSO, tenant isolation, audit logs, RBAC, a security questionnaire, a SOC 2 report, an RPO/RTO commitment, a DPA, a support SLA. Teams usually discover these one at a time, mid-deal, under time pressure — and each one is an architectural change, not a config flag.

This repo lists them up front so you can decide what to build now, what to build later, and what to say "not yet" to honestly.

## Who it's for

| Role | Use it to |
| --- | --- |
| Engineering / Architecture | Find the changes that get harder the longer you wait |
| Security | Baseline controls before a customer asks for them |
| DevOps / SRE | Scope reliability, DR, and operational work |
| Product | Sequence enterprise work against roadmap pressure |
| Founders / Leadership | Understand what "enterprise ready" actually costs |

## What this is not

- Not a compliance certification, and not a substitute for an auditor or lawyer.
- Not tied to any cloud, vendor, or stack.
- Not a mandate. Plenty of products succeed while skipping large parts of this. The point is to skip deliberately.

---

## How to use it

1. **Score each of the 30 areas** from 1 to 4 using the maturity model below. Be honest; a partially-built control is a 1.
2. **Take the floor, not the average.** Your product's level is the *lowest* score across areas that matter to your buyer. One missing capability fails an evaluation regardless of how strong everything else is.
3. **Pick a target level** and identify the gaps between current and target.
4. **Sort the gaps by reversibility.** Multi-tenancy, identity, and data model decisions are expensive to retrofit. Documentation and support processes are not. Do the irreversible work first.
5. **Re-score quarterly**, or before entering a new market segment.

---

## Maturity model

| Level | Name | Question it answers | Goal |
| --- | --- | --- | --- |
| **1** | MVP | Does it work? | Validate the product |
| **2** | Production Ready | Can we run it for real customers? | Operate reliably |
| **3** | Enterprise Ready | Can we pass an enterprise evaluation? | Win and keep enterprise deals |
| **4** | Enterprise Scale | Can we do this for many customers without breaking? | Scale without operational fragility |

**Level 1 — MVP**
Core functionality, basic UX, basic auth, manual or simple deployment, some tests.

**Level 2 — Production Ready**
Production infrastructure, monitoring and alerting, tested backups, CI/CD, a security baseline, real error handling, acceptable performance, user-facing documentation.

**Level 3 — Enterprise Ready**
Multi-tenancy with enforced isolation, RBAC, SSO/SCIM, audit logging, hardened security controls, high availability, a tested disaster recovery plan, enterprise support with SLAs, compliance evidence, and a repeatable onboarding process.

**Level 4 — Enterprise Scale**
Multi-region, advanced security controls, dedicated and private-network deployment options, automated provisioning, capacity planning, mature SRE practice, and formal, continuously audited compliance.

---

## The 30 capability areas

Grouped for navigation; numbering is stable and maps to file names.

### Foundation

| # | Area | Core question |
| --- | --- | --- |
| 01 | Product | Is the value proposition and scope clear to a buyer? |
| 02 | Architecture | Does the design support the levels you're targeting? |
| 03 | Multi-Tenancy | Is tenant data isolated, and provably so? |

### Security

| # | Area | Core question |
| --- | --- | --- |
| 04 | Identity & Access | SSO, SCIM, MFA, RBAC, least privilege |
| 05 | Application Security | SDLC, dependency and code scanning, pen testing |
| 06 | Data Security | Encryption in transit and at rest, key management, retention, residency |
| 07 | Secrets & Configuration | Secret storage, rotation, environment separation |

### Reliability & Operations

| # | Area | Core question |
| --- | --- | --- |
| 08 | Reliability | SLOs, redundancy, graceful degradation |
| 09 | Performance & Scalability | Load characteristics, limits, capacity headroom |
| 10 | Observability | Logs, metrics, traces, and the ability to answer new questions |
| 16 | Disaster Recovery | Defined RPO/RTO, tested restores, documented failover |
| 17 | Incident Management | On-call, severity levels, customer comms, postmortems |

### Engineering & Platform

| # | Area | Core question |
| --- | --- | --- |
| 11 | DevOps & CI/CD | Repeatable, reversible, auditable releases |
| 12 | Infrastructure | Infrastructure as code, environment parity, network design |
| 13 | Database | Schema evolution, migrations, backups, performance |
| 14 | API Platform | Versioning, deprecation policy, rate limits, webhooks |
| 15 | Testing | Coverage that reflects real risk, not line counts |

### Governance & Compliance

| # | Area | Core question |
| --- | --- | --- |
| 18 | Audit & Governance | Immutable audit trail, change control, access reviews |
| 19 | Compliance & Privacy | SOC 2 / ISO 27001 / GDPR posture and evidence |
| 26 | Legal | Contracts, DPAs, subprocessors, liability, IP |

### Customer Experience

| # | Area | Core question |
| --- | --- | --- |
| 20 | Customer Onboarding | Time to first value, repeatable implementation |
| 21 | Enterprise Administration | Admin controls, user lifecycle, org and team management |
| 22 | Enterprise Deployment | SaaS, private, self-hosted, air-gapped — which do you support? |
| 23 | Documentation | Product, admin, API, and security documentation |
| 24 | Customer Support | Tiers, SLAs, escalation, named contacts |

### Business

| # | Area | Core question |
| --- | --- | --- |
| 25 | Commercial Readiness | Pricing, packaging, contracting, procurement |
| 27 | Product Analytics | Usage visibility, adoption and health signals |
| 28 | Cost Management | Unit economics, cost per tenant, cost observability |
| 29 | Team & Operational Maturity | Ownership, runbooks, bus factor, hiring plan |
| 30 | Enterprise Sales Readiness | Security questionnaires, trust center, reference architecture |

---

## Repository structure

```text
areas/            One file per capability area, with checklists per maturity level
maturity/         The maturity model in detail, with scoring guidance
templates/        Scorecards, gap analysis, security questionnaire responses
examples/         Worked examples of scoring a hypothetical product
```

## Roadmap

Work is ordered by what everything else depends on — the per-area file schema before the 30 files that inherit it, templates before the examples that use them.

[ROADMAP.md](ROADMAP.md) has the sequence, what is deliberately not planned, and how to argue for a different order.

## Contributing

Contributions are welcome, particularly from people who have been through real enterprise evaluations. A requirement a buyer actually asked for is worth more here than one a framework says they should ask for.

Two rules govern everything: stay vendor-neutral, and make every item verifiable. [CONTRIBUTING.md](CONTRIBUTING.md) covers what those mean in practice, how to place an item at the right maturity level, and what to expect from review. Participation is subject to the [Code of Conduct](CODE_OF_CONDUCT.md).

## License

Copyright © 2026 Parth Sankhavara.

Documentation is available under [CC BY 4.0](LICENSE). Use it in your own org however you like — internally, commercially, adapted, or verbatim. The one condition is attribution.

To attribute, copy this:

```text
"Enterprise Product Readiness" by Parth Sankhavara, licensed under CC BY 4.0.
Source: https://github.com/parthbs/product-engineering
License: https://creativecommons.org/licenses/by/4.0/
```
