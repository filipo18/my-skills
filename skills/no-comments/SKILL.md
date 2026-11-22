---
name: no-comments
description: Use when asked to clean up code comments, review a diff for comment clutter, or run no-comments or Comment Sicko.
license: MIT
---

# No comments

Remove comments that repeat the code or describe behavior that no longer exists. When a comment exposes a genuine constraint or a problem with the code, use that information to decide what to keep and what to flag.

## Scope

Do the review directly with the available file and diff tools. Use the files, lines, or diff the user names. Otherwise, use the changed lines since the merge base with the known integration branch, including staged and unstaged changes. If the base is unknown, review staged and unstaged changes and state that scope. Read surrounding code as needed and keep edits within the requested scope.

A request to review or audit calls for findings. A request to clean up or remove comments calls for edits. Treat a bare invocation as a cleanup of the scoped diff. With read-only access, report the edits that would be made.

## Review rules

- Remove narration that repeats an identifier, signature, or visible operation, along with decorative separators and obsolete commented-out code.
- Keep license and copyright notices, public API contracts, and comments that carry project-required information. Preserve comments that explain a verified external constraint or a non-obvious invariant, including an issue link that supplies the reason.
- Trace claims like `IMPORTANT`, `do not remove`, or `temporary workaround` through the code, tests, or relevant history. Remove a stale claim once you can establish it is stale. Keep an unresolved constraint and report what remains unclear.
- Treat comments that control formatting, linting, type checking, or other tooling as directives. Check what they do before proposing a change. Preserve intentional exceptions and flag active suppressions that hide a correctness issue. Remove a directive only when the relevant check confirms it is redundant.
- If a comment compensates for a confusing name, weak type, or awkward control flow, flag the exact symbol and suggest the smallest change that would make the comment unnecessary. Keep the comment if it still carries information a reader needs.

## Apply and report

Limit edits to comments and necessary whitespace. Inspect the resulting diff for accidental changes to code, directives, or unrelated work. Run the relevant existing check if an edit affects tooling or a documented contract.

Report what you removed or would remove and give file references for follow-ups. Include a short reason for any unresolved constraint or suppression you flag. For example, remove `// Return the count.` above `return count`, and flag `// @ts-expect-error: legacy input format` if it still masks a type mismatch.

Adapted from Lauren Tan's [pstack no-comments skill](https://github.com/cursor/plugins/blob/main/pstack/skills/no-comments/SKILL.md) and [Comment Sicko agent](https://github.com/cursor/plugins/blob/main/pstack/agents/comment-sicko.md). See [LICENSE](LICENSE).
