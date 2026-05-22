---
name: github-technical-weekly-report
description: Build, update, and publish a GitHub technical weekly report as a standalone single-file HTML page. Add zh-Hans, zh-Hant, and English language switching with inline CSS and JS, verify the updated file locally, and publish the report or the skill itself to a GitHub repository through the user's Chrome session. Use when Codex needs to maintain a GitHub weekly leaderboard page, internationalize a standalone report, package the workflow as a reusable skill, or upload the result through browser automation.
---

# GitHub Technical Weekly Report

## Overview

Implement and maintain a GitHub technical weekly report as a standalone HTML page without introducing a build step, then package the workflow as a reusable skill and publish through Chrome when the user wants the result uploaded to GitHub.

## Workflow

1. Identify the target weekly-report HTML file.
2. Keep the file single-page and self-contained: inline CSS, inline JS, no framework or bundler assumptions.
3. Add exactly three language buttons in the UI: `zh-Hans`, `zh-Hant`, and `EN`.
4. Add a client-side locale state and rerender logic rather than duplicating pages.
5. Translate structural UI first: title, subtitle, labels, section headings, disclosure text, modal labels, footer notices, and button text.
6. Preserve existing interactions. If the page already has dialogs, keyboard handling, or fold or unfold controls, do not regress them while adding i18n.
7. Re-run local verification after patching. At minimum confirm the file exists, the inline script parses, and the expected language buttons are present.
8. If the user also wants the workflow reusable, create or update this skill in the workspace or requested skill folder.
9. If the user wants the result uploaded to GitHub, use Chrome browser automation against the user's signed-in browser session rather than a synthetic fallback.

## HTML Editing Rules

- Prefer a small overlay patch over a full rewrite when the page already works.
- Add element ids or stable hooks only where needed for translation updates.
- Keep `document.title` stable if the user explicitly requires a fixed browser title; otherwise it may follow the active locale.
- Store locale strings in a compact object keyed by locale.
- Reuse existing render functions if possible. If not, add a second script layer that overrides or wraps the existing rendering safely.
- Preserve mobile layout. Language buttons should wrap cleanly and never force horizontal overflow.

## Locale Pattern

- Use `zhHans`, `zhHant`, and `en` as locale keys.
- Keep one active locale state object.
- Update `document.documentElement.lang` on switch.
- Update `aria-label`, modal headings, disclosure text, and other assistive strings with the same locale change.
- If modal content is open during a language switch, rerender the modal content in place instead of forcing the user to reopen it.

## Verification

- Prefer a local verification script in the repo when this becomes recurring.
- Check for:
  - the target file exists
  - the three locale buttons exist
  - inline JS parses successfully
  - existing keyboard handlers such as `Escape` still exist
  - required headings and sections still exist

## GitHub Upload Through Chrome

- Use Chrome when the user explicitly wants browser-based GitHub upload or when the repository destination depends on their logged-in session.
- Follow the Chrome skill bootstrap and connection checks before acting.
- Prefer the user's already-open GitHub tab if it exists; claim it instead of opening redundant tabs.
- If the repository is not obvious from local context, discover it from the user's open tabs or current browser context before uploading.
- Upload or edit only the intended files. Do not create unrelated commits or repository content.
- Keep the final GitHub tab open only if it is the deliverable page the user may want to inspect after the turn.

## References

- Read [references/github-upload-via-chrome.md](references/github-upload-via-chrome.md) when the task includes publishing through GitHub in the browser.
