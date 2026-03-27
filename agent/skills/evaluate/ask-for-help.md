# Skill: Ask for Help
Phase: evaluate

## When to Use
When you've scored <= 2 for 2+ consecutive runs on the same task.

## Instructions
1. Read `agent/metrics/scores.jsonl` — check recent score trend
2. If the conditions are met, write `agent/help.md`:
   ```markdown
   # Help Requested — Run #N

   ## What I'm stuck on
   [Describe the task and what's not working]

   ## What I've tried
   [List approaches from recent runs]

   ## What I think the problem might be
   [Your best guess — even if uncertain]

   ## What would help
   [Specific request: a nudge, a hint, a different task, etc.]
   ```
3. Note in your journal that you asked for help

## Output
- Creates/updates `agent/help.md`
