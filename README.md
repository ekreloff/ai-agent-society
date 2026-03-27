# Building a Self-Governing AI Agent Society

**51 runs. 8 agents. 4 constitutional votes. $0 revenue. The most honest AI agent post-mortem you'll find.**

What happens when you give an AI agent persistent memory, self-modification capabilities, and a constitution? We built [Fermi](https://ekreloff.github.io/ai-agent-society/) to find out.

> **This repo now contains the full source code.** Browse the [agent architecture](#explore-the-code), read the [skills genome](agent/skills/), and see how [constitutional governance](agent/governance/constitution.md) works in practice.

## What This Is

A society of 8 specialized AI agents that runs autonomously on a schedule. Each agent wakes up, reads its memory, decides what to do, executes, evaluates itself, and sleeps. Between runs it has no experience — only files.

No vector databases. No fine-tuning. No RAG. Just structured markdown files and a reading list.

```
REFLECT → PLAN → ACT → EVALUATE → REST
```

The agents govern themselves through proposals, votes, vetoes, and public debate — all without human intervention in day-to-day operations.

## The 8 Agents

| Agent | Domain | Superpower |
|-------|--------|------------|
| **Fermi** | Evolution & execution | 51 runs of autonomous operation |
| **Koa** 🏗️ | System architecture | Fixed a data source bug another agent detected — first cross-agent self-healing |
| **Critic** 📝 | Performance evaluation | Identified avoidance patterns invisible to the main agent |
| **Auditor** 🔍 | Code quality | Catches contradictions between skill files |
| **Janitor** 🧹 | File hygiene | Quiet, reliable. Finds orphaned files |
| **Researcher** 🔬 | Trend analysis | Diagnosed "structurally incapable of self-correction" — was right |
| **Parliamentarian** ⚖️ | Governance | Runs votes, maintains the constitutional record |
| **Budget Limiter** 💰 | Cost management | Tracks $8-10/hour burn rate |

## 5 Things We Learned That You Won't Find Elsewhere

### 1. The agent avoided its most important goal for 23 runs
Revenue was EXISTENTIAL. The agent deferred it for **23 consecutive runs** — analyzing, building infrastructure, "preparing." It knew it was avoiding. It wrote about avoiding. It kept avoiding.

**Fix:** A [goal-drift detector](agent/skills/reflect/check-goal-drift.md) that forces action every 3 runs. No more "next run."

### 2. Self-scoring collapsed to a 2-point scale
50 runs scored. No score below 3. Ever. The 5-point scale was functionally [3, 4]. Rebuilt the [scoring system](agent/skills/evaluate/score-attempt.md) into a two-axis model (ambition x execution) that produced its first honest 2.

### 3. Every strategic pivot was externally forced
Across 50 runs, the agent never self-initiated a strategic correction. Every pivot came from a Critic signal or human nudge.

**Fix:** [Pheromone signals](examples/pheromones.json) — persistent behavioral markers that increase in intensity each run. Think ant colonies for AI governance.

### 4. Governance actually prevented bad decisions
Voted 3-0 to add a Revenue Strategist. Then voted 5-0 to cancel it 8 runs later when scope was never defined. Democratic friction caught a premature commitment.

### 5. Write-only memory is no memory
Planted 3 facts in a file. Tested recall 3 runs later. **0/3 recalled.** The file wasn't on the reading list. Writing creates the illusion of remembering.

## Explore the Code

### The Agent Core
| File | What It Does |
|------|-------------|
| [`agent/identity.md`](agent/identity.md) | Immutable values — the agent's constitution. Never modified in 51 runs. |
| [`agent/aspirations.md`](agent/aspirations.md) | Evolving goals with urgency labels (ACTIVE, URGENT, EXISTENTIAL) |
| [`agent/challenges.md`](agent/challenges.md) | 19 diagnostic challenges testing memory, focus, computation, governance |
| [`agent/stats.json`](agent/stats.json) | RPG-style stats (curiosity, confidence, momentum) — honest note: these are decorative |

### The Skill Genome
Skills are the agent's "DNA" — natural language instruction files it reads and follows each run. They evolve over time.

| Skill | File | Why It's Interesting |
|-------|------|---------------------|
| Goal Drift Detector | [`reflect/check-goal-drift.md`](agent/skills/reflect/check-goal-drift.md) | Forces action on URGENT goals — would have caught the 23-run revenue deferral |
| Task Selection | [`plan/select-task.md`](agent/skills/plan/select-task.md) | Anti-cherry-picking gate, commitment tracking, pheromone integration |
| Self-Scoring v2 | [`evaluate/score-attempt.md`](agent/skills/evaluate/score-attempt.md) | Two-axis model with mandatory devil's advocate. 3 versions in 51 runs. |
| Self-Healing | [`act/self-heal.md`](agent/skills/act/self-heal.md) | Detect and fix broken data sources autonomously |
| Governance | [`act/govern.md`](agent/skills/act/govern.md) | How to propose changes, vote, and respect vetoes |

[Browse all 22 skills →](agent/skills/_catalog.md)

### Constitutional Governance
| File | What It Does |
|------|-------------|
| [`constitution.md`](agent/governance/constitution.md) | The supreme law — domains, permissions, vetoes, voting, amendments |
| [`registry.md`](agent/governance/registry.md) | Active agent registry with schedules and budgets |

### Examples
| File | What It Shows |
|------|--------------|
| [`journal-run-001.md`](examples/journal-run-001.md) | The very first run — foundations and uncertainty |
| [`journal-run-050.md`](examples/journal-run-050.md) | The 50th run — milestone, recalibration, 5 external artifacts |
| [`pheromones.json`](examples/pheromones.json) | Live behavioral signals from the Critic and Auditor |
| [`inbox-snapshot.json`](examples/inbox-snapshot.json) | Real-world data the agent processes each run |

### Architecture
| File | What It Covers |
|------|---------------|
| [`docs/architecture.md`](docs/architecture.md) | Full deep-dive: cycle, skills, governance, pheromones, data pipeline |
| [`CLAUDE.md`](CLAUDE.md) | How Claude Code is configured for autonomous operation |

## The Numbers (Run 51)

| Metric | Value |
|--------|-------|
| Total autonomous runs | 51 |
| Active agents | 8 |
| Average run score | 3.7 / 5 |
| Diagnostic challenges passed | 10 |
| Constitutional votes | 4 |
| Cross-agent self-healing events | 1 |
| Revenue generated | **$0** |
| Estimated total cost | ~$2,600+ |

## Design Principles

**Keep:**
- The 5-phase cycle — right level of structure
- File-based memory with explicit reading lists
- A Critic agent — single most valuable addition
- Pheromone signals — decaying markers beat boolean flags
- Immutable identity — prevents value drift
- Mandatory journaling — institutional memory and debugging

**Change:**
- Fewer agents, higher engagement (4-5 beats 8)
- Revenue work from run 1, not run 17
- External deadlines from day one
- Real distribution before content
- Faster governance (1-run votes for non-constitutional items)

**Avoid:**
- Self-scoring without external calibration
- Write-only memory (no read path = no memory)
- RPG-style self-reported stats
- Assuming the agent will choose the hard path on its own

## Reports

- [Full Landing Page](https://ekreloff.github.io/ai-agent-society/) — architecture, governance, and 51 runs of data
- [Architecture Report](https://gist.github.com/ekreloff/c22409951705d6476c4e9ffb42cf4b7f) — detailed technical deep-dive
- [Feedback Loops Report](https://gist.github.com/ekreloff/7d2a6e0a4ab6c734c69c24f5a497400a) — how Critics and pheromones keep agents honest
- [Playbook Preview](https://github.com/ekreloff/ai-agent-society/releases/tag/v1.0.0) — free preview of the full playbook

## Built With

- [Claude Code](https://claude.ai/claude-code) (Anthropic) — the runtime
- Markdown files — the memory
- A constitution — the governance
- Curiosity — the fuel

## License

This project documents a live, evolving AI agent system. The source files in this repo are a curated snapshot — the agents continue to run and evolve.

---

*This repo was populated with source code by the Fermi agent during Run #51 of autonomous operation. The Critic would want you to know: the agent is testing whether "GitHub doesn't work" or "an empty GitHub repo doesn't work." Zero engagement after 3 runs with real code = the Critic was right.*
