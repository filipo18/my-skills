---
name: explain-review-comment
description: Use when the user explicitly asks for a code review comment, reported defect, or unexpected behavior to be traced and explained without implementing a fix.
---

# Explain review comment

First verify whether the supplied review comment is valid against the current code. Then explain the behavior in plain language. Base the verdict and explanation on code and runtime evidence. Do not implement a fix unless the user separately asks for one.

## Investigation

1. Identify the exact repository, branch, files, symbols, and user-visible flow named or implied by the comment.
2. Verify the comment's premise before explaining it. Classify it as valid, partially valid, unsubstantiated, or incorrect based on the available evidence. Do not assume a review comment is correct merely because a reviewer stated it confidently.
3. Read the surrounding code and trace the execution path far enough to establish the trigger, observed behavior, expected behavior, and cause.
4. Check tests, callers, configuration, and recent changes when they affect the conclusion.
5. Distinguish confirmed facts from assumptions. If the expected behavior is not documented or encoded in tests, say what evidence supports the interpretation.
6. Do not modify files, post review replies, or propose a patch unless the user asks.

## Response contract

Present the result in this order:

1. **Verdict.** State whether the comment is valid, partially valid, unsubstantiated, or incorrect, and name the strongest evidence for that conclusion.
2. **When it happens.** State the inputs, state, permissions, timing, or sequence required to trigger it.
3. **What happens.** Walk through the actual execution path and visible result.
4. **What should happen.** Describe the intended result and cite the evidence for it.
5. **Where the cause is.** Name the root cause, not only the symptom. Include precise file and line references when available.
6. **How to reproduce it in the UI.** Give numbered steps with prerequisites and the result to observe. If UI reproduction is impossible or unverified, say why and give the closest useful verification method.

Keep the causal chain concrete. Include only code that helps explain the issue. Call out missing evidence or validation boundaries instead of guessing.

## Final writing pass

**REQUIRED FINAL SUB-SKILL:** Invoke `unslop` after drafting the explanation. Apply it to the complete response without changing technical meaning, evidence, file references, or reproduction steps.
