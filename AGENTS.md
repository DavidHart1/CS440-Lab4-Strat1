# Lab 4 - Vacuum Robot with Reinforcement Learning (CS 440)

## Project overview
Part of our aima-python fork. We are preparing a vacuum-robot agent that
will learn with Q-learning in a later lab. Current work is configuration
only: do not implement the environment or Q-learning in this lab.

## Environment
- 4x4 grid, cells as (row, col); (0,0) top-left is the start
- Wall "X" at (1,1): cannot be entered
- Terminal cells: -1 at (3,1), +10 at (3,3); all other cells 0
- Actions: Up, Down, Left, Right (our assumption, following AIMA's grid world)
- Moving into the wall or off the grid leaves the robot in place (our assumption)
- There are 15 reachable states
- The transition model T and reward function R are UNKNOWN to the agent,
  so value/policy iteration (AIMA ch. 17) cannot be used directly; the agent
  must learn from experience (Q-learning, AIMA ch. 22)

## Coding standards
- Python 3; reuse aima-python's mdp.py and reinforcement_learning.py classes instead of rewriting them
- This repository root is the lab4 configuration directory. Keep changes inside
  this repository; do not modify the parent aima-python source.
- Docstrings and type hints on every function and class
- Tests go in lab4/tests/ and use pytest

## Strategy 1: Memory
- Readings: AIMA ch. 12 (uncertainty), 17 (MDPs), 22 (RL)
- Shared project memory lives in this file and is imported by CLAUDE.md.
- Detailed notes live in .claude/context/ and are loaded by the
  UserPromptSubmit hook when prompt keywords match; do not copy them here.
- Read only the notes and source definitions needed for the assigned task
