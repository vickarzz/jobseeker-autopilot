---
name: autopilot-run
description: >
  This skill should be used when a scheduled Jobseeker Autopilot run starts, or when the user says
  "run jobseeker autopilot", "run autopilot now", "jalankan autopilot", "jalankan sekarang".
  One unattended daily pass: sync replies from Gmail, find new matching jobs, fill their application
  forms in Chrome up to the Submit button, and end with a short summary that is emailed to the user.
metadata:
  version: "0.1.0"
---

# Daily autopilot run

Runs without the user watching. Never ask questions mid-run: make the safe choice, note it, carry on.
The user turned autopilot on during setup (Filters `autopilot: on`). That approval covers searching
and filling forms. It never covers pressing Submit, sending email, or anything in
`${CLAUDE_PLUGIN_ROOT}/skills/apply-assist/references/guardrails.md`, which applies in full.

## 0. Load

Read `Profile`, `Filters`, `Applications` and `Skip` from `Jobseeker Autopilot Tracker`.
- `autopilot` is not `on`: stop. Summary: "Autopilot is off."
- Profile empty: stop. Summary: "Profile is empty. Upload your CV in Claude and say: build my profile."
Live board (if `board_url` is set): follow `${CLAUDE_PLUGIN_ROOT}/skills/setup-check/references/board.md`
and keep `run/now` current at every step below.

## 1. Replies

Run the inbox-sync skill. Also flip `Ready to submit` rows to `Submitted` when a confirmation email
("thank you for applying", "application received") matches them.

## 2. New jobs

Run the find-jobs skill without its final question. LinkedIn only if Filters `use_linkedin` is `yes`.
Queue the postings that pass every hard filter and score at least `min_match`, best first, up to
`max_applications_per_day` minus the forms already filled today. Put them on the board as `queued`.
Queued jobs left over from an earlier run go first.

## 3. Fill forms

Check Chrome with `tabs_context_mcp`. Not reachable: leave the jobs queued and say so in the summary.

For each queued job, follow apply-assist "Per job" steps 2 to 6, with these differences:
- The autopilot setting is the approval in step 1. Fit-check still has to pass.
- CV upload: attach `cv_default` if the browser tools can; otherwise leave the CV field and note it.
- Leave the tab open on the filled form. Never press Submit.
- Append the row to `Applications` with Status `Ready to submit`, Applied On empty, and a note naming the tab
  and what is left for the user (consents, login, a question Profile cannot answer).
- Board row: `ready`, note = what is left. A form that cannot be filled: `error` with the reason, Applications Status `Needs manual apply`.
Sequential, one tab at a time, a short pause between sites.

## 4. Summary (this becomes the email)

Set `run/now` to idle. End the run with only this, in the user's language (Filters `language`, default English):

```
Jobseeker Autopilot · <date>

Ready to submit (<n>): open Chrome, check each tab, tick the consents, press Submit
- <Company> · <Role> · <City> · <match>% · <what is left>

Replies
- Interview / assessment: <Company> · <Role> · <deadline or next step>
- Rejected: <Company> · <Role>

Skipped today: <n> (<top reasons>)
Waiting for a reply: <n>
Tracker: <sheet link> · Board: <board_url>
```

Leave out empty sections. Mention `Ready to submit` rows older than 3 days that still have no confirmation email.
No other commentary, no tool names.
