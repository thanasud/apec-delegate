# Apec Delegate

Apec Delegate is a Codex skill for identifying bounded work that can be delegated to Antigravity Gemini Flash through the `agy` CLI. It keeps Codex responsible for task scope, review, and integration, and defines fallback behavior for unavailable tools and failed delegation.

## What It Does

- Evaluates whether a task is suitable for delegation and whether delegation overhead is worthwhile.
- Checks that the selected model appears in `agy models` before invoking it.
- Sends only the context, constraints, and acceptance criteria needed for the delegated task.
- Requires Codex to review delegated results before using or integrating them.
- Defines retry limits and fallback behavior for transient failures, quota exhaustion, and an unavailable CLI.

## Requirements

- OpenAI Codex with support for personal skills.
- The Antigravity `agy` CLI installed and configured when using Gemini delegation.
- At least one suitable Gemini model available in `agy models`.

The skill checks the exact model identifier before dispatch. Model availability can vary by environment.

## Installation

Clone this repository, then copy `SKILL.md` into your personal Codex skills directory:

```sh
git clone https://github.com/<owner>/apec-delegate.git
mkdir -p ~/.codex/skills/apec-delegate
cp apec-delegate/SKILL.md ~/.codex/skills/apec-delegate/SKILL.md
```

Replace `<owner>` with the GitHub account or organization that owns the repository. Start a new Codex session after installation.

## Usage

Codex considers this workflow when a request has a useful, bounded subtask to delegate. Tiny or indivisible tasks stay with the primary model. Before each delegation, the skill requires checking the exact model name with:

```sh
agy models
```

The skill then invokes the selected model in JSON print mode and reviews the returned status, response, and any changed files. If delegation cannot be used, Codex handles the work directly when feasible. GPT-6 Luna is an alternate worker only when the skill's fallback conditions apply and a supported Codex agent is available.

## Repository Contents

- `SKILL.md` — skill metadata and workflow instructions.
- `README.md` — project overview and installation guide.
