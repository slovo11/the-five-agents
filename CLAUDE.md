# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Agent Instructions

At the start of every session, read `agent.md` before processing any user request.
This file contains the CEO Agent's operational instructions, sub-agent registry,
memory path, and all orchestration rules.

## Project Overview

**The Five Agents** is a multi-agent content creation system. A lead agent (the "CEO") orchestrates a team of specialized sub-agents, each responsible for a different aspect of content production. The full agent roster and responsibilities will be defined as the project evolves.

## Project Structure

```
.claude/
├── agents/      # Custom sub-agent definitions for this project
├── skills/      # Reusable skills available to agents
└── commands/    # Custom slash commands for Claude Code
```

All agent logic, skill implementations, and custom commands specific to this project live under `.claude/`. These directories are currently empty and will be populated incrementally.
