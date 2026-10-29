# CS440 Lab 4 - Strategy 1: Persistent Memory (Write)

This repository sets up an agent's memory for a vacuum robot that will later
learn with Q-learning in a 4x4 grid world. It uses context engineering
**Strategy 1 (Write)**: the agent's knowledge is written into files at
different levels, so it never has to be re-explained, and detailed notes are
loaded only when needed. No Q-learning code yet: this lab is setup only.

## Structure

```
CLAUDE.md                     Entry point Claude Code reads every session; imports AGENTS.md
AGENTS.md                     PROJECT memory: grid, rewards, unknown T and R, coding standards
user-memory/CLAUDE.md         USER memory example: personal preferences (really lives in ~/.claude/)
.claude/settings.json         Registers the UserPromptSubmit hook
.claude/context/              DETAILED context, loaded on demand by the hook
    environment.md            Grid layout, cells, actions, what the agent doesn't know
    mdp.md                    AIMA ch. 17: MDPs, Bellman, why value iteration doesn't apply
    qlearning.md              AIMA ch. 22: Q-update, exploration, aima-python QLearningAgent
scripts/context-switcher.sh   Hook script: picks context files by prompt keywords
.gitattributes                Keeps the .sh file on LF line endings (Windows-safe)
```

## The three memory levels

| Level | File | Loaded | Why |
| --- | --- | --- | --- |
| Project | CLAUDE.md -> AGENTS.md | Every session | Facts every task needs; shared through git |
| User | ~/.claude/CLAUDE.md (example in user-memory/) | Every session, all projects | Personal style, not project facts |
| Detailed context | .claude/context/*.md | Only when the prompt needs it | Keeps the context window small |

## Design decisions

- **AGENTS.md + CLAUDE.md:** AGENTS.md is an open standard many coding agents
  read, so the project memory isn't tied to one tool. CLAUDE.md imports it with
  `@AGENTS.md`, the import syntax from the lecture.
- **Short always-on memory:** everything in CLAUDE.md/AGENTS.md costs tokens on
  every turn, so long notes live in .claude/context/ instead. This prevents
  context overload and context confusion.
- **The hook lives in settings.json, the logic lives in the script.** The script
  matches keywords (e.g. "Q-learning" loads qlearning.md).
- **Idempotent injection:** `grep -qxF` checks whether a file was already loaded
  this session, so the context never fills with duplicates.
- **Keywords instead of git branches:** the lecture's example also switches by
  branch name; this lab has no topic branches, so prompt keywords are the useful signal.

## How to try it

1. Open a terminal in this repo root and run `claude`.
2. Ask: "Explain the Q-learning update for our grid." The hook loads qlearning.md.
3. Ask again in the same session: the file isn't loaded twice.

Test the script on its own in Git Bash:

```bash
rm -f /tmp/lab4-context-demo.txt
echo '{"session_id":"demo","prompt":"explain q-learning"}' | bash scripts/context-switcher.sh
echo '{"session_id":"demo","prompt":"explain q-learning"}' | bash scripts/context-switcher.sh
```

The first run prints qlearning.md; the second prints nothing.

## References

- Lecture: Agentic AI - Context Engineering, Strategy 1 (pp. 21-28)
- Russell and Norvig, AIMA ch. 12, 17, 22
- aima-python: mdp.py, reinforcement_learning.py