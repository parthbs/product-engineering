# Capability areas

One file per capability area, each holding checklists for maturity levels 1
through 4. This file defines the format every area file follows, and indexes all
30.

If you are adding or correcting content, read [CONTRIBUTING.md](../CONTRIBUTING.md)
first — it covers the rules every item must satisfy. This file covers where
those items go.

## File naming

```text
areas/NN-kebab-name.md
```

The number comes from the [area index](#the-30-areas) and never changes — it is
the stable identity, and other files reference areas by number. The slug can be
renamed if a better name emerges.

Examples: `areas/03-multi-tenancy.md`, `areas/04-identity-and-access.md`.

## Skeleton

Sections appear in this order, in every file:

```text
# NN — Area Name

> The core question, verbatim from the README table

**Reversibility: high|medium|low** — one line on what retrofitting costs

## Applicability          (only when the area can genuinely not apply)

## Level 1 — MVP
## Level 2 — Production Ready
## Level 3 — Enterprise Ready
## Level 4 — Enterprise Scale

## Related areas
```

All four level headings appear in every file, always. A level with no distinct
requirement for this area says so in a sentence and lists no items. This matters
while the repo is incomplete: a reader must be able to tell "nothing is required
here" from "nobody has written this yet."

## The header

**The core question** is copied verbatim from the README's area table, as a
blockquote. If the question needs changing, change it in both places in the same
pull request.

**The reversibility marker** answers: if you skip this and come back in two
years, what does it cost?

| Marker | Means |
| --- | --- |
| `high` | Retrofitting is an architectural project — data model, identity, or isolation decisions that touch everything downstream |
| `medium` | Retrofitting is real work but bounded, usually a subsystem or a process people must adopt |
| `low` | Can be added at almost any point at roughly the same cost |

This is the field the gap-analysis template sorts on. It is what turns the
README's "do the irreversible work first" from advice into a procedure, so it is
worth arguing about when it is wrong.

## Applicability

Include this section **only** when an area can legitimately not apply to a
product — and say precisely under what conditions, rather than leaving it to the
reader to decide they are exempt.

Most areas apply to everyone and omit the section entirely. Do not add it to say
"this applies to all products."

## Level sections

Each level opens with **one short paragraph** describing what that level means
for this specific area, in concrete terms. Not "isolation is stronger here" but
"one datastore, tenant-scoped rows, enforced in application code."

The paragraph is the part that teaches. A reader who scores themselves without
it can tick boxes while missing which gaps are architectural — the exact failure
this project exists to prevent.

Then the items.

For guidance on which level an item belongs at, see
[CONTRIBUTING.md](../CONTRIBUTING.md#placing-an-item-at-the-right-level).

## Item format

Every item is a checkbox followed by a mandatory evidence line:

```markdown
- [ ] Every read and write is scoped by tenant identifier
      *Evidence:* an automated test that fails when a cross-tenant read returns rows
```

The evidence line names the artifact that proves the item: a test, a log, a
record, a document, a configuration, a completed exercise. It is what makes the
item verifiable rather than aspirational.

**If you cannot name the evidence, the item is not finished.** That is the point
of the rule — an item without provable evidence is a claim, and this project
does not collect claims.

Good — the evidence names an artifact someone could actually produce:

```markdown
- [ ] Access reviews are performed at least quarterly
      *Evidence:* the review records, with dates and reviewer
```

Bad — no artifact could settle it, so two people will disagree forever:

```markdown
- [ ] Access management is mature
      *Evidence:* the team's judgement
```

Bad — the evidence restates the item instead of naming what proves it:

```markdown
- [ ] Isolation is tested
      *Evidence:* tests exist
```

Items may reference another area inline when the evidence lives there — write
`see area 18`, not a link, so renames do not break.

## Related areas

A short list of areas this one connects to, each with one line on *how*. Not a
formal dependency graph: no reverse edges to keep consistent, nothing for a
rename to break.

Name the connection, not just the area. "04 Identity & Access — tenant
membership is resolved here; isolation is only as good as the identity it
trusts" tells a reader something. "See also area 04" does not.

## The 30 areas

Numeric order. Files link as they are written; unlinked entries are not yet
started.

| # | Area | Core question |
| --- | --- | --- |
| 01 | Product | Is the value proposition and scope clear to a buyer? |
| 02 | Architecture | Does the design support the levels you're targeting? |
| 03 | [Multi-Tenancy](03-multi-tenancy.md) | Is tenant data isolated, and provably so? |
| 04 | Identity & Access | SSO, SCIM, MFA, RBAC, least privilege |
| 05 | Application Security | SDLC, dependency and code scanning, pen testing |
| 06 | Data Security | Encryption in transit and at rest, key management, retention, residency |
| 07 | Secrets & Configuration | Secret storage, rotation, environment separation |
| 08 | Reliability | SLOs, redundancy, graceful degradation |
| 09 | Performance & Scalability | Load characteristics, limits, capacity headroom |
| 10 | Observability | Logs, metrics, traces, and the ability to answer new questions |
| 11 | DevOps & CI/CD | Repeatable, reversible, auditable releases |
| 12 | Infrastructure | Infrastructure as code, environment parity, network design |
| 13 | Database | Schema evolution, migrations, backups, performance |
| 14 | API Platform | Versioning, deprecation policy, rate limits, webhooks |
| 15 | Testing | Coverage that reflects real risk, not line counts |
| 16 | Disaster Recovery | Defined RPO/RTO, tested restores, documented failover |
| 17 | Incident Management | On-call, severity levels, customer comms, postmortems |
| 18 | Audit & Governance | Immutable audit trail, change control, access reviews |
| 19 | Compliance & Privacy | SOC 2 / ISO 27001 / GDPR posture and evidence |
| 20 | Customer Onboarding | Time to first value, repeatable implementation |
| 21 | Enterprise Administration | Admin controls, user lifecycle, org and team management |
| 22 | Enterprise Deployment | SaaS, private, self-hosted, air-gapped — which do you support? |
| 23 | Documentation | Product, admin, API, and security documentation |
| 24 | Customer Support | Tiers, SLAs, escalation, named contacts |
| 25 | Commercial Readiness | Pricing, packaging, contracting, procurement |
| 26 | Legal | Contracts, DPAs, subprocessors, liability, IP |
| 27 | Product Analytics | Usage visibility, adoption and health signals |
| 28 | Cost Management | Unit economics, cost per tenant, cost observability |
| 29 | Team & Operational Maturity | Ownership, runbooks, bus factor, hiring plan |
| 30 | Enterprise Sales Readiness | Security questionnaires, trust center, reference architecture |
