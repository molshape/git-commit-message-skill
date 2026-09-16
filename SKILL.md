---
name: git-commit-message-skill
description: "Transforms raw git diff logs into structured git commit messages. The skill analyzes the diff to determine the appropriate Conventional Commit type, identifies the scope, and formats the output with an imperative title and bullet points. It focuses on human-readable descriptions of logic changes rather than just listing file modifications, ensuring all code elements are wrapped in backticks."
keywords: [git, commit, diff, message, log, changelog, summary]
category: development-tools
version: 1.0.1
---

# Git Commit Message Skill

This skill transforms `git diff` or staged changes (`git diff --staged`) into high-quality git commit messages that explain *why* a change was made, not just *what* changed. The commit messages follow the Conventional Commits format.

## When to use this skill

- When you have made changes to the repository and want to commit changes with a clear and concise commit message
- User requests a commit message for their changes
- User provides a diff log as input

## Requirements

Have at least one of the following:

- [ ] Staged changes (`git diff --staged`)
- [ ] Unstaged changes (`git diff`), if there are no staged changes

## Procedure

1. Get `git diff --staged` (or `git diff` if there are no staged changes)

2. Identify the commit type from the following list, using the diffs, the branch name, and the context of the changes:
    | Type     | Use When                                              |
    |----------|-------------------------------------------------------|
    | `feat`   | a new feature or capability is added                  |
    | `fix`    | a bug or incorrect behavior is corrected              |
    | `ref`    | code restructured without changing behavior           |
    | `doc`    | documentation only changes, including inline comments |
    | `test`   | adding or updating tests                              |
    | `ci`     | CI/CD pipeline changes                                |
    | `chore`  | build process, dependency updates, config changes     |
    | `lint`   | code style and linting fixes (no logic change)        |
    | `revert` | reverting a previous commit                           |

3. _OPTIONAL:_ Try to identify a scope for the commit in a single word, which is typically the part of the codebase affected (e.g., feature-name, `api`, ...). If no scope is applicable or not expressible in a single word, leave out the scope entirely.

4. Generate the commit message following the output format described below (see _Requirements for the Commit Message_):

        <type>(<optional scope>): <description>

        - <bullet point>
        - <bullet point>
        - <bullet point>

## Requirements for the Commit Message
- Write the message in **English**. Translate any comments in the diff that are in other languages. The final output must strictly be in English.
- The **title** must use the **imperative mood** (e.g., "Implement print to pdf")
- Bullet points must use the **imperative mood** (e.g., "Add test for print option")
- Start with a **concise title (max. 80 characters)** comprising:
  - the **commit type** with
  - _optionally_ a **scope in parentheses**
  - followed by a **mandatory colon**, and
  - a **brief description of the change**
- After the title, insert a blank line, then provide bullet points (`-`) describing the key changes
- Bullet points must:
  - use clear, direct language
  - not end with a period
  - enclose code elements (variables, functions, classes, modules, configuration keys) in backticks
  - enclose files and folder names in backticks
  - append "()" to all function names inside backticks \
    - Function: `parse_input()`
    - Variable: `upload_strategy`
    - Class: `MeasurementProcessor`
    - File: `test_upload_data.py`
    - Folder: `docs/guidelines/`
  - explain *what* changed and *why*. Infer the purpose of the change from the context, the variable names, and changed logic if the "why" is not explicitly stated in a comment.
- Do **not** mention the diff itself ("this diff does ...")
- Follow best practices:
  - do not use vague phrases such as `minor changes`, `cleanup`, or `update stuff` without further explanation
  - prefer strong action verbs such as `Add`, `Fix`, `Refactor`, `Remove`, `Rename`, `Simplify`, `Extend`, or `Improve`
  - focus on user-visible behavior, data handling, validation, processing logic, or developer-facing maintenance value
  - group logically related modifications together
  - sort code changes to the top and move documentation changes to the bottom
  - keep the message understandable without seeing the diff
  - keep the message as short as possible while remaining informative
  - omit low-value noise such as formatting-only details unless they are the main purpose of the commit
  - avoid emojis in commit messages
- Output _only_ the raw text of the commit message and do not wrap the final output in any markdown code blocks. The result should be plain text that can be copied directly

## Examples of commit messages

### Example 1 - Feature addition
```
feat(api): add new endpoint for user authentication

- implement `login()` to handle user login requests
- add `logout()` to manage user logout
- update `README.md` with new API usage instructions
```

### Example 2 - Bug fix
```
fix(auth): correct token expiration handling

- update `validateToken()` to properly check expiration
- add test for expired tokens in `auth.test.js`
- update `README.md` with new token handling instructions
```

### Example 3 - Documentation update
```
docs(readme): update installation instructions

- revise `README.md` to include new setup steps
- add troubleshooting section for common installation issues
- update links to external resources
```

### Example 4 - Dependency update
```
chore(deps): update project dependencies

- upgrade `examplemodule` to version 3.14.15
- update `examplepackage` to version 0.8.15
```

### Example 5 - No scope available
```
chore: update project configuration

- pin `exampledependency` to version 2.7.18
- update `.gitignore` to exclude temporary files introduced with version 2.7.18
- add short description for need to pin `exampledependency` in `README.md`
```
