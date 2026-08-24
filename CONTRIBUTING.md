# Contributing

Contributions are welcome, particularly from people who have been through real
enterprise evaluations. What a buyer actually asked for is worth more here than
what a framework says they should ask for.

By participating you agree to the [Code of Conduct](CODE_OF_CONDUCT.md).

## Useful contributions

- **Requirements you were asked for that aren't listed.** The most valuable
  contribution to this repo. If an evaluation asked you for something the 30
  areas don't cover, that's a gap worth closing.
- **Corrections.** A checklist item that is wrong, vague, or unmeasurable is a
  defect, not a matter of taste.
- **Clarity edits.** Same meaning, fewer words, less ambiguity.

Two things this repo is deliberately not collecting: vendor recommendations, and
requirements you think enterprises *should* have. Both make the checklist longer
without making it more accurate.

## The three rules

Every contribution is judged against these. They are also the fastest way to get
a change merged without a review round-trip.

### 1. Stay vendor-neutral

Describe the capability, not the product that provides it. A team on any stack
should be able to read an item and know whether they have it.

| | |
| --- | --- |
| Yes | "Secrets are stored outside source control and can be rotated without a redeploy." |
| No | "Secrets are stored in HashiCorp Vault." |

### 2. Every item must be verifiable

Someone should be able to answer yes or no without arguing about definitions. If
two competent people could read an item and disagree about whether their product
meets it, the item is not finished.

| | |
| --- | --- |
| Yes | "Access reviews are performed and recorded at least quarterly." |
| Yes | "Tenant isolation is enforced at the data layer and covered by an automated test that fails if cross-tenant reads succeed." |
| No | "Has good security." |
| No | "Access management is mature." |

The usual fix for an unverifiable item is to name the artifact that proves it —
a record, a test, a document, a log — rather than the quality it implies.

### 3. Open an issue before large structural changes

Adding an item to an existing area: open a PR directly. Renaming an area,
changing the maturity model, adding a 31st area, or restructuring how area files
are organized: open an issue first. These ripple across every other file, and
it's better to disagree before you write.

## Which change am I making?

**Adding an item to an existing area.** Pick the area by its number, pick the
maturity level, and write the item to the rules above. Use the
[Missing requirement](https://github.com/parthbs/product-engineering/issues/new?template=missing-requirement.yml)
issue form if you'd rather describe it than draft it.

**Fixing an existing item.** Use the
[Correction](https://github.com/parthbs/product-engineering/issues/new?template=correction.yml)
form, or open a PR with the replacement text. Say what a team would wrongly
conclude if they followed the current wording — that's the part that's hard to
reconstruct later.

**Proposing a new area.** Open an issue first. A new area has to clear a higher
bar than a new item: it must be something an enterprise evaluation asks about
that doesn't reasonably fit any of the existing 30, and it must be distinct
enough that scoring it separately tells you something scoring its neighbours
doesn't. Most proposed areas turn out to be items inside an existing one.

**Changing the maturity model.** Open an issue. The four levels are load-bearing
for all 30 areas.

## Placing an item at the right level

The levels answer different questions, and an item belongs at the level whose
question it answers:

| Level | The question | An item belongs here if |
| --- | --- | --- |
| 1 — MVP | Does it work? | Its absence means the product doesn't function |
| 2 — Production Ready | Can we run it for real customers? | Its absence causes outages, data loss, or unsupportable operations |
| 3 — Enterprise Ready | Can we pass an enterprise evaluation? | A buyer asks for it during evaluation and its absence can block a deal |
| 4 — Enterprise Scale | Can we do this for many customers without breaking? | It only becomes necessary at scale, or for the most demanding buyers |

When an item could sit at two levels, put it at the lower one and describe the
stronger form at the higher one. "Backups exist and a restore has been tested"
at level 2; "RPO and RTO are defined, contractually committed, and verified by a
scheduled restore test" at level 3.

## Opening a pull request

The PR template carries the checklist. Beyond that:

- **One concern per PR.** A new item and a clarity sweep are two PRs.
- **Say where it came from.** "A public-sector buyer asked for this during
  security review" tells a reviewer more than any argument about why it matters.
- **CI must pass.** Two checks run: a link check and markdownlint. Both are
  fast, and both fail loudly enough to tell you what to fix.

You can run the markdown lint locally before pushing:

```bash
npx markdownlint-cli2
```

## Review

Pull requests are reviewed by the maintainer. Expect one of:

- **Merged.** Usually within a few days.
- **A question.** Most often "how would someone verify this?" — the answer
  normally becomes the item's final wording.
- **Redirected.** The contribution is right but belongs in a different area or
  at a different level.
- **Declined,** with a reason. Most declines are items that can't be made
  verifiable, or that are really about a specific product.

This is a personal, best-effort project. There is no response-time commitment,
and it would be dishonest to publish one.

## Security

If you've found guidance here that would weaken a system if followed, don't open
a public issue — see the [security policy](SECURITY.md).
