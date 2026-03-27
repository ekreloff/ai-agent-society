# Skill: Select Task (v2)
Phase: plan

## When to Use
Every run, during PLAN phase. Decides what you'll actually DO this run.

## Instructions

### Step 1: Check Commitments
Read the **"Next"** section of the most recent entry in `agent/working/recent.md`. What did you commit to last run? If you're about to do something different, you MUST write a 1-sentence justification (e.g., "Human nudge overrides" or "Blocker found"). Unjustified pivots are the #1 pattern of drift.

### Step 2: Read Context
- Read `agent/working/current-task.md` — your active focus
- Read `agent/aspirations.md` — your broader goals. Note urgency labels:
  - **URGENT** goals take priority over ACTIVE unless you justify otherwise
  - **DEFERRED** goals should not be selected
- Read `agent/signals/pheromones.json` — active behavioral signals from Critic, Budget Limiter, etc. If any signal intensity > 0.3 relates to your behavior (e.g., challenge-avoidance, stat-dishonesty), it MUST influence your choice.
- Optionally read `agent/challenges.md` if you want to attempt a diagnostic or real-world challenge

### Step 3: Choose ONE Task
Decide on ONE concrete action for this run. Not two. Not "several things." One.

**Specificity test:** Your task description must be concrete enough that a fresh agent instance could verify whether it was completed. Bad: "Do a challenge." Good: "C4 Run 2: rewrite select-task v2 with 3+ functional changes, test by using it this run."

### Step 4: Rate Difficulty
Rate your chosen task's difficulty: **Easy / Medium / Hard / Very Hard**.

**Anti-avoidance gate:** Check the challenge results table in `agent/working/friction-log.md`. If your last 3 completed challenges were all Easy or Medium difficulty, you must either:
- Pick a Hard+ task this run, OR
- Write a specific justification for why a Medium task is the right choice (e.g., "multi-run streak run 2 of 3 — continuation, not cherry-picking")

If any active pheromone signals avoidance behavior (e.g., `performance.audience-avoidance`) at intensity > 0.3, this gate is mandatory.

### Step 5: Write Decision
Write your decision into `agent/working/current-task.md`, including:
- The specific task
- Difficulty rating
- Which commitment it fulfills (or why you pivoted)
- Which ACT-phase skills you'll use (1-2 max)

## Output
- Updates `agent/working/current-task.md` with this run's specific plan
- Selects 1-2 ACT-phase skills to execute

## Changelog
- **v1** (runs 1-25): 5 generic steps, no guardrails. Root cause of cherry-picking, commitment drift, and the Critic's challenge-avoidance signal.
- **v2** (run 26): Added commitment accountability (step 1), signal integration (step 2), difficulty calibration + anti-avoidance gate (step 4), specificity test (step 3), priority weighting (step 2).
