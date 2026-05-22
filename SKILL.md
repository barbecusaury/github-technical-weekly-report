---
name: github-technical-weekly-report
description: Use when Codex needs to create, update, internationalize, verify, package, or publish a standalone GitHub technical weekly report HTML page, especially a leaderboard with zh-Hans, zh-Hant, and English UI, localized repository summaries, accessible modal details, and GitHub browser upload requirements.
---

# GitHub Technical Weekly Report

## Overview

Implement and maintain a GitHub technical weekly report as a standalone HTML page without introducing a build step. Keep leaderboard content, modal details, and skill documentation consistent across zh-Hans, zh-Hant, and English.

## Workflow

1. Identify the target weekly-report HTML file.
2. Keep the file single-page and self-contained: inline CSS, inline JS, no framework or bundler assumptions.
3. Add exactly three language buttons in the UI: `zh-Hans`, `zh-Hant`, and `EN`.
4. Add a client-side locale state and rerender logic rather than duplicating pages.
5. Translate structural UI first: title, subtitle, labels, section headings, disclosure text, modal labels, footer notices, and button text.
6. Localize repository-facing copy next: row summaries, modal project introductions, caution text, and fallback-source notes. Do not leave Chinese locales showing English project briefs unless the source text is a proper noun, command, or product name.
7. Preserve existing interactions. If the page already has dialogs, keyboard handling, or fold or unfold controls, do not regress them while adding i18n.
8. Re-run local verification after patching. At minimum confirm the file exists, the inline script parses, the expected language buttons are present, and modal project introductions use the localized summary path.
9. If the user also wants the workflow reusable, create or update this skill in the workspace or requested skill folder.
10. If the user wants the result uploaded to GitHub, use Chrome browser automation against the user's signed-in browser session when available; if the web editor is blocked but a Git remote is available, use Git and verify the remote page afterward.

## HTML Editing Rules

- Prefer a small overlay patch over a full rewrite when the page already works.
- Add element ids or stable hooks only where needed for translation updates.
- Keep `document.title` stable if the user explicitly requires a fixed browser title; otherwise it may follow the active locale.
- Store locale strings in a compact object keyed by locale.
- Store repository-specific localized summaries in a map keyed by canonical `owner/repo` so the list and modal can share the same copy.
- Reuse existing render functions if possible. If not, add a second script layer that overrides or wraps the existing rendering safely.
- Preserve mobile layout. Language buttons should wrap cleanly and never force horizontal overflow.

## Locale Pattern

- Use `zhHans`, `zhHant`, and `en` as locale keys.
- Keep one active locale state object.
- Update `document.documentElement.lang` on switch.
- Update `aria-label`, modal headings, disclosure text, and other assistive strings with the same locale change.
- If modal content is open during a language switch, rerender the modal content in place instead of forcing the user to reopen it.
- Route modal project introductions through a `localizedSummary(entry)`-style helper. Avoid `entry.summary` fallbacks for zh-Hans or zh-Hant unless no translation exists and the limitation is explicit.

## Verification

- Prefer a local verification script in the repo when this becomes recurring.
- Check for:
  - the target file exists
  - the three locale buttons exist
  - inline JS parses successfully
  - existing keyboard handlers such as `Escape` still exist
  - required headings and sections still exist
  - list summaries and modal project introductions are localized in zh-Hans and zh-Hant

## GitHub Upload Through Chrome

- Use Chrome when the user explicitly wants browser-based GitHub upload or when the repository destination depends on their logged-in session.
- Follow the Chrome skill bootstrap and connection checks before acting.
- Prefer the user's already-open GitHub tab if it exists; claim it instead of opening redundant tabs.
- If the repository is not obvious from local context, discover it from the user's open tabs or current browser context before uploading.
- Upload or edit only the intended files. Do not create unrelated commits or repository content.
- Keep the final GitHub tab open only if it is the deliverable page the user may want to inspect after the turn.

## References

- Read [references/github-upload-via-chrome.md](references/github-upload-via-chrome.md) when the task includes publishing through GitHub in the browser.
- Read [references/intro.zh-CN.md](references/intro.zh-CN.md), [references/intro.zh-Hant.md](references/intro.zh-Hant.md), or [references/intro.en.md](references/intro.en.md) when the user asks for a human-facing explanation of this skill.
