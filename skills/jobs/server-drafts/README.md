# Server-side drafts

The Jobs workflow guides (`start`, `workflows/score.md`, `references/storage.md`) are served live by the connector's `guide` tool, not from this repo. These files are paste-ready additions for the administrator to publish there. They change nothing until published; once published, every user gets them immediately because the guides are fetched at the start of each task.

Written against Jobs server `skill_version` 2.3.0. Check each insertion point against the current guide before pasting.

| Draft | Insert into |
|---|---|
| `start.addendum.md` | `start`, after the "Route" table |
| `score.md.addendum.md` | `workflows/score.md`, before step 1, and a line after step 3 |
| `storage.md.addendum.md` | `references/storage.md`, new section before "Limits the server enforces" |

Step-by-step publishing, checks and rollback are in `PUBLISHING.md`.

Users on older plugin copies do not have the bundled templates. The addenda therefore carry the essential rules in a self-contained form and refer to the templates only as "where available".
