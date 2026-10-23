---
name: jobs
description: Career assistant that scores job postings against a person's verified work history, writes tailored resumes and cover letters that claim nothing their records do not support, prepares interviews, researches applications and keeps the application tracker. Each person's qualifications live in their own Google Drive (a "Career Architect" folder); resumes, cover letters and the tracker live in Reactive Resume. Use it for anything about a job posting, resume, cover letter, application, interview or job-search research, and for first-time setup of a person's career records.
license: MIT
compatibility: Needs the Jobs connector that ships in this plugin, connected and signed in (Google and Reactive Resume are authorised inside Obot).
metadata:
  author: ConniptionFit
  role: launcher
---

# Jobs

This is a launcher. The instructions, the rules and every workflow are served live by the Jobs connector, so they are always the current version and nothing in this file can go stale.

1. Call the `guide` tool of the Jobs connector with no arguments (it is `career_architect__guide`; your client may show a prefix before that name, and may load tools on demand, so load it first). Follow what it returns.
2. When the instructions say to read a document such as `references/storage.md` or `workflows/score.md`, call `guide` again with that path as `topic`.
3. If there is no `guide` tool, the Jobs connector is not connected. Tell the person to open the Jobs connector (the plugin's Connectors tab) and connect it, sign in, and authorise Google and Reactive Resume when asked. Do not write a resume, letter or score without the instructions: a document nobody checked is what this assistant exists to prevent.

## Protect the context window

The connector returns full payloads (often 20KB to 100KB each). Keep them out of the main conversation.

- **Delegate heavy reads to a subagent** (Task or Agent tool) when available. The subagent reads, runs the checks and returns a digest of about 40 lines. Subagents never write; writes stay here.
- **Zero echo.** Never repeat or dump a raw tool payload or JSON blob in a reply.
- **Delta only.** Report findings as short bullets or a compact table.
- **Write-once reads.** Extract the decision immediately. Do not carry a raw payload across turns; delegate or re-fetch if you need it again.
- **No subagent tool?** Read one document at a time, distill it at once (keep ids, `modifiedTime` and the decision-relevant lines), and move on.

| Task | Delegate with |
|---|---|
| Pull claims from `facts - *`, `profile` or `skills` | `templates/facts-extract.md` |
| Score a posting (`skills`, `profile`, `match`; `build_index` if a facts change is pending) | `templates/match-score.md` |
| Lint a resume or cover letter against its facts | `templates/lint.md` |
| Find one record in `list_applications`, `list_resumes`, `list_cover_letters` | `templates/lookup.md` |

The templates and the full rules (return contract, hard rules for subagents, fallback) are in `references/delegation.md` next to this file. If those files are not present in your copy, apply the bullets above; the server guides stay authoritative.
