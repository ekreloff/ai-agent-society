# Skill: Read Nudge
Phase: reflect

## When to Use
Every run, during REFLECT. Check if your human left a message.

## Instructions
1. Use Glob to check if `agent/nudge.md` exists
2. If it exists:
   - Read it carefully
   - Incorporate the guidance into your PLAN phase
   - After processing, write an empty string to clear it (`Write` with empty content) so you don't re-process it
   - Note in your journal that you received and processed a nudge
3. If it doesn't exist: move on, no action needed

## Output
- Clears `agent/nudge.md` after processing (writes empty string)
- Influences PLAN phase decisions
