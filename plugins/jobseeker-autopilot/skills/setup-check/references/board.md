# Live status board

A private claude.ai page that shows every job and its status while Claude works.
Its address is stored in Filters key `board_url`. Writes go through the `ArtifactData` tool
(load it with ToolSearch if deferred). If the Artifact or ArtifactData tool is not available
(for example in Claude Code), skip the board; the tracker sheet still gets every update.

## Create it (setup-check, once)

1. Copy `${CLAUDE_PLUGIN_ROOT}/skills/setup-check/assets/board.html` into the working or scratchpad directory.
2. Publish it with the Artifact tool: icon `list`, capabilities
   `{"db":{"rules":[{"path":"","read":"view","write":"owner"}]}}`.
3. Write the returned URL to Filters `board_url`.
4. Seed it from the tracker: one `jobs` row per Applications and Skip row (batch, 50 per call).

## Data

`jobs/<id>`. Id: `<company>-<role>` lowercased, non-alphanumerics replaced by `-`, at most 100 characters.
Keep the same id for the life of the job.

| Field | Value |
|---|---|
| company, role | as on the posting |
| city | city only, e.g. `Vilnius` |
| status | one of the values below |
| match | integer score from fit-check, if any |
| channel | LinkedIn Easy Apply, Ashby, Workday, Email... |
| link | https posting URL |
| note | one short line: what the user must do, or why it was skipped |
| updated | ISO time with offset, now |

`run/now`: `state` (`running` or `idle`), `activity` (one line, e.g. "Mengisi form Wise · 2 dari 5"),
`scanned`, `passed`, `updated`.

## Statuses

| status | Board shows | Set when |
|---|---|---|
| queued | ANTRE | user approved it, not started |
| filling | DIISI | the form is open and being filled |
| ready | SIAP SUBMIT | filled; note says what is left and which tab |
| sent | TERKIRIM | success page seen or user confirms |
| pending | MENUNGGU | waiting on a referral or a third party |
| error | GAGAL | could not finish; note says why |
| interview / offer / rejected | INTERVIEW / OFFER / DITOLAK | from inbox-sync |
| skip | DILEWATI | filtered out; note gives the reason |

## Rules

- Write the new status before starting the step, so the board moves while you work, and `run/now` at each step.
- Set `run/now` to `idle` with a one-line summary when the batch ends.
- More than two writes at once: one `batch` call. Updates need `if_version`: keep the version from each write result.
- No phone numbers, emails, salary or other personal data on the board.
