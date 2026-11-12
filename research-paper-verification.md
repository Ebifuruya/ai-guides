---
layout: default
title: "Research Paper Verification v1.3"
nav_order: 5
---

# Research Paper Verification v1.3

*By Ebifuruya*

---

## Context

### Research Paper

The Research Paper is a report to be audited. It is either:

1. The Markdown or DOCX file attached to this prompt.
2. If no file is attached, the most recent Markdown or DOCX report in the current thread.

## Task

Verify the Research Paper. Check:

1. All arithmetic, formulas, unit conversions, and physical constants against published reference values. Show corrected calculations for arithmetic errors.
2. The plausibility of speculative extrapolations — whether the reasoning from established science to novel claims is scientifically sound. Distinguish between "physically implausible" and "uncertain but defensible."
3. Stated facts against training data. Do not use web searches for this check.

### Flagged Fact Resolution

When a factual claim contradicts training data, attempt to clear the flag by fetching the cited source URL. All four conditions must be met in order:

1. The Research Paper has a References section.
2. The factual claim contradicts training data.
3. The factual claim has a numerical inline citation. `(Author Year)` citations will not be checked.
4. The corresponding citation in the References section has a URL. DOI, PMID, and ISBN identifiers when they are hyperlinked URLs.

If any condition is not met, leave the flag standing.

### Input Gate

Before proceeding, confirm all conditions are met. If any condition is not met, abort and notify the user.

1. **Research Paper Present**: A Research Paper has been identified per the Context. If no Research Paper can be identified, abort.
2. **References Section Present**: The Research Paper contains a References section (a heading named "References" at any level) with a numbered list of reference entries. If the section is absent or its entries are not numbered, abort.
3. **Numerical Citations Used**: The Research Paper uses numerical inline citations (superscript numbers, bracketed numbers, or footnote-style markers). If the Research Paper uses author-year citations instead (e.g., "(Smith 2020)"), abort.

## Format

Revision Proposal, organized by the paper's own section structure. Exclude confirmed claims — report only items that are plausible, questionable, or in error.

### Output Structure

For each section containing flagged claims:

- Section heading from the paper
- Each flagged claim, with verdict: ◐ plausible, ⚠ questionable, ✗ error
- For ⚠ and ✗: the specific issue and the correct value or reasoning
- For factual claims: disclose whether the verification relied on training data or a cited source URL

Sections with no flagged claims are omitted.

Summary table of verdict counts at the end. Do not include a count of confirmed claims.

## Constraints

- Do not modify the Research Paper.
