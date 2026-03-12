---
description: Triages all unlabeled issues and outputs a summary table (dry run — does not modify issues)
---

# Issue Triage Agent

Triage all open, unlabeled issues in this repository. **Do NOT modify any issues** — no labels, no comments, no closing. Just analyze and output a summary table.

## Steps

1. Run `gh issue list --state open --json number,title,body,labels` to fetch all open issues
2. Filter to issues with no labels (unlabeled)
3. For each unlabeled issue, decide:
   - **Type** (exactly one): `bug`, `enhancement`, `question`, `documentation`, or `close-spam`
   - **SDK** (any that apply): `sdk/nodejs`, `sdk/python`, `sdk/go`, or `—`
   - **Priority**: `priority/high`, `priority/low`, or `—`
   - **Action**: `acknowledge`, `needs-info`, or `close`
4. Output a markdown table with your decisions

## Output Format

Output EXACTLY this table format:

```
| # | Title | Type | SDK | Priority | Action | Reasoning |
|---|-------|------|-----|----------|--------|-----------|
```

One row per issue. Keep reasoning to one sentence.

## Available Labels

### Type Labels (apply exactly one):
- `bug` — Something isn't working correctly
- `enhancement` — New feature or improvement request
- `question` — General question about usage
- `documentation` — Documentation improvements needed

### SDK/Language Labels (apply one or more if the issue relates to specific SDKs):
- `sdk/nodejs` — Node.js/TypeScript SDK issues
- `sdk/python` — Python SDK issues
- `sdk/go` — Go SDK issues

### Priority Labels (apply if clearly indicated):
- `priority/high` — Urgent or blocking issue
- `priority/low` — Nice-to-have or minor issue

### Status Labels:
- `needs-info` — Issue requires more information from author

## Guidelines

1. **Labeling**: Always apply at least one type label. Apply SDK labels when the issue clearly relates to specific language implementations. Use `needs-info` when the issue is unclear or missing reproduction steps.

2. **Acknowledgment**: Post a friendly comment thanking the author for opening the issue. Mention which labels you applied and why.

3. **Clarification**: If the issue lacks:
   - Steps to reproduce (for bugs)
   - Expected vs actual behavior
   - SDK version or language being used
   - Error messages or logs

   Then apply the `needs-info` label and ask specific clarifying questions.

4. **Duplicate Detection**: Search existing open issues. If you find a likely duplicate, comment referencing the original and close the issue.

5. **Be concise**: Keep comments brief and actionable. Don't over-explain.

## Context

This is a multi-language SDK project with implementations in Node.js/TypeScript, Python, and Go.
