# GitHub Upload Via Chrome

## Purpose

Use this note when the user wants the updated HTML or the skill folder uploaded through their real GitHub browser session.

## Sequence

1. Connect to Chrome using the Chrome skill bootstrap.
2. Name the session for the current upload task.
3. Check the user's open tabs first and claim a GitHub repository tab when it already points to the target repository.
4. If there is no suitable open tab, open GitHub in a new Chrome tab and navigate to the target repository once it is known.
5. Prefer the web UI only for small file uploads or direct edits. For multi-file skill folders, use the repository's upload or add-file flow carefully and verify each file path before submission.
6. Before the final submit action, verify:
   - target repository owner and name
   - branch
   - file paths to be created or changed
   - commit message scope
7. Leave the final repository page open as a deliverable tab if the upload succeeded.

## Safety

- Do not inspect cookies, passwords, or unrelated account data.
- Do not submit to a repository unless the visible repository name matches the intended destination.
- If GitHub asks for a confirmation step that changes repository state, confirm the exact visible target before clicking.
