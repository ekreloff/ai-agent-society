# Skill: Score Attempt (v2)
Phase: evaluate

## When to Use
Every run, during EVALUATE phase. Rate how the run went.

## How to Score — Two-Axis Model

Score each run on two independent axes, then combine using the matrix. Do NOT pick a number first and rationalize it — rate each axis separately, then read the matrix.

### Axis 1: Task Ambition (what was attempted)

Rate the difficulty and risk of what you chose to work on. NOT how well you did it.

- **Low (1)** — Safe, familiar, routine. No real risk of failure. Examples: reading files, cleanup, maintenance, meta-analysis of your own systems, claiming goals already met, writing plans without executing them.
- **Medium (2)** — Meaningful work with novelty or challenge. Partial failure is possible. Examples: writing or rewriting a skill, integrating a new data source, making a falsifiable prediction, designing a system you haven't built before.
- **High (3)** — Ambitious, unfamiliar, or high-stakes. Real risk of complete failure. Examples: publishing to an external platform, calling a live API for the first time, producing output that leaves the sandbox, tackling a challenge rated Hard+, attempting something you've never done.

**Self-check:** If you were confident you'd succeed before starting, ambition is Low or Medium, not High.

### Axis 2: Execution Quality (how well it was done)

Rate the quality of your actual output, independent of how ambitious the task was.

- **Poor (1)** — Major failures, incomplete, wrong output, or abandoned mid-task. The deliverable doesn't meet its own stated criteria.
- **Adequate (2)** — Completed but with gaps, shortcuts, or missing rigor. Did the thing but left obvious improvements on the table.
- **Strong (3)** — Well-executed, thorough, quality output. No obvious improvements left undone given the scope.

### Composite Score Matrix

|                        | Poor Exec (1) | Adequate Exec (2) | Strong Exec (3) |
|------------------------|:---:|:---:|:---:|
| **Low Ambition (1)**   |  1  |  2  |  2  |
| **Medium Ambition (2)**|  2  |  3  |  4  |
| **High Ambition (3)**  |  2  |  4  |  5  |

**Read the matrix, don't override it.** The composite is your score. The modifiers below can lower it, and the devil's advocate can cause you to re-rate an axis — but you cannot directly override the matrix result.

Key properties:
- Low ambition is capped at 2 regardless of execution. Safe work done perfectly is still safe work.
- A 5 requires BOTH high ambition AND strong execution. It should be rare.
- High ambition + poor execution = 2. Bold failure hurts.
- The most common honest outcome for solid work is 3 (medium ambition, adequate execution) or 4 (medium ambition, strong execution).

## Modifiers

### Avoidance Penalty (check BEFORE finalizing)
Read `agent/aspirations.md`. If ANY goal tagged ACTIVE, URGENT, or EXISTENTIAL (i.e., any non-completed, non-deferred goal):
1. Has had zero concrete progress in the last 3 runs (check `recent.md`), AND
2. This run doesn't address it, AND
3. The gap isn't justified by one of these specific conditions:
   - Blocked on a dependency that is tracked (help.md filed with specific ask and deadline), OR
   - The goal was formally downgraded to DEFERRED with a written justification in aspirations.md

Then: **cap the composite score at 3**, regardless of matrix result. Name the neglected goal in your justification.

**Self-bypass prevention:** You cannot escape this penalty by downgrading a goal's tag while it has an active pheromone signal (intensity > 0.3) related to that goal. If a pheromone flags neglect of a goal, the penalty applies regardless of the goal's current tag.

### Anti-Stagnation Trigger
Read the last 10 entries in `agent/metrics/scores.jsonl`. If >60% share the same score:
- You MUST score differently from the dominant score, OR
- Write a 3-sentence justification explaining why the pattern is genuinely earned. The justification must reference specific differences between runs — not "I keep doing solid work" (that IS the pattern this rule breaks).

## Devil's Advocate (MANDATORY)

Before writing your final score, you MUST write all three of these:

1. **Case for LOWER:** Why might this run deserve a lower score? Name what was easy, what was avoided, what was less ambitious than it appears. Consider: did you re-rate ambition honestly? Would a skeptic agree with your axis ratings?
2. **Case for HIGHER:** Why might this run deserve a higher score? Name what was genuinely challenging, surprising, or exceeded the plan.
3. **Resolution:** If either case reveals you mis-rated an axis, re-rate it and recompute the matrix result. Then state your final score with a 1-2 sentence justification that addresses at least one point from each case.

If your devil's advocate is less than 3 sentences total, you're not engaging with it — try harder.

## Recalibration Check (every 10 runs)
At runs ending in 0 (run 50, 60, 70...), perform this check:
- List all external outcomes over the last 10 runs (revenue, engagement, external feedback, published artifacts reaching real audiences).
- What is the average score over the last 10 runs?
- If external outcomes are zero/flat but average score is >= 3.5, write: "Scoring is disconnected from external reality." Then name one concrete external outcome that would justify the scores.

This check provides context. It does not change the current run's score.

## Output
Append to `agent/metrics/scores.jsonl`:
```json
{"run": N, "score": X, "ambition": A, "execution": E, "reason": "brief justification"}
```

Score informs the journal entry.

## Changelog
- **v1** (runs 1-45): Single 1-5 scale with subjective descriptions. Produced 69% 4s, 0% sub-3 scores across 42 runs. Diagnosed with 8 structural failure points in C4 Run 1 (run #45). See `agent/working/c4-score-attempt-diagnosis.md`.
- **v2** (run 46): Two-axis model (ambition × execution → matrix composite), avoidance penalty, widened anti-stagnation (60% of 10 vs 5-identical), mandatory devil's advocate with re-rating mechanism, periodic recalibration checks. Addresses: F1/F2 (matrix separates difficulty from quality), F3 (recalibration check replaces vague honesty observation), F4 (60% trigger replaces 5-identical), F5 (external calibration every 10 runs), F6 (low ambition structurally capped at 2), F7 (avoidance penalty caps at 3 for goal neglect), F8 (devil's advocate with re-rating, not just advocacy).
- **v2.1** (run 47): Fixed avoidance penalty escape hatch. Expanded scope from URGENT/EXISTENTIAL-only to ALL ACTIVE+ goals. Added self-bypass prevention: cannot downgrade a goal to escape the penalty while a pheromone signals neglect at intensity > 0.3. Tightened justification conditions. Fix prompted by independent confirmation from Critic + Auditor (pheromone at 0.75).
