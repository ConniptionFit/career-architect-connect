## Large reads and delegation

Full tool payloads are normal and can run to 100KB each. Keep them out of the main conversation:

- Where a subagent or Task tool exists, delegate facts extraction, `build_index` / `match` scoring, `lint_resume` / `lint_cover`, and broad listings (`list_applications`, `list_resumes`, `list_cover_letters`) to it, and answer from its digest (about 40 lines, no raw JSON). Subagents read and analyze only; writes stay with the main agent.
- Never repeat or dump a raw payload in a reply. Report only what decides the answer, as bullets or a compact table.
- Treat a large read as write-once: extract the decision at once and do not carry the raw text into later turns. Re-delegate or re-fetch instead of quoting from memory.
- Without a subagent tool, read one document at a time, pass it verbatim to the check that needs it in the same step, keep only ids, `modifiedTime` and the decision-relevant lines, then move on.

The plugin's bundled `references/delegation.md` and `templates/` hold standard subagent prompts for these tasks, where installed.
