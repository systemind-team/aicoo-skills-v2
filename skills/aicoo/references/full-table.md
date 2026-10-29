# Aicoo full tables

Use Aicoo's connected tools first. Aicoo full tables are structured document blocks (`type: db`), distinct from plain Markdown tables (`type: table`). Reading a full table as Markdown does not mean the same interface can write it.

## Choose the supported editing path

1. Find the requested document with `search` / `list_docs`, then `read_doc`. Identify the specific block by id, title and columns. Ask for a link only if discovery leaves the target ambiguous.
2. Inspect the available tool schema and current capabilities. The interface inspected on 2026-10-29 has no full-table mutation tool; `edit_doc` does not accept `fulltable` as an insert type. The local server implementation rejects replacing a `db` block with “A table can only be changed in aicoo.” Recheck capabilities in later sessions rather than treating this as permanent.
3. When the connector cannot perform the requested change, explain that briefly and use the signed-in Aicoo web or desktop UI through available browser/computer tools. The user's request to edit authorizes ordinary scoped UI edits; do not ask again solely because the transport changes. If sign-in is required, ask the user to complete sign-in.
4. If a future connector supports full tables, use its documented schema and review flow. For `edit_doc` / `apply_edit`, show the returned diff and obtain the required approval before applying. Never invent a table endpoint or bypass that review through another API.

## Edit and verify in the Aicoo UI

For a fresh test document, the `/table` insert menu creates a structured table.
Text cells are editable fields; checkbox cells expose checkboxes. Click a column
header to edit its name or type. Commit text edits by leaving the field and wait
for Saved. If accessibility handles become stale after a table rerender, obtain
a fresh full UI tree before retrying. Read back through `read_doc` to verify
server persistence and confirm the block remains `type: db`.


- Open the exact document and full table, inspect existing columns, types, choices, formulas, rows and active filters before changing them. A filtered view may hide records.
- Use native cell, column and view controls for the requested operation. Preserve row identity and unrequested data, formulas, column types, choices, views and linked form settings.
- For a linked collection form, inspect its form controls separately: a column label, form question, required flag and visible field may be different settings. Do not publish or change sharing unless requested.
- Make small, reviewable changes. Re-read the edited values and check that saving completed; for structural edits, reopen the table and verify the affected field configuration. Report only verified results.
- If UI tools are unavailable or the required control is missing, state the exact blocked operation and provide the prepared edits. Do not report a successful write.

## Boundaries

Do not delete and recreate a full table as a workaround, replace it with Markdown, use Feishu tools, or write directly to its backing database. Those approaches can lose metadata or bypass permissions and version checks. Full-table creation/editing supported by Aicoo's built-in AI is not proof that an external agent API supports it. In particular, do not assume a fenced `fulltable` block has special meaning in external `create_doc`.

Verification basis: Aicoo's public `https://www.aicoo.io/skill.md`, the connected MCP schema, and the Aicoo implementation's `api/_lib/agentcore.js` (`normalizeOps`) and `api/_lib/agentmd.js` (`blocksMarkdown`). This skill adds routing and UI fallback, not new server capabilities.

## Verification (2026-10-29)

Live smoke test in a separate private test document: created a full table through
the desktop UI, edited two text cells, checked one checkbox, and renamed a text
column. MCP `read_doc` returned all saved values and the same `db` block id. A
preview-only `edit_doc` replacement was rejected with “A table can only be
changed in aicoo.” Browser automation was unavailable in that run; desktop UI
provided the working fallback. Formula, filter and linked-form changes were not
tested. This is evidence for basic UI editing, not complete table API support.
