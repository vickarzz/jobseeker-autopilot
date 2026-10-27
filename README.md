# Jobseeker Autopilot

A Claude plugin that finds jobs matching your CV and filters, checks the fit, fills applications in your own Chrome for you to submit, drafts recruiter emails, and keeps a Google Sheet tracker in sync with your inbox.

Setup guide: https://vickarzz.github.io/jobseeker-autopilot/

## Install

Claude desktop app (Pro, Max, Team or Enterprise):

1. Open **Customize → Plugins**.
2. Choose **Add marketplace** and enter `vickarzz/jobseeker-autopilot`.
3. Install **Jobseeker Autopilot**.

Or download `docs/jobseeker-autopilot.plugin` and upload it on the same Plugins page.

Claude Code:

```
/plugin install jobseeker-autopilot --marketplace vickarzz/jobseeker-autopilot
```

## First run

In Claude, type `Set up jobseeker autopilot`. Claude checks Gmail, Google Drive, Google Sheets and Claude in Chrome, then creates the tracker sheet. Then upload your CV and say `Build my profile`. Setup also creates a live status board in claude.ai that shows each application moving from queued to filled to submitted.

## Layout

```
.claude-plugin/marketplace.json   marketplace entry
plugins/jobseeker-autopilot/      the plugin
docs/                             setup site (GitHub Pages) and downloadable plugin file
```
