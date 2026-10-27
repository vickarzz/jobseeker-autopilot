---
name: setup-check
description: >
  This skill should be used when the user says "set up jobseeker autopilot", "start jobseeker autopilot", "set up job autopilot",
  "check my setup", "is the plugin working", "health check", "cek setup", "cek plugin",
  or before the first job search in a new account. It verifies that Gmail, Google Drive/Sheets
  and Claude in Chrome are connected and working, and creates the tracker sheet.
metadata:
  version: "0.1.0"
---

# Setup and health check

Run every check below, then report one table: Check | Status (OK / Missing / Error) | What to do.
Never stop at the first failure; finish all checks so the user sees everything at once.

## 1. Connectors

For each connector, load its tools (ToolSearch if deferred) and make one harmless read call.

| Connector | Test call | Needed for |
|---|---|---|
| Gmail | search threads with query `newer_than:1d`, max 1 result | recruiter emails, status sync, drafts |
| Google Drive | search files named "Jobseeker Autopilot" | storing CV and profile |
| Google Sheets | read the tracker (step 2) | tracker |
| Claude in Chrome | `tabs_context_mcp` | filling application forms, LinkedIn |
| Artifacts | Artifact and ArtifactData tools present | live status board (optional) |
| Scheduling | a scheduled-task tool present | daily autopilot run (optional) |

- Tool absent: status Missing. Tell the user which connector to add in Claude settings (Connectors) or, for Chrome, to install the Claude in Chrome extension and keep Chrome open. If a connector-suggestion tool is available, offer it.
- Tool present but the call errors: status Error, quote the error in one line, suggest reconnecting.
- Chrome present but no browser reachable: status Error, ask the user to open Chrome with the extension signed in.

## 2. Tracker sheet

Search Drive for a spreadsheet named exactly `Jobseeker Autopilot Tracker`.

- Found: read the first row of each tab and confirm these tabs and headers exist; add any missing tab or header.
- Not found: create it with the tabs below, then report its link.

| Tab | Columns |
|---|---|
| Applications | No, Company, Role, Location, Status, Channel, Applied On, Link, Job ID, Match %, Last Update, Notes |
| Profile | Key, Value |
| Filters | Key, Value |
| Skip | Company, Role, Link, Reason, Date |

## 3. Profile and filters

Read the Profile and Filters tabs.
- Empty Profile: tell the user the next step is to share their CV ("upload your CV and say: build my profile").
- Empty Filters: list the filter keys from `${CLAUDE_PLUGIN_ROOT}/skills/fit-check/references/filters.md` and ask for the ones that matter most (countries, minimum salary, visa sponsorship needed, languages, target roles).
- If the user pasted a settings block from the Jobseeker Autopilot web page (it starts with `JOB-AUTOPILOT-SETTINGS`), write each `key: value` line into Filters and confirm.
  Lines starting `profile_hint.` are hints for the profile, not filters.
- If the block has a `CV-TEXT` ... `END-CV` section, build the profile from that text with the profile-from-cv skill
  (it counts as the CV). Ask in one message for the "ask" fields still empty, and for the CV file itself (PDF or DOCX)
  so forms can attach it; save it as profile-from-cv step 5 says.

## 4. Status board

If Filters has no `board_url`, create the live board and seed it from the tracker as described in
`references/board.md`. If it exists, open it once with the Artifact tool (`read`) to confirm it still loads.
Add a row "Status board" to the summary table with its link.

## 5. Daily autopilot

Only when Filters has `autopilot: on` (from the web page) or the user asks for a daily run.

1. Find the session's scheduling tools (ToolSearch "scheduled task" or "create_trigger"). None: say a daily
   run cannot be set up here and that "run autopilot now" works any time.
2. List existing scheduled tasks; if one named `Jobseeker Autopilot` exists, update it instead of adding another.
3. Create it:
   - name `Jobseeker Autopilot`
   - schedule: every day at Filters `run_time` (default 10:00) in Filters `timezone`
     (`CRON_TZ=<timezone> <min> <hour> * * *`; the tool may move it a few minutes earlier, which is fine)
   - prompt: `Run the Jobseeker Autopilot daily run (autopilot-run skill) for the "Jobseeker Autopilot Tracker" sheet.`
   - needs the user's computer (Chrome), email and push notifications on (the summary is the status email)
4. Write `autopilot_task` (task name and time) to Filters. Tell the user in one line when it runs, that Chrome and
   the Claude desktop app must be open then, and whether runs need approval (if so, point to the task's
   automatic-approval setting).
5. Offer to run it once now ("run autopilot now").

## 6. Summary

End with the table and one line: "Ready" when all checks pass, otherwise the single most important fix.
Do not change any account settings yourself.
