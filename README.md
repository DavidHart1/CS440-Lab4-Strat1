# AIMA Lab 4 - Strategy 1: Memory

Configuration-only preparation for the CS 440 vacuum-robot project using
aima-python. This repository demonstrates persistent project memory and
keyword-triggered context loading. It does not implement the environment or
Q-learning.

## Structure

This checkout is the lab4 configuration directory. Launch Claude Code from
the repository root. If used inside the team's aima-python fork, place this
directory at `lab4/` and launch Claude Code there.

```text
.
|-- AGENTS.md
|-- CLAUDE.md
|-- README.md
|-- .gitattributes
|-- .claude/
|   |-- settings.json
|   `-- context/
|       |-- environment.md
|       |-- mdp.md
|       `-- qlearning.md
`-- scripts/
    `-- context-switcher.sh
```

## How memory works

- [AGENTS.md](AGENTS.md) holds shared project facts, scope, and coding standards.
- [CLAUDE.md](CLAUDE.md) imports that memory using Claude Code's `@` syntax.
- [settings.json](.claude/settings.json) registers a `UserPromptSubmit` hook
  that runs [context-switcher.sh](scripts/context-switcher.sh) with Bash.
- The hook prints matching topic notes into the conversation and records loaded
  filenames in a temporary, session-specific file. Repeated prompts in the same
  session do not inject the same note again. A new session loads notes afresh.
- [.gitattributes](.gitattributes) keeps shell scripts on LF line endings.

| Prompt keywords (case-insensitive) | Memory loaded |
| --- | --- |
| grid, wall, cell, reward, terminal, environment | [Environment](.claude/context/environment.md) |
| mdp, bellman, value iteration, policy iteration, transition | [MDPs](.claude/context/mdp.md) |
| q-learning, qlearning, q learning, q-value, epsilon, explor, reinforcement | [Q-learning](.claude/context/qlearning.md) |

A prompt can match multiple topics. Other assistants must use their own
instruction-loading mechanism; the hook is specific to Claude Code.

## Project constraints

The robot starts at `(0,0)` on a 4x4 grid. Cell `(1,1)` is a wall; terminal
rewards are -1 at `(3,1)` and +10 at `(3,3)`. Other cells have reward 0.
The learner does not know the transition model or reward function and will
learn from experience in a later lab. See [shared memory](AGENTS.md) for the
full constraints and [topic notes](.claude/context/environment.md) for details.

## Validation

Requires Claude Code and Bash (for example, Git Bash on Windows). The hook uses
standard shell utilities: `cat`, `sed`, `touch`, and `grep`.

1. Launch Claude Code from this directory and confirm it loads the shared memory.
2. In a fresh session, submit "Explain Q-learning". Confirm that the Q-learning
   notes appear in the hook context.
3. Repeat the prompt in the same session. Confirm the notes are not injected again.
4. Submit "Describe the grid", then "Explain Bellman". Confirm that the
   environment and MDP notes load independently.
5. Start a new session and repeat the Q-learning prompt. Confirm the notes load again.

Shell-level checks can validate routing and deduplication, but do not prove
native Claude Code discovery or context injection.
