## Insert before step 1

0. **Delegate when you can.** If a subagent or Task tool is available, run steps 1 to 3 in a subagent (the plugin's `templates/match-score.md` where installed). It reads `profile` and `skills`, builds the requirements string, calls `match`, and returns only: the ceiling and proposed score, the trimmed requirement table with evidence atom ids, the gaps, the `ask` list, and any assistant-directed sentence it found in the posting. Answer from that digest in the shape of step 4. Do not paste `profile`, `skills`, the posting or the raw `match` result into the main conversation. If the digest says an index rebuild is needed, the main agent does the write, following `references/storage.md` ("Write").

## Insert after step 3

Without a subagent: read `profile` and `skills`, pass each verbatim to `match` in the same step, and keep only the ceiling, the table rows that decide the score, the gaps and the `ask` list. Do not repeat the raw result.
