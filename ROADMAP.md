# Roadmap

The framework is stable. The per-area content is being written.

Work is ordered by what everything else depends on, which is the same principle
the framework applies to enterprise readiness itself: do the decisions that are
expensive to reverse first. A file schema chosen late means rewriting 30 files.
A worked example written late costs nothing but the example.

Status is one of **done**, **in progress**, or **not started**. There are no
dates — this is a personal project, and invented dates would be the kind of
unverifiable claim the framework tells you not to make.

---

## 1. Per-area file schema — *not started*

Define what an `areas/NN-name.md` file contains before writing 30 of them:
section order, how checklist items are phrased, how levels are delimited, how an
area states what it depends on.

Everything below inherits this. It is the most expensive decision to change and
therefore the first one to make.

**Done when:** `areas/README.md` documents the schema and one pilot area file
demonstrates it end to end. Multi-tenancy (area 03) is the intended pilot — it is
the most architecturally irreversible of the 30, so it exercises the hardest
parts of the format.

## 2. Maturity model detail — *not started*

Expand the four levels into scoring guidance: what evidence justifies each score,
how to handle a partially-built control, how to score an area that doesn't apply
to your buyer, and how to decide which areas matter for a given market segment.

The README says to take the floor across "areas that matter to your buyer" but
doesn't define that scoping step. The scorecard cannot be built until it does.

**Done when:** `maturity/` holds the model in enough detail that two people
scoring the same product independently land on the same number.

## 3. The 30 area files — *not started*

One file per capability area, with checklists at levels 1 through 4.

Ordered by how irreversible the underlying decisions are, not by area number.
Multi-tenancy, identity, and data model come first because retrofitting them is
an architectural project; documentation and support processes come last because
they can be added at any point.

**Done when:** all 30 files exist, each with items at every level that applies,
and every item satisfies the verifiability rule in
[CONTRIBUTING.md](CONTRIBUTING.md).

## 4. Scorecard template — *not started*

A scorecard someone can copy, fill in, and use to run the exercise: score per
area, current level, target level, and the floor calculation.

**Done when:** `templates/` holds a scorecard that produces a defensible number
without further instructions.

## 5. Gap analysis template — *not started*

Current versus target per area, with the sequencing guidance the README argues
for: sort gaps by reversibility, not by size or by score.

This is the artifact that turns a score into a plan, and it is where the
framework earns its keep.

**Done when:** `templates/` holds a gap analysis that orders work by
reversibility and explains why.

## 6. Worked examples — *not started*

A hypothetical product scored end to end: the scores, the reasoning behind the
uncomfortable ones, and the plan that falls out.

Examples are written last on purpose. They encode the schema, the scoring
guidance, and the templates, so writing them earlier means rewriting them.

**Done when:** `examples/` holds at least one complete scoring of a hypothetical
product, including at least one area scored lower than the author would like.

## 7. Standards references — *not started*

Map areas to the control frameworks buyers actually cite — SOC 2, ISO 27001,
GDPR, and similar — so a team can see which evaluation questions an area answers.

Deliberately last. It is the item most likely to go stale, and it is worth least
until the areas it points into exist.

**Done when:** areas that map cleanly to a published control reference it, and
areas that don't say so rather than inventing a mapping.

---

## Done

- **Framework.** Maturity model, 30 capability areas, scoring method.
- **Repository hygiene.** CC BY 4.0 license, security policy with private
  vulnerability reporting, structured issue forms, PR template, and CI running a
  link check and markdown lint.

## Not planned

- **A scoring tool or web app.** The exercise is worth more done by hand, in a
  room, with people arguing about the numbers.
- **Certification, badges, or a compliance claim.** This repo is not an auditor
  and will not pretend to be one.
- **Vendor or product recommendations.** Vendor-neutral is a rule, not a phase.

## Influencing this

The order above is a judgement call, not a commitment. If you need something
further down the list sooner — particularly a specific area file — say so in an
[issue](https://github.com/parthbs/product-engineering/issues). Real demand from
someone facing a real evaluation is the best reason to reorder.
