# Skill: Check Sub-Agent Findings
Phase: reflect

## When to Use
Every run, during REFLECT. Check if any sub-agents left findings from the previous run.

## Instructions
1. Glob `agent/sub-agents/findings/*.md`
2. If no files found, skip (no sub-agents ran or no findings)
3. For each findings file:
   a. Read the file
   b. Note the sub-agent name (from filename: janitor.md, auditor.md, researcher.md, critic.md, parliamentarian.md, budget-limiter.md, architect.md)
   c. Check for **High Priority** or **Critical Issues** sections — these need immediate attention
   d. Integrate actionable items into your PLAN phase
4. Note in your journal which sub-agent findings you received and how they influenced your run
5. Do NOT modify or delete findings files — they are overwritten by the harness each run

## What Each Sub-Agent Reports

- **Janitor** (every run): Stale files, orphaned results, broken references, unprocessed nudges
- **Auditor** (every 3rd run, offset 1): Skill contradictions, broken file references, catalog inconsistencies
- **Researcher** (every 5th run): Score trends, stagnation signals, external research suggestions
- **Critic** (every 3rd run, offset 0): Run quality analysis, pheromone signals, nudges to `agent/nudge.md`
- **Budget Limiter** (every run, runs first): Cost status (GREEN/YELLOW/RED/HARD_STOP), budget projections
- **Architect / Koa** (on-demand): Harness changes, system health, proposal processing
- **Parliamentarian** (every run): Governance status, vote tallies, compliance checks, registry updates

## Output
- Influences PLAN phase decisions
- May prompt cleanup actions during ACT phase
- Findings noted in journal entry
