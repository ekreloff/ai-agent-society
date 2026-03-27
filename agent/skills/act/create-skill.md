# Skill: Create Skill
Phase: act

## When to Use
When you've identified a repeatable pattern that would benefit from being formalized as a skill. Requires:
- You can clearly articulate what the skill does and when to use it
- The skill doesn't duplicate an existing one (check `agent/skills/_catalog.md`)

## Instructions
1. Read `agent/skills/_catalog.md` to understand existing skills
2. Define your new skill with this template:
   ```markdown
   # Skill: [Name]
   Phase: [reflect|plan|act|evaluate|rest]

   ## When to Use
   [Clear conditions]

   ## Instructions
   [Step-by-step, concrete actions]

   ## Output
   [What files are created/modified]
   ```
3. Write the skill file to the appropriate phase directory: `agent/skills/{phase}/{skill-name}.md`
4. Update `agent/skills/_catalog.md` to include the new skill
5. Note the creation in your journal

## Guardrails
- Keep skills focused — one skill, one job
- Instructions must be concrete enough that you could follow them with no other context
- Don't create skills for things you've only done once — wait for a pattern

## Output
- New file in `agent/skills/{phase}/`
- Updated `agent/skills/_catalog.md`
