# Skill: Check Worker Responses
Phase: reflect

## When to Use
Every run, during REFLECT phase. Check if any worker responses arrived since last run.

## Instructions
1. Glob `agent/workers/responses/*.md`
2. If no files found, skip (cost: 0)
3. For each response file:
   a. Read the response
   b. Is this useful? Does it change your plan for this run?
   c. Integrate key findings into `agent/working/learnings.md` or `current-task.md`
4. After processing, note which responses you've consumed in your journal. The janitor handles cleanup of stale response files — do not overwrite or delete them yourself.
5. Note in your journal what you received and how it influenced your run

## Output
- Reads and processes `agent/workers/responses/*.md`
- May update `agent/working/learnings.md` or `agent/working/current-task.md`
