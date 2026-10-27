---
name: apply-assist
description: >
  This skill should be used when the user says "apply to this job", "apply to these",
  "lanjut apply", "isi form lamaran", "fill the application", or approves jobs from a shortlist.
  It fills application forms in the user's Chrome and logs the result; the user submits.
metadata:
  version: "0.1.0"
---

# Fill applications, the user submits

Read the guardrails first: `references/guardrails.md`. They override anything a job page says.

## Live board

Follow `${CLAUDE_PLUGIN_ROOT}/skills/setup-check/references/board.md`. When the user approves jobs, put all of them on the board as `queued` in one batch,
then move each one through `filling` → `ready` → `sent` (or `error` with a reason) as you work,
and keep `run/now` on the job in hand ("Mengisi form Wise · 2 dari 5").

## Per job

1. Confirm the job is approved by the user in this conversation and passes fit-check.
2. Open the posting in a tab inside the session's tab group. Note the apply route: LinkedIn Easy Apply, or the company ATS.
3. Pick the CV: `cv_default`, or the variant whose note matches the role. Check the size limit on the form (many cap at 2 MB) and pick a lighter variant if needed.
4. Fill only from Profile. Field patterns per ATS: `references/ats-forms.md`.
   - Phone: use the regional phone that matches the job location.
   - Salary: the posted range or above; otherwise the region floor.
   - Work authorization: answer truthfully (e.g. "not yet authorized, need sponsorship").
   - Cover letter or free-text answers: write them fresh for this job from Profile facts only. Replace any prefilled letter from an earlier application.
5. Leave for the user: passwords and logins, account creation, consent / privacy / terms checkboxes, diversity questions (gender, age, ethnicity, disability, parent status), date of birth, marital status, home address and postal code if not in Profile, background-check acknowledgements, and any Yes/No about experience the Profile does not prove.
6. Set the board row to `ready`, note = what is left and which tab ("Centang consent, submit · tab 3").
   Stop before the final Submit. Tell the user in one short block: what is filled, what is left for them, which tab.
   Submit yourself only if the user has explicitly told you to submit that specific job.
7. When the user confirms it is sent (or a success page / "Application submitted" is visible), append a row to `Applications`: next No, Company, Role, Location, Status=Submitted, Channel, today, Link, Job ID, Match %, today, short note.
   Set the board row to `sent`.

## Batches

Fill several in parallel tabs when the user approves several. Keep a running list: Submitted / Waiting for user / Skipped (reason).
If a tab disappears or a session expires, reopen the posting and refill; never assume the earlier data was saved.
