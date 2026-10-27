---
name: profile-from-cv
description: >
  This skill should be used when the user uploads or shares a CV/resume and says
  "build my profile", "read my CV", "update my profile", "baca CV saya", "buat profil dari CV",
  or when another Jobseeker Autopilot skill needs profile data that is missing.
metadata:
  version: "0.1.0"
---

# Build the profile from a CV

The profile is the single source of truth for every application form. Only write facts that are
in the CV or that the user states. Never infer years, tools, degrees, salaries or visa status.

## Steps

1. Read the CV (PDF/DOCX). Extract the fields in `references/profile-fields.md`.
2. Compute total years and years per tool from the dated roles. Show the arithmetic in one line per tool so the user can correct it.
3. Show the extracted profile as a compact table and list every field marked "ask" that is still empty (salary floors, notice period, work authorization, nationality, phone per region). Ask for those in one message.
4. After the user confirms, write the profile to the `Profile` tab of `Jobseeker Autopilot Tracker` (Key, Value). Overwrite only keys that changed.
5. Save the CV file into a Drive folder `Jobseeker Autopilot/CV` if it is not already there, and store its name in Profile key `cv_default`.
6. Suggest 3-6 target role titles and search keywords derived from the CV. Write the ones the user accepts into `Filters` keys `target_roles` and `keywords`.

## Rules

- Experience descriptions: one achievement per line, never a run-on paragraph.
- Education: only the entries the user wants shown; remove parser junk (courses, community roles) unless the user keeps them.
- If the user has several CV variants (for example a Power BI CV and a manager CV), store each in Profile as `cv_<label>` with a one-line note on when to use it.
- Keep sensitive data out of the sheet: no ID numbers, bank details or passwords. Date of birth, gender and marital status stay out too; forms ask the user for them at submit time.
