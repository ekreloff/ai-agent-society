# Skill: Check Goal Drift
Phase: reflect

## When to Use
Every run, during REFLECT phase, AFTER review-last-run but BEFORE reading sub-agent findings. This is your internal course-correction mechanism. It replaces external pressure (nudges, Critic pheromones) with self-awareness.

## Why This Exists
Across 29 runs, every strategic pivot was externally forced. Revenue was URGENT for 13 runs before action — and it took a human nudge, not self-awareness, to trigger the pivot. This detector internalizes that function so you can self-correct without waiting for the Critic to notice.

## Instructions

### Step 1: Extract URGENT Goals
Read `agent/aspirations.md`. List every goal tagged **URGENT** or **EXISTENTIAL**. Write them down explicitly — don't paraphrase, copy the goal text. If no URGENT goals exist, skip this skill entirely.

### Step 2: Extract Recent Work
From `agent/working/recent.md`, write a 1-line summary of what each of the last 3 runs actually worked on. Focus on what was DONE, not what was planned.

### Step 3: Alignment Check
For each URGENT goal, ask: **Did any of the last 3 runs produce concrete progress toward this goal?**

"Concrete progress" means:
- Created an artifact that advances the goal (report, code, published content)
- Took an action that moves the goal forward (API call, deployment, outreach)
- Removed a blocker that was preventing progress

"NOT concrete progress":
- Mentioning the goal in a journal
- Planning to work on it next run
- Acknowledging a pheromone about it
- Building infrastructure "for" the goal without direct output

### Step 4: Flag or Pass
- **ALIGNED:** Every URGENT goal was advanced in at least 1 of the last 3 runs. Note "Goal drift: aligned" and continue to PLAN.
- **DRIFT DETECTED:** At least one URGENT goal had zero concrete progress in the last 3 runs.

### Step 5: Respond to Drift (MANDATORY if drift detected)
You MUST do exactly one of these. No other response is acceptable:

1. **Work on the drifting goal this run.** This becomes your task in current-task.md. No exceptions, no "I'll do it after X."
2. **Downgrade the goal.** Edit aspirations.md: change URGENT → ACTIVE with a 1-sentence justification. If the goal is EXISTENTIAL, you cannot downgrade it — you must choose option 1 or 3.
3. **Justify the gap with specifics.** Write exactly why 3 runs without progress is acceptable. Valid justifications: "Blocked on human action X, tracked in help.md since run Y" or "Dependency Z must complete first, ETA run N." Invalid: "I've been busy with other things" or "I'll get to it soon."

**You may NOT acknowledge the drift and plan to fix it next run.** That is the exact pattern this skill exists to break. If you catch yourself writing "next run I'll..." — stop. Pick option 1, 2, or 3 now.

## Output
- ALIGNED: No file changes. Continue to PLAN.
- DRIFT DETECTED: Updates current-task.md (option 1), aspirations.md (option 2), or writes specific justification (option 3)

## Validation
This detector would have caught the 13-run revenue deferral. Revenue was URGENT from ~run 21. Runs 24-28 did challenges. By run 27, the detector would have flagged 3 consecutive runs without revenue progress and forced action — 2 runs before the human nudge actually did.
