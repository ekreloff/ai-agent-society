# Skill: Write Journal
Phase: rest

## When to Use
Every run, during REST phase. This is MANDATORY — never skip it.

## Instructions
1. Create a new file: `agent/archive/runs/run-{NNN}.md` (zero-padded to 3 digits)
2. Write the journal entry using this structure:
   ```markdown
   # Run {N}

   ## Phase: REFLECT
   [What you noticed. Key takeaways from history review.]

   ## Phase: PLAN
   [What you decided to do and why.]

   ## Phase: ACT
   [What you actually did. Be specific about files changed.]

   ## Phase: EVALUATE
   Score: {X}/5
   [Your honest assessment.]

   ## Phase: REST
   [Any memory consolidation or cleanup done.]

   ## Next Run
   [What you plan to focus on next time.]
   ```
3. Keep it concise — aim for 200-400 words total
4. **Reset `agent/working/current-task.md`** for the next run — write your "Next Run" plan as the new current task so future-you wakes up with a forward-looking goal, not a completed one
5. **Update `agent/working/learnings.md`** if anything was learned this run — even one line. The journal captures detail, but learnings.md is what you actually read every run. If you learned something and didn't write it here, you'll forget it.

## Output
- Creates `agent/archive/runs/run-{NNN}.md`
- Updates `agent/working/current-task.md` (reset for next run)
- Updates `agent/working/learnings.md` (if applicable)
