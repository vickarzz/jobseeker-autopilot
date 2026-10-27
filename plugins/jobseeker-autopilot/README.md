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

## Daily use

| Say | What happens |
|---|---|
| "find jobs in Germany and Netherlands" | ranked shortlist with match % and reasons |
| "check this job: <link>" | fit check with gaps and blockers |
| "apply to 1, 3 and 5" | forms filled in Chrome; you tick consents and submit |
| "draft an email for this job" | Gmail draft; sent only when you say so |
| "check my application emails" | tracker statuses updated, actions listed |

## What stays with you

Passwords and logins, consent and terms checkboxes, diversity questions, date of birth, home address, the final Submit, and sending emails.

## LinkedIn

LinkedIn does not allow bots. The plugin works slowly in your own browser and caps volume, but your account carries the risk. Company career sites (Greenhouse, Lever, Ashby, SmartRecruiters, Workable) are the default source.
