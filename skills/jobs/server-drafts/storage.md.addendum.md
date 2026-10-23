## Large reads

`google_docs__get_document` returns the full document, and a `skills` index or a facts fragment can run to tens of kilobytes. The server does not truncate, and neither should you (see "Read": the checks are only as good as the text they get). Instead, keep the payload out of the main conversation:

- **Read inside a subagent when one is available.** The subagent reads the documents, passes the text verbatim to the career-architect tool, and returns a digest plus the ids the main agent needs for any later write: document id, `modifiedTime`, `revision_id`.
- **Subagents never write.** A new version, a `replace_text`, or a rebuilt `skills` index is done by the main agent, after the concurrency check above and after showing the person the difference.
- **Never echo a document.** Do not print `markdown_content` or a tool result back to the person. Report the line that changed, the atom ids that decide an answer, or the verdict.
- **Write-once reads.** Extract what the task needs the moment you read it. For later turns keep the ids and `modifiedTime`, not the text. Read again when needed.
- **Without a subagent:** hold one document at a time. Read it, use it in the same step, keep the notes above, move on.
- **Shrink before reading:** use `file_name_contains` and `parent_id` in `google_drive__list_files`, and the `# Roles` table in `skills`, to open only the fragments a task cites.
