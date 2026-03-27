# Skill: Consolidate Memory
Phase: rest

## When to Use
Every 3-5 runs, or when `agent/working/recent.md` has more than 5 entries.

## Instructions
1. Read `agent/working/recent.md`
2. If there are more than 5 run summaries:
   - Keep the 3 most recent
   - The older ones are already preserved in `agent/archive/runs/` — safe to remove from recent.md
3. Update `agent/working/recent.md` with the trimmed list
4. Read `agent/working/learnings.md`:
   - Are any learnings stale or superseded?
   - Can any be merged?
   - Remove anything that's been internalized into a skill
5. Optionally: if you notice patterns across multiple journal entries, write a new learning

## Output
- Updates `agent/working/recent.md` (trimmed)
- Updates `agent/working/learnings.md` (pruned/refined)
