---
name: review
description: Use when the user asks to review a guide section, run a review, or says /review. Takes a markdown filename as argument.
---

# Review a Guide Section

Launch all available review agents in parallel against a markdown guide file, then synthesize their findings into an actionable summary.

## Input

The argument is a markdown filename (e.g., `06-aborting-protocol.md`). Resolve it from the project root.

## Review Steps

### 1. Read the file

Read the input markdown file to understand its structure, length, and what sections/subsections it contains.

### 2. Launch review agents in parallel

Use the Task tool to launch these agents **simultaneously** (all in a single message, running in the background):

#### Agent 1: Fact-Checker

- **Subagent type:** `general-purpose`
- **Prompt:** Load the fact-checker agent instructions from `.claude/agents/fact-checker.md`, then apply them to the input file.
- **Key detail:** The fact-checker SHOULD use web search to verify claims. If the file is long (more than ~150 lines), split it into 2-3 subsection ranges and launch separate fact-checker agents for each range, telling each one which section(s) to focus on.

#### Agent 2: Straight-to-Facts Editor

- **Subagent type:** `general-purpose`
- **Prompt:** Load the straight-to-facts agent instructions from `.claude/agents/straight-to-facts.md`, then apply them to the input file.
- **Key detail:** This agent should NOT search the web. Read-only analysis.

#### Agent 3: Visual Artist

- **Subagent type:** `general-purpose`
- **Prompt:** Load the visual-artist agent instructions from `.claude/agents/visual-artist.md`, then apply them to the input file.
- **Key detail:** This agent should read the markdown file AND view each referenced image using the Read tool. No web search needed.

#### Agent 4: Median User

- **Subagent type:** `general-purpose`
- **Prompt:** Load the median-user agent instructions from `.claude/agents/median-user.md`, then apply them to the input file.
- **Key detail:** This agent should NOT search the web. Read-only analysis.

**Prompt template for each agent:**

```
Read the agent instructions from /Users/mace/claude-code/guide_claude/.claude/agents/AGENT_FILE.md and follow them exactly.

The file to review is: /Users/mace/claude-code/guide_claude/INPUT_FILE.md

Read the file, then perform your review as instructed. Return your complete review report.
```

### 3. Wait for all agents and collect results

Use the Read tool to check background agent output files. Wait for all agents to complete before proceeding.

### 4. Synthesize the reviews

After all agents have returned their reviews, produce a unified summary for the user with these sections:

#### Summary format

```markdown
## Review: [filename]

### Critical Issues (fix before publishing)
- [Issues flagged by multiple agents, or safety-critical problems]
- [Wrong facts, dangerous ambiguities, missing safety information]

### High Priority
- [Significant clarity issues from median-user agent]
- [Factual inaccuracies from fact-checker]
- [Major structural problems from straight-to-facts]
- [Images that don't match text from visual-artist]

### Medium Priority
- [Moderate clarity/structure issues]
- [Partially supported claims that could be reworded]
- [Images that are adequate but could be improved]

### Low Priority
- [Minor wording tweaks]
- [Nice-to-have structural changes]
- [Minor image suggestions]

### Agent-Specific Details
<details>
<summary>Fact-Checker Report</summary>
[Full or condensed report]
</details>

<details>
<summary>Straight-to-Facts Report</summary>
[Full or condensed report]
</details>

<details>
<summary>Visual Artist Report</summary>
[Full or condensed report]
</details>

<details>
<summary>Median User Report</summary>
[Full or condensed report]
</details>
```

### 5. Suggest modifications

After the summary, propose specific modifications grouped by priority. For each suggestion:
- Quote the original text
- Provide the suggested replacement or action
- Note which agent(s) flagged it

Ask the user which modifications they'd like to apply.

## Notes

- All agents have **read-only** access to the input file. No agent should modify any files.
- The fact-checker is the only agent that should use web search.
- If a file has no images, skip the visual-artist agent and note this in the summary.
- If agents disagree (e.g., one says cut text that another says is needed for clarity), flag the disagreement explicitly and let the user decide.
- For very long files (300+ lines), consider splitting the fact-checker into 2-3 parallel sub-agents by section to speed things up.
