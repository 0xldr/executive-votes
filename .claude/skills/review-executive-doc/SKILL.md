---
name: review-executive-doc
description: Review a Sky executive vote document for content, structure, formatting, and convention compliance. Use when asked to review, check, or give feedback on an executive vote markdown file in 2025/ or 2026/ (e.g. "review the June 4 exec doc", "check this executive vote").
---

# Review Executive Doc

Structured, constructive review of a Sky executive vote document against the
project checklists, principles, and the established conventions of recent docs.

## Inputs

- The target executive doc (a markdown file in `2025/` or `2026/`). If the user
  didn't name one, ask or infer from the open editor file.

## Process

1. **Read the governing process docs** (source of truth — re-read, don't rely on memory):
   - `processes/executive-doc-review-checklist.md`
   - `processes/executive-doc-creation-checklist.md`
   - `processes/executive-doc-principles.md`
   - `processes/drafting-style-guideline.md`
   - `templates/executive-vote-template.md`
2. **Read 1–2 recent docs of the same shape** from `2025/`/`2026/` to anchor
   conventions: the most recent month, plus an earlier one containing the same
   items. Use them to verify recurring addresses, link styles, and section structure.
3. **Read the target doc in full.**
4. **Produce structured feedback** grouped by severity:
   - 🔴 **Blocking** — broken rendering, wrong/inconsistent addresses, factual errors.
   - 🟠 **Formatting/markdown** bugs.
   - 🟡 **Checklist / convention** gaps.
   - 🔵 **Clarity / accuracy** (constructive).
   - ✅ **Looks good** — call out what checks out, so the author knows it was verified.
5. Cite findings by `file:line`. Do **not** edit the file unless the user asks —
   default to feedback. When you do edit, only apply mechanical fixes and leave
   judgment calls (addresses, value wording) for the author to confirm.

## High-value checks (beyond the checklists)

These recur and are easy to miss. Check each explicitly.

### Markdown rendering bugs
- **Backtick-wrapped links**: a `[text](url)` wrapped entirely in backticks
  renders as literal text, not a link. Put any code span *inside* the link instead.
- **Nested/double links**: a link whose text is itself a link is malformed -
  collapse to one.
- **Bullets missing the space** after the hyphen won't render as list items.
- **Misplaced backticks** that split a word or token.
- **Plain-text trailing links**: the Review and Resources sections (Governance
  forum, Operational Manual, Sky Governance Calendar) must be hyperlinked per the
  template — these are frequently left as plain text.
- **Run markdownlint** over the doc to catch standard Markdown deviations
  (inconsistent list markers, heading levels, spacing, etc.) per the
  `drafting-style-guideline.md` recommendation. If a linter binary is available
  (e.g. `markdownlint`/`markdownlint-cli2`), run it and report findings; otherwise
  check the equivalent rules manually.

### Addresses
- All Ethereum addresses **checksummed** (EIP-55 casing); flag all-lowercase.
- **Verify each address matches its label.** Cross-check recurring entities
  against recent docs; a label paired with an address used for a different entity
  elsewhere is a likely copy-paste error.
- **Verify each address links to the correct block explorer for its chain.**
  Determine each address's chain from its item context (e.g. the `[chain]` tag or
  surrounding text) and confirm the hyperlink points to that chain's explorer
  (Ethereum mainnet → `etherscan.io`, Avalanche → `snowscan.xyz`, Base →
  `basescan.org`, etc.). A mainnet explorer link on a non-mainnet address (or vice
  versa) is a common error.
- Newly deployed contracts must have their **address given and hyperlinked**.

### Consistency
- **Chain tags**: pick one convention per chain and apply it to *every* item;
  watch for a single outlier left behind after a find/replace.
- **Title ↔ Summary ↔ Executive Summary ↔ Proposal Details** must list the same
  items in the same order, ordered by judged impact.
- **Frontmatter summary wording vs. body**: match the precise body wording, 
  especially for numeric/parameter changes.
- **Internal arithmetic**: verify stated deltas and totals add up and are
  consistent with prior docs.
- **Units**: every numeric parameter and amount carries the correct unit, and
  the unit matches the action (e.g. USDS vs USDC, hours vs days, % vs bps, token
  symbol). Flag missing, mismatched, or wrong-denomination units.

### Spelling & grammar
- Read for spelling and grammatical correctness throughout. Flag typos, wrong-word
  errors, and broken sentences. Use the project's spelling conventions — do not
  flag intentional protocol terms, ticker symbols, or technical identifiers.

### Framing & links
- Top-level items use future-conditional framing: "If this executive proposal
  passes, then…".
- Each top-level item has **Authorization** and **Proposal** links.
- GSM Pause Delay value, office-hours modifier, and expiry are present, and the
  GSM value reflects the current setting (confirm, don't assume).
- `$` placeholders: only `address: "$spell_address"` should remain; flag any other.

### Parameter tables — confirm intentional asymmetry
- When a list of assets each carry a set of parameters but one entry is missing a
  line its siblings have, flag it to confirm it's deliberate, not an omission.

## Proxy spell items — scope exclusions (IMPORTANT)

The Spark/Grove **Prime Agent / Star proxy spell** sub-items follow different
conventions. Do **not** flag the following for proxy spell content:

- **Safe Harbor Update**: proxy spell contracts (the proxy spells themselves and
  the contracts they touch — e.g. ALM Proxy Freezable upgrades, CCTPv2 receivers,
  vaults onboarded inside a Spark/Grove spell) are **out of scope**. Only assess
  core/main-spell contracts for the template's Safe Harbor section.
- **Bug Bounty "new contracts" check**: same exclusion — proxy spell contracts are
  not relevant.
- **Prior/before values**: proxy spell items state new values only by convention.
  Only suggest "from X to Y" framing for main-spell items (e.g. core risk
  parameters like ALLOCATOR-SPARK-A DC-IAM, the MKR-to-SKY penalty), not for proxy
  spell parameter changes (reserve factors, caps, rate limits inside Spark/Grove
  spells).

## Process / awareness checks (can't verify from the file — raise as questions)

- **Parties implicated**: if the spell offboards or removes an external party,
  confirm that party is aware of the wording used.
- **Standby Spells**: if an ilk is onboarded/offboarded, a `dss-emergency-spells`
  README PR is likely required.
- **Atlas active elements**: if the spell changes values tracked in Sky Atlas, a
  `next-gen-atlas` PR should exist.
- **Hash verification**: confirm the author's hash once the doc is approved.
