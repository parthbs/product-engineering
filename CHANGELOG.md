# Changelog

Notable changes to this project. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

No release has been cut yet, so everything lives under Unreleased. When the
first release happens, this section becomes `0.1.0` and versioning follows
[Semantic Versioning](https://semver.org/spec/v2.0.0.html), read as: a **major**
bump changes the maturity model or the set of capability areas, a **minor** bump
adds areas or checklist items, and a **patch** corrects or clarifies existing
content.

## [Unreleased]

### Added

- `areas/README.md` — the per-area file schema: fixed section order, the
  mandatory evidence line on every checklist item, the reversibility marker the
  gap analysis will sort on, and an index of all 30 areas.
- `areas/03-multi-tenancy.md` — first area file, written against that schema.
  19 items across levels 1 to 4, each naming the artifact that proves it.
- Maturity model with four levels — MVP, Production Ready, Enterprise Ready,
  Enterprise Scale — and the scoring method: score each area 1 to 4, take the
  floor rather than the average, sequence gaps by reversibility.
- The 30 capability areas, grouped for navigation with stable numbering that
  maps to file names.
- `LICENSE` — full CC BY 4.0 legal code, and a copy-paste attribution string in
  the README.
- `SECURITY.md` — scoped to a documentation repository: guidance that would
  weaken a system if followed, and this repository's own supply chain. Private
  vulnerability reporting is enabled.
- `CONTRIBUTING.md` — the three rules (vendor-neutral, verifiable, issue before
  structural change), how to place an item at the right maturity level, and what
  to expect from review.
- `CODE_OF_CONDUCT.md` — Contributor Covenant 2.1.
- `ROADMAP.md` — planned work ordered by what everything else depends on, with
  an explicit "not planned" section.
- Issue forms for the two contribution types the project asks for — missing
  requirements and corrections — both requiring a verifiable restatement.
- Pull request template carrying the contribution rules as a checklist.
- CI on pull requests and pushes to `main`: link check (lychee) and markdown
  lint (markdownlint-cli2).
- `.gitignore` for macOS, Windows, and editor artifacts.

### Changed

- README's Contributing and Roadmap sections replaced with pointers to
  `CONTRIBUTING.md` and `ROADMAP.md`, which now hold that content.
- README's area table links each area to its file as that file is written.
- Markdown normalized repository-wide to satisfy the lint job: table separator
  spacing, blank lines around headings and tables, fenced code block languages.

[Unreleased]: https://github.com/parthbs/product-engineering/commits/main
