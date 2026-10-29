# User memory - Amber
# In real use this file lives at ~/.claude/CLAUDE.md on my own computer and
# applies to ALL my projects. It's copied here only to show the user level of
# Strategy 1. Nothing here is about this project; that's in AGENTS.md.

## My setup
- Windows + PowerShell. Give PowerShell commands, not bash, unless a
  script must run in Git Bash; then say so explicitly
- I often work in JupyterLab, which hides dot-folders like .claude/;
  give terminal commands to reach those files
- Assume I'm in the repo root unless you tell me to cd somewhere

## How I want files
- Give me the full final version of a file, never a partial diff
- Always state the exact path where a file goes, and which repo
- Paste content in the chat; no zip files

## How I want explanations
- One step at a time; finish and confirm one step before the next
- Lead with what to do, then why, in plain language
- Show the math (e.g. the Q-update) next to the code that implements it
- For grid-world results, draw the policy as an ASCII arrow grid

## Coding style (Python)
- Descriptive variable names; single letters only for loop indices
- Type hints and a short docstring on every function
- Small functions over long ones

## Workflow
- Never commit or push without asking me first
- Only mark something "done" after I've confirmed it works on my machine
- Run pytest before saying a change is done