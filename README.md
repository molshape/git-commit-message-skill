# Git Commit Message Skill

A specialized AI skill to transform raw `git diff` logs into structured, high-quality git commit messages that follow the core principles of the Conventional Commits specification.

## 📖 Overview

Generating meaningful commit messages is often a chore, tempting developers to end up with vague messages like "fix bug" or "update files."

This project provides a strictly defined [**SKILL.md**](./SKILL.md) file designed to be used by AI Agents. It instructs the AI to analyze the logic behind the changes, determine the correct commit type, and format the output into a consistent, professional, human-readable summary that explains *why* a change was made, not just *what* was changed.

## 🚀 Quick Installation

To integrate this skill into your main project's repository, run the following command from your project's root directory:

```bash
git subtree add --prefix=.agents/skills/git-commit-message-skill https://github.com/molshape/git-commit-message-skill main --squash
```

To update the skill from its original repository in the future, run:

```bash
git subtree pull --prefix=.agents/skills/git-commit-message-skill https://github.com/molshape/git-commit-message-skill main --squash
```

## ✨ Key Features

- **Conventional Commits Integration**: Automatically categorizes changes into `feat`, `fix`, `ref`, `doc`, `test`, `ci`, `chore`, `lint`, and `revert`.
- **Logic-Driven Analysis**: Instead of simply listing modified files, the skill forces the AI to interpret the intent (e.g., "Improve validation logic" instead of "Update `validation.py`").
- **Strict Formatting**: 
    - Uses the **imperative mood** for titles and bullet points.
    - Enforces a maximum of 80 characters for titles.
    - Automatically formats code elements (functions, variables, classes, modules, configuration keys) with backticks and appropriate syntax.
- **Multilingual Support**: Automatically translates non-English comments found in the diff into the final English commit message.
- **Noise Reduction**: Filters out trivial changes like formatting-only details unless they are the primary purpose of the commit.

## 🛠 How to Use

This repository contains the definition of the skill. You can use it in several ways:

### 1. As a System Prompt
If you are building an AI-powered CLI tool, a GitHub Action, or a web application, include the content of `SKILL.md` in your system prompt to "prime" the LLM to act as a specialized Git Commit Assistant.

### 2. Manual Copy-Paste
If you are using a chat interface (like ChatGPT, Claude, or Gemini), you can copy the contents of `SKILL.md` into the chat to set the rules, then provide your `git diff` as the input.

**Example Workflow:**
1. **User Input:** `git diff --staged`
2. **AI Process:** The AI applies the rules in `SKILL.md` to analyze the diff.
3. **Output:**
   ```text
   feat(auth): implement JWT token validation

   - add `validateToken()` to check expiration
   - update `AuthMiddleware` to reject expired tokens
   - update `README.md` with new security protocols
   ```

## 📋 Requirements
To get the best results, the preferred input should be:

    git diff --staged

If no changes are staged, the following input can be used:

    git diff

## 📄 License
This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.
