# Claude Code entry point

@AGENTS.md

Launch Claude Code from this repository root (the lab4 configuration directory)
so it discovers .claude/settings.json. Shared project memory lives in AGENTS.md;
keep it there rather than duplicating it in this file.

The UserPromptSubmit hook loads relevant notes from .claude/context/ once per
session. This repository contains only Strategy 1: Memory; environment and
Q-learning implementation belong to a later lab.
