---
name: fit-check
description: >
  This skill should be used when the user asks "is this job a fit", "check this job",
  "how well do I match", "cek kecocokan", "cocok gak", pastes a job link or description,
  or when find-jobs needs to score a posting against the user's profile and filters.
metadata:
  version: "0.1.0"
---

# Check fit against filters and CV

Load `Profile` and `Filters` from the tracker. Filter keys and their meaning: `references/filters.md`.

## 1. Hard filters (any hit = exclude, give the reason)

Check the full description, not the card:
- Local language required that the user does not speak (e.g. "fluent German", "Dutch C1", "Arabic required", JLPT). "Nice to have" or "a plus" is not a blocker; mention it.
- Work rights: "must already have the right to work", "EU citizens only", "no visa sponsorship", "nationals only", "must be based in <country>", "local candidates only", "own visa". Apply only when the user needs sponsorship there.
- Salary: posted maximum below the user's floor for that region.
- Seniority mismatch: internship, junior or student roles when the user targets senior roles.
- Already applied or in Skip. Do-not-apply companies in Filters.
- Closed or expired posting.
- Postings that forbid AI assistance in applications: do not fill them; tell the user to apply personally.

## 2. Match score (0-100)

Score only against facts in Profile:
- Must-have requirements met (50 points, pro-rata). A requirement written as "essential", "required" or "must" that the user lacks caps the score at 70.
- Years of experience vs. requirement (15).
- Tools and stack overlap (20).
- Domain / industry overlap (10).
- Seniority and scope match (5).

Report: score, the 2-3 strongest matches, and every gap (be explicit, e.g. "needs dbt + Databricks at strong level; profile shows neither").
Apply when the score is at or above `min_match` (default 80) or LinkedIn shows "top applicant", unless the user overrides.

## 3. Visa notes

When the posting says nothing about sponsorship, say so. Add the country rule from `references/filters.md` (for example Germany: EU Blue Card if salary meets the threshold; Netherlands: employer must be a recognised sponsor).
