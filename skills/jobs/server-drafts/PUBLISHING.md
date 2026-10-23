# Publishing the server-side drafts

For the administrator of the Jobs connector. These steps put the additions in this folder into the guides the connector serves. Nothing here touches a person's data.

Written against guide `skill_version` 2.3.0. If your version differs, re-check each anchor below before pasting.

## Before you start

1. Call the connector's `guide` tool for `start`, `workflows/score.md` and `references/storage.md`, and confirm each anchor in the table exists. If one moved, insert at the nearest equivalent and note it in the commit message.
2. Make sure none of the guides already contain a "Large reads" or "Large reads and delegation" section (avoid duplicates).

## Insertions

| Draft | Guide topic | Insert at |
|---|---|---|
| `start.addendum.md` | `start` | New `##` section directly after the "Route" table, before "## Rules" |
| `score.md.addendum.md`, "Insert before step 1" | `workflows/score.md` | As new step 0, before step 1 ("Read `profile` and `skills`...") |
| `score.md.addendum.md`, "Insert after step 3" | `workflows/score.md` | Directly after step 3 ("Call `match`...") |
| `storage.md.addendum.md` | `references/storage.md` | New `##` section directly before "## Limits the server enforces" |

Paste each draft's text only, not its own heading line from the "Insert before/after" labels in `score.md.addendum.md`.

## After publishing

1. Bump the server's `skill_version` (a minor bump) so the change is identifiable.
2. Call `guide` for each of the three topics and confirm the new text is present.
3. Ask a client to score a short sample posting. Confirm the answer keeps the shape in `score.md` step 4 and that the raw `profile`, `skills` and posting text are not echoed into the reply.
4. If the client has no subagent tool, confirm the fallback wording is followed: one document at a time, distilled at once.

## Rollback

Remove the inserted sections and restore the previous `skill_version`. The additions only change instructions; no documents, tool behavior or stored data depend on them, so rollback has no side effects.

## What the additions rely on

- The plugin's bundled `references/delegation.md` and `templates/` are referenced "where installed". Users on an older plugin copy still get the self-contained rules from these addenda.
- Subagents are read-only. The additions never ask a subagent to write; writes stay with the main agent under `references/storage.md` ("Write").
