# Security Policy

## What this repository is

This repository publishes documentation — a checklist and maturity model. There is
no service, no application, no published package, and no executable code beyond the
GitHub Actions workflows used to lint the docs.

That means there is no deployed system here to attack, and no "supported versions"
table to maintain: the current state of `main` is the only version, and it is the
one that gets fixed.

## What is worth reporting privately

Two things in a repository like this can genuinely cause harm, and both should come
to us privately rather than through a public issue:

1. **Guidance that weakens security if followed.** An item that recommends an unsafe
   practice, describes a control in a way that produces false assurance, or would
   lead a team to believe they have coverage they don't have. A checklist that tells
   people the wrong thing is the security defect this project can actually ship.

2. **Problems with this repository's own supply chain.** A compromised or
   suspiciously modified GitHub Actions workflow, an action resolving somewhere
   unexpected, or credentials or secrets committed to the history.

## How to report

Use GitHub's private vulnerability reporting:

**[Report a vulnerability](https://github.com/parthbs/product-engineering/security/advisories/new)**

That opens a private channel visible only to the maintainer. Please don't open a
public issue for either category above.

Include what the problem is, where it appears, and — for guidance defects — what a
team would wrongly conclude if they followed it as written.

## What not to send here

- **Vulnerabilities in your own product or a third party's.** This project can't
  help with those, and please don't send details of an unfixed issue in someone
  else's system to an unrelated repository.
- **General security questions**, or disagreements about whether an item is right.
  Those are ordinary [issues](https://github.com/parthbs/product-engineering/issues)
  and are better discussed in the open.

## What to expect

This is a personal, best-effort project, not a funded security program. Reports are
acknowledged as soon as they're seen — usually within a few days, but there is no
guaranteed response time and it would be dishonest to publish one. Valid guidance
defects are corrected in `main` and noted in the changelog. Credit is given unless
you'd rather stay anonymous.
