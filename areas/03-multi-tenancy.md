# 03 — Multi-Tenancy

> Is tenant data isolated, and provably so?

**Reversibility: high** — isolation chosen late means rewriting every query path,
re-proving every access route, and migrating live customer data while both models
run side by side.

## Applicability

Skip this area only if you deploy a dedicated instance per customer with no
shared data plane — no shared database, cache, queue, search index, or object
store. That is a legitimate strategy with its own costs, covered in area 22.

A shared control plane over dedicated data planes does **not** exempt you: the
control plane is where cross-tenant mistakes then happen.

## Level 1 — MVP

The product may serve one customer, or a handful sharing one deployment. Nothing
here requires isolation machinery. But the data model decision made now is the
single most expensive one in this area to reverse, and it is usually made by
accident.

- [ ] The tenancy model is a deliberate, recorded decision — shared data plane,
      dedicated instance per customer, or a hybrid
      *Evidence:* a design note or ADR naming the choice and why it was made
- [ ] Every table that will ever hold customer data carries a tenant identifier,
      even while only one tenant exists
      *Evidence:* the schema, or the migration that introduces the column

## Level 2 — Production Ready

Several customers share one deployment. Isolation is enforced in application
code, consistently, on every path — and something fails loudly when it is not.

At this level isolation is a discipline. A single query that forgets its tenant
filter is a data breach, and nothing below the application will catch it.

- [ ] Every read and write is scoped by tenant identifier
      *Evidence:* an automated test that fails when a cross-tenant read returns rows
- [ ] The tenant identifier is derived from the authenticated session and never
      accepted from client input
      *Evidence:* the request-handling path where tenant context is established
- [ ] Background jobs, scheduled tasks, and operator scripts carry tenant context
      the same way request handlers do
      *Evidence:* a job that refuses to run without tenant context
- [ ] Caches, queues, object storage paths, and search indexes are keyed by tenant
      *Evidence:* the key format, plus a test that a cached response cannot be
      served to a different tenant
- [ ] Deleting a tenant removes or anonymizes that tenant's data everywhere it
      lives, including derived stores
      *Evidence:* a documented deletion procedure listing every store it touches

## Level 3 — Enterprise Ready

A buyer will ask you to prove isolation, not describe it. Enforcement moves below
the application, so that a bug in one query cannot expose another customer's
data, and every deliberate crossing is authorized and recorded.

This is the level where "we're careful" stops being an answer.

- [ ] Isolation is enforced at the data layer as well as in application code —
      row-level security, per-tenant schemas, or per-tenant databases
      *Evidence:* the policy or schema definition, plus a test showing an
      unscoped raw query returns nothing
- [ ] Every cross-tenant access path — support tooling, admin console, data
      export, analytics — is explicit, authorized, and logged per access
      *Evidence:* audit entries naming operator, tenant, records touched, and
      reason; see area 18
- [ ] Isolation tests run on every change and a failure blocks release
      *Evidence:* the CI job, and a record of it failing against a deliberately
      introduced violation
- [ ] Tenant provisioning and offboarding are automated and leave no residue
      *Evidence:* a provisioning run, plus a verification that offboarding left
      nothing behind
- [ ] The isolation model is documented for buyers in terms they can evaluate
      *Evidence:* an architecture description in the trust centre; see area 30
- [ ] A penetration test or independent review has specifically targeted
      cross-tenant access
      *Evidence:* the report section covering tenant isolation; see area 05

## Level 4 — Enterprise Scale

Many tenants, unequal in size and in what they demand. Some buyers require their
own keys, their own region, or their own infrastructure — and one tenant's load
must not become another tenant's incident.

- [ ] Per-tenant encryption keys are supported, and customer-managed keys are
      available to buyers who require them
      *Evidence:* the key hierarchy, and a rotation performed without downtime;
      see area 06
- [ ] A tenant can be placed in a named region and its data provably stays there
      *Evidence:* the residency configuration, plus evidence that cross-region
      access is blocked rather than merely avoided
- [ ] Per-tenant quotas or limits prevent one tenant degrading others
      *Evidence:* the limits, and a load test showing containment; see area 09
- [ ] A dedicated or single-tenant deployment option exists for buyers who
      require it
      *Evidence:* the deployment path, and at least one customer running on it;
      see area 22
- [ ] Cost and resource usage are attributable per tenant
      *Evidence:* a report showing infrastructure spend for a named tenant over a
      billing period; see area 28
- [ ] A tenant's data can be exported or migrated between deployment models on
      request
      *Evidence:* a completed export or migration, end to end

## Related areas

- **04 Identity & Access** — tenant membership and role are resolved here.
  Isolation is only ever as good as the identity it trusts.
- **06 Data Security** — per-tenant keys, retention, and residency are the
  level-4 form of isolation.
- **13 Database** — where isolation is enforced at level 3, and where a migration
  can silently remove it.
- **18 Audit & Governance** — every deliberate cross-tenant access must be
  attributable to a person and a reason.
- **22 Enterprise Deployment** — dedicated and single-tenant deployments are the
  answer to buyers this area cannot satisfy.
- **28 Cost Management** — shared infrastructure makes per-tenant cost invisible
  unless it is deliberately measured.
