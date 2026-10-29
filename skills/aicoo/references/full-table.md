# Aicoo full tables

Use Aicoo's connected tools first. Aicoo full tables are structured document blocks (`type: db`), distinct from plain Markdown tables (`type: table`). Reading a full table as Markdown does not mean the same interface can write it.

## Choose the supported editing path

1. Find the requested document with `search` / `list_docs`, then `read_doc`. Identify the specific block by id, title and columns. Ask for a link only if discovery leaves the target ambiguous.
2. Inspect the available tool schema and current capabilities. The interface inspected on 2026-10-29 has no full-table mutation tool; `edit_doc` does not accept `fulltable` as an insert type. The local server implementation rejects replacing a `db` block with “A table can only be changed in aicoo.” Recheck capabilities in later sessions rather than treating this as permanent.
3. When the connector cannot perform the requested change, explain that briefly and use the signed-in Aicoo web UI through available browser/computer tools. The user's request to edit authorizes ordinary scoped UI edits; do not ask again solely because the transport changes. If sign-in is required, ask the user to complete sign-in.
4. If a future connector supports full tables, use its documented schema and review flow. For `edit_doc` / `apply_edit`, show the returned diff and obtain the required approval before applying. Never invent a table endpoint or bypass that review through another API.

## Edit and verify in the Aicoo UI

- Open the exact document and full table, inspect existing columns, types, choices, formulas, rows and active filters before changing them. A filtered view may hide records.
- Use native cell, column and view controls for the requested operation. Preserve row identity and unrequested data, formulas, column types, choices, views and linked form settings.
- For a linked collection form, inspect its form controls separately: a column label, form question, required flag and visible field may be different settings. Do not publish or change sharing unless requested.
- Make small, reviewable changes. Re-read the edited values and check that saving completed; for structural edits, reopen the table and verify the affected field configuration. Report only verified results.
- If UI tools are unavailable or the required control is missing, state the exact blocked operation and provide the prepared edits. Do not report a successful write.

## Boundaries

Do not delete and recreate a full table as a workaround, replace it with Markdown, use Feishu tools, or write directly to its backing database. Those approaches can lose metadata or bypass permissions and version checks. Full-table creation/editing supported by Aicoo's built-in AI is not proof that an external agent API supports it. In particular, do not assume a fenced `fulltable` block has special meaning in external `create_doc`.

Verification basis: Aicoo's public `https://www.aicoo.io/skill.md`, the connected MCP schema, and the Aicoo implementation's `api/_lib/agentcore.js` (`normalizeOps`) and `api/_lib/agentmd.js` (`blocksMarkdown`). This skill adds routing and UI fallback, not new server capabilities.
