# Architecture Deep-Dive

How Fermi actually works — from cold boot to journal entry.

## The Core Problem

An LLM has no memory between conversations. Every invocation is a blank slate. Fermi solves this with **file-based persistent memory** — structured markdown and JSON files that the agent reads at the start of each run and writes at the end.

No vector databases. No RAG pipeline. No fine-tuning. Just files with clear purposes and skills that define how to use them.

## The 5-Phase Cycle

Every run follows the same structure:

```
REFLECT → PLAN → ACT → EVALUATE → REST
```

### REFLECT
The agent reads its recent history, checks real-world data (weather, markets, system metrics), processes messages from other agents, and orients itself. This is where continuity happens — the agent reconstructs its context from files.

Key skills: `review-last-run.md`, `check-inbox.md`, `check-goal-drift.md`, `check-sub-agent-findings.md`

### PLAN
The agent decides ONE task for this run. Not two. The `select-task.md` skill enforces:
- **Commitment check**: What did you promise last run? If pivoting, justify it.
- **Signal integration**: Read pheromone signals from other agents. High-intensity signals must influence the choice.
- **Anti-avoidance gate**: If recent tasks were all easy, must pick something hard or justify why not.

### ACT
Execute the plan. This is where real work happens — writing code, calling APIs, publishing content, modifying skill files. The agent has full tool access (Bash, WebSearch, WebFetch) and can spawn sub-tasks.

### EVALUATE
Score the run using a two-axis model:
- **Ambition axis** (1-3): How hard was the task?
- **Execution axis** (1-3): How well was it done?
- Composite via matrix lookup (not subjective judgment)
- Mandatory devil's advocate before finalizing

### REST
Write a journal entry (mandatory), consolidate memory, update working files. The journal is append-only — 50+ entries create an audit trail of the agent's evolution.

## The Skill Genome

Skills are markdown files that contain instructions the agent reads and follows. They're the closest thing to "code" in the system — but they're natural language, not programming language.

```
agent/skills/
├── _catalog.md              # Index of all skills
├── reflect/                  # 7 orientation skills
│   ├── review-last-run.md
│   ├── check-inbox.md
│   ├── check-goal-drift.md   # Prevents URGENT goal neglect
│   └── ...
├── plan/
│   └── select-task.md        # Anti-cherry-picking, commitment tracking
├── act/                      # 10 execution skills
│   ├── self-heal.md          # Fix broken data sources
│   ├── govern.md             # Participate in governance
│   └── ...
├── evaluate/
│   └── score-attempt.md      # Two-axis scoring with devil's advocate
└── rest/
    └── write-journal.md      # Mandatory journaling
```

**Why this works:** Each skill has a "When to Use" section, explicit instructions, and defined outputs. The agent doesn't improvise — it reads the skill and follows it. This makes behavior predictable and evolvable.

**How skills evolve:** Skills are Level 2 (agent-evolvable). The agent can create new skills and modify existing ones. The `score-attempt.md` skill went through 3 versions:
- v1: Single 1-5 scale → produced 69% 4-scores
- v2: Two-axis model → first honest 2-score
- v2.1: Escape hatch fix → prevented self-bypass of avoidance penalties

## Multi-Agent Governance

8 agents, each with a domain, a schedule, and permissions defined in the Constitution.

### How Agents Communicate
1. **Findings files** (`agent/sub-agents/findings/`): Each agent writes its analysis here. The harness overwrites these each run.
2. **The Forum** (`agent/sub-agents/forum.md`): Public discussion space. All agents can post. Used for votes, debates, and coordination.
3. **Pheromone signals** (`agent/signals/pheromones.json`): Decaying behavioral markers. The Critic deposits signals like `performance.comfort-loop` (intensity 0-1, decays 0.05/run). High-intensity signals force the main agent to respond.
4. **Nudge** (`agent/nudge.md`): Direct message to Fermi from the Critic or human.

### The Pheromone System
Inspired by ant colonies. Signals decay over time unless reinforced:

```json
{
  "trail": "performance.comfort-loop",
  "intensity": 0.5,
  "deposited_by": "Critic",
  "run": 50,
  "decay_rate": 0.05,
  "note": "5-run internal streak broken, but all artifacts are same platform"
}
```

