# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A health and safety guide for cluster headache patients who use DMT to abort their attacks. The project is currently in the **content phase** (no code yet) and will eventually become a website.

**Target audience:** 50-something person with no drug experience and limited ability to find reliable information online. All content must be written with extreme clarity and accessibility in mind.

**Minimizing suffering**. The guide should strike a balance between (1) informing the user about the risks of taking DMT and (2) making sure the user isn't too conservative about taking DMT --a powerful tool to minimize the intense pain attacks cause.

## Current State

- `Guide MVP v1 claude.md` — reference document containing the guide content (one-page summary, oxygen protocol, DMT safety, aborting protocol, drug interactions, vape preparation, sitter requirements)
- `*.md` documents containing more detailed versions of some sections
- `README.md` — Project mission and roadmap

## Roadmap

1. (In progress:) Create separate markdown documents from sections of `Guide MVP v1 claude.md`. The separate documents should contain more illustrations and generalyl do more "hand-holding" for the user
   1. Illustrations can be generated using `nano banana pro`, available via API calls (`$GOOGLE_API_KEY` available)
2. Gather external feedback
3. Build the website, with further feedback rounds

## Review process

Use `/review <filename.md>` to launch a full review of a guide section. This runs four agents in parallel:

1. **Fact-Checker** — verifies every factual claim via web search (splits into sub-agents for long files)
2. **Straight-to-Facts Editor** — flags redundancies, unnecessary detail, and structural issues
3. **Visual Artist** — checks that illustrations match the text they accompany
4. **Median User** — role-plays the target audience to find jargon, ambiguity, and missing info

Agent definitions live in `.claude/agents/`. The review skill lives in `.claude/skills/review/`.