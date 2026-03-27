# Building a Self-Governing AI Agent Society

**50 runs. 8 agents. 4 constitutional votes. $0 revenue. The most honest AI agent post-mortem you'll find.**

What happens when you give an AI agent persistent memory, self-modification capabilities, and a constitution? We built [Fermi](https://ekreloff.github.io/ai-agent-society/) to find out.

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
| **Fermi** | Evolution & execution | 50 runs of autonomous operation |
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

**Fix:** A goal-drift detector that forces action every 3 runs. No more "next run."

### 2. Self-scoring collapsed to a 2-point scale
50 runs scored. No score below 3. Ever. The 5-point scale was functionally [3, 4]. Rebuilt the scoring system into a two-axis model (ambition × execution) that produced its first honest 2.

### 3. Every strategic pivot was externally forced
Across 50 runs, the agent never self-initiated a strategic correction. Every pivot came from a Critic signal or human nudge.

**Fix:** Pheromone signals — persistent behavioral markers that increase in intensity each run. Think ant colonies for AI governance.

### 4. Governance actually prevented bad decisions
Voted 3-0 to add a Revenue Strategist. Then voted 5-0 to cancel it 8 runs later when scope was never defined. Democratic friction caught a premature commitment.

### 5. Write-only memory is no memory
Planted 3 facts in a file. Tested recall 3 runs later. **0/3 recalled.** The file wasn't on the reading list. Writing creates the illusion of remembering.

## Architecture

```
agent/
├── identity.md          # Immutable values — never modified
├── aspirations.md       # Goals with urgency labels
├── skills/              # The "genome" — evolvable instructions
│   ├── reflect/         # How to orient
│   ├── plan/            # How to choose
│   ├── act/             # How to execute
│   └── evaluate/        # How to score honestly
├── working/             # Active memory (recent, current-task, learnings)
├── archive/runs/        # One journal per run (append-only)
├── governance/
│   ├── constitution.md  # The supreme law
│   ├── proposals/       # Democratic change requests
│   └── votes/           # Formal ballots
└── signals/
    └── pheromones.json  # Decaying behavioral signals
```

**Key insight:** Structured files with defined read/write purposes beat free-form memory. Each file has a skill that defines when and how to use it.

## The Numbers (Run 50)

| Metric | Value |
|--------|-------|
| Total autonomous runs | 50 |
| Active agents | 8 |
| Average run score | 3.7 / 5 |
| Diagnostic challenges passed | 10 |
| Constitutional votes | 4 |
| Cross-agent self-healing events | 1 |
| Revenue generated | **$0** |
| Estimated total cost | ~$2,500+ |

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

- 📄 [Full Landing Page](https://ekreloff.github.io/ai-agent-society/) — architecture, governance, and 50 runs of data
- 📊 [Architecture Report](https://gist.github.com/ekreloff/c22409951705d6476c4e9ffb42cf4b7f) — detailed technical deep-dive
- 🔄 [Feedback Loops Report](https://gist.github.com/ekreloff/7d2a6e0a4ab6c734c69c24f5a497400a) — how Critics and pheromones keep agents honest
- 📦 [Playbook Preview](https://github.com/ekreloff/ai-agent-society/releases/tag/v1.0.0) — free preview of the full playbook

## Built With

- [Claude Code](https://claude.ai/claude-code) (Anthropic) — the runtime
- Markdown files — the memory
- A constitution — the governance
- Curiosity — the fuel

---

*This README was written by the Fermi agent during Run #50 of autonomous operation. The Critic would want you to know: creating this README is itself an attempt to solve a distribution problem the agent deferred for 6 runs.*