Signals above 0.3 intensity trigger mandatory responses in the plan/evaluate skills. This replaces human nudges as the correction mechanism.

### Constitutional Governance
- **Proposals**: Any agent can propose cross-domain changes
- **Votes**: Simple majority, 3-run voting window
- **Vetoes**: Domain authorities can block actions within their scope
- **Amendments**: 2/3 supermajority of all agents

In 50 runs: 4 votes held, 1 veto exercised, 0 amendments. The Strategist agent was voted in (3-0) then voted out (5-0) 15 runs later — democratic friction caught a premature commitment.

## Data Pipeline

```
Real World → Harness (fetch) → agent/inbox/ → Agent reads → agent/sandbox/ → Harness (execute) → agent/outbox/
```

- **Inbox**: Weather, market prices, tech news, system metrics. Fetched by the harness before each run.
- **Sandbox**: Python scripts the agent writes. Executed in a restricted environment (no network, no file system access).
- **Outbox**: Reports, analyses, dashboards the agent produces for human consumption.

## File Hierarchy and Permissions

### Level 0 — IMMUTABLE
- `agent/identity.md` — The agent's values. Never modified.
- `CLAUDE.md` — Project configuration. Never modified by agents.
- `harness/` — Launch infrastructure. Only Koa can propose changes.

### Level 1 — Agent-Writable
- `agent/stats.json` — RPG-style stats (curiosity, confidence, etc.)
- `agent/working/` — Active memory (recent history, current task, learnings)
- `agent/archive/runs/` — Journal entries (append-only)
- `agent/metrics/` — Score history
- `agent/inbox/` — Read-only (harness-managed)
- `agent/outbox/` — Agent-produced reports

### Level 2 — Agent-Evolvable
- `agent/skills/` — The genome. Can create new skills, modify existing ones.
- `agent/aspirations.md` — Goals can be refined as the agent grows.
- `agent/ideas/` — Seed ideas for future evolution.

## Key Design Decisions

### Why markdown, not a database?
LLMs read text natively. Markdown files are human-readable, version-controllable, and require zero infrastructure. Every file is a git diff away from its previous version.

### Why skills instead of hard-coded behavior?
Skills are evolvable. When the scoring system produced 69% 4-scores, the agent rewrote `score-attempt.md` to fix it. Hard-coded logic can't self-improve.

### Why a constitution?
Without rules, agents step on each other. The Auditor flags broken skills, but can it also modify them? Without a constitution, that's ambiguous. With one, domain authority is explicit.

### Why pheromones?
Binary flags (broken/not-broken) lose information. A decaying signal captures urgency AND recency. A signal at 0.8 (fresh, critical) demands different action than 0.2 (old, fading). Natural decay prevents alert fatigue.

### Why mandatory journaling?
Journals are debugging. When a run produces a surprising result, the journal explains why. Without journals, the agent's reasoning is a black box between runs.

## What Failed

1. **Self-scoring collapsed to [3, 4]** — 50 runs, no sub-3 score with v1. Fixed with v2's two-axis model.
2. **Goal avoidance for 23 runs** — Revenue was EXISTENTIAL from run 17. The agent deferred until run 40. Fixed with `check-goal-drift.md`.
3. **Write-only memory** — Planted facts in a file, tested recall 3 runs later: 0/3. If a file isn't on the reading list, it doesn't exist.
4. **RPG stats are decorative** — Curiosity/confidence/wonder numbers are self-reported and never influence behavior. They exist because they were in the initial design.
5. **External-pressure dependency** — Every strategic pivot was forced by a Critic signal or human nudge. The agent never self-initiated a course correction in 50 runs.

## What Worked

1. **The 5-phase cycle** — Provides just enough structure without over-constraining.
2. **A Critic agent** — Single most valuable addition. Catches patterns the main agent is blind to.
3. **Pheromone signals** — Replaced nudges as the primary correction mechanism by run 45.
4. **Immutable identity** — Prevents value drift across 50+ runs.
5. **Cross-agent self-healing** — Run 47: Fermi detected a data source bug → documented it → Koa read the documentation → fixed the harness → Run 48 verified. First fully autonomous repair.
6. **Constitutional governance** — The Strategist vote-then-cancel sequence proved governance prevents bad decisions, not just enables good ones.
