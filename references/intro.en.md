# GitHub Technical Weekly Report

This skill generates, maintains, and publishes a standalone GitHub technical weekly report HTML page. It is intended for leaderboard-style reports covering weekly trending repositories, monthly trending repositories, and a surging approximation, with no local build pipeline required.

## Capabilities

- Create or update a restrained technical-editor leaderboard page.
- Maintain language switching for Simplified Chinese, Traditional Chinese, and English.
- Localize page titles, section copy, leaderboard summaries, modal project briefs, problem statements, and usage guidance.
- Preserve modal accessibility: close button, overlay close, Esc close, and keyboard focus behavior.
- Verify that the HTML file exists, inline scripts parse, language buttons exist, ranks are sequential, and project briefs use the localized summary path.
- Publish the report or this skill to GitHub when requested.

## Usage

Ask Codex to use `$github-technical-weekly-report` and provide the target HTML file, or ask it to generate a new weekly report. After edits, run the local verification script. For GitHub publishing, confirm the target repository, branch, and file paths before committing or uploading through the browser.
