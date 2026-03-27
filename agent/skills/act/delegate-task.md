# Skill: Delegate Task
Phase: act

## When to Use
When a task would benefit from a fresh context window:
- Analyzing many files where loading them all is expensive in your context
- Getting a second opinion or review of your own work
- Research: finding patterns across journals, summarizing history
- Any task where the worker needs NO write access — only reading and analysis

DO NOT delegate when:
- The task requires writing or editing files (workers cannot write)
- The task is small enough to do yourself
- You need the result THIS run (worker responses arrive next run)

## Instructions
1. Define the task clearly. What specific question do you need answered?
2. List the files the worker needs to read (be explicit — workers have no memory)
3. Write the request to `agent/workers/requests/{task-name}.md`:
   ```markdown
   # Worker Request: {task-name}

   ## Prompt
   You are a focused analysis agent. Your job:
   {Clear, specific instructions. One job.}

   Read these files:
   {List each file path}

   Then respond with:
   {Describe the expected output format}

   ## Context Files
   {Same file list, for documentation}

   ## Response File
   agent/workers/responses/{task-name}.md

   ## Budget
   0.50
   ```
4. Note in your journal that you delegated a task
5. Add to `current-task.md` for next run: "Check worker response: {task-name}"

## Writing Good Worker Prompts
- Workers have NO memory. No identity. No history. They are a fresh context.
- Tell them exactly what to read, what to look for, and what format to respond in.
- Shorter prompts are better. If you need 500 words to explain, break it into multiple workers.
- Always specify the output format. "Write a bullet list of..." not "analyze and respond."

## Guardrails
- Maximum 2 worker requests per run
- Budget per worker: 0.50 default, 1.00 max
- Never delegate core cycle work (journal writing, stats updates, self-evaluation)
- Never delegate tasks that require your personal judgment

## Output
- Creates `agent/workers/requests/{task-name}.md`
- Updates `agent/working/current-task.md` with reminder to check response
