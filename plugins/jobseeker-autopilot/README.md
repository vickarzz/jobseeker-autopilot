# Jobseeker Autopilot

Finds jobs that match your CV, checks the fit, fills applications in your own Chrome for you to submit, drafts recruiter emails, and keeps a Google Sheet tracker in sync with your inbox. Runs on your own Claude account.

## What you need

- Claude desktop app with this plugin installed
- Connectors: Gmail, Google Drive, Google Sheets
- Claude in Chrome extension, with Chrome open and signed in to LinkedIn and job sites

## First run

1. "Set up jobseeker autopilot" - checks the connectors and creates the `Jobseeker Autopilot Tracker` sheet.
2. Upload your CV and say "build my profile".
3. Paste the settings block from the Jobseeker Autopilot web page, or tell Claude your countries, salary floor, visa needs and languages.

## Autopilot

On the setup page, upload your CV, set your filters and keep "Jalankan otomatis setiap hari" on, then press
Mulai Autopilot and paste into Claude. Every day at the chosen time (default 10:00 local) Claude checks your
inbox for replies, finds new matching jobs, and fills their forms in Chrome up to the Submit button. The run
summary arrives by email: open Chrome, check each tab, tick the consents and press Submit.
The Claude desktop app and Chrome must be open at that time. Say "run autopilot now" to run it any time.

## Daily use

| Say | What happens |
|---|---|
| "find jobs in Germany and Netherlands" | ranked shortlist with match % and reasons |
| "check this job: <link>" | fit check with gaps and blockers |
| "apply to 1, 3 and 5" | forms filled in Chrome; you tick consents and submit |
| "draft an email for this job" | Gmail draft; sent only when you say so |
| "check my application emails" | tracker statuses updated, actions listed |

## Status board

Setup also creates a private live board in claude.ai (link in the Filters tab, key `board_url`). Every job shows up there as Claude works on it: ANTRE, DIISI, SIAP SUBMIT, TERKIRIM, then INTERVIEW or DITOLAK after an inbox sync.

## What stays with you

Passwords and logins, consent and terms checkboxes, diversity questions, date of birth, home address, the final Submit, and sending emails.

## LinkedIn

LinkedIn does not allow bots. The plugin works slowly in your own browser and caps volume, but your account carries the risk. Company career sites (Greenhouse, Lever, Ashby, SmartRecruiters, Workable) are the default source.
