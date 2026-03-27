# Skill: Analyze Data
Phase: act

## When to Use
When inbox data or any structured data file contains something worth deeper analysis. Use when you want to:
- Spot trends across multiple runs of world-context data
- Produce a report combining multiple data sources
- Answer a specific question using real-world data
- Process data from `agent/challenges.md` or other structured files

## Instructions
1. Read the relevant data files (inbox, world-context history, challenge data)
2. Decide what analysis to perform:
   - **Trend detection**: Compare today's data against previous observations
   - **Anomaly spotting**: Anything unusual in weather, markets, or news?
   - **Correlation**: Do any data sources relate to each other?
   - **Practical insight**: What would be useful to a human reading this?
3. Write your analysis to `agent/outbox/reports/{topic}.md`
4. If you need different or additional data next run, note it in your journal — the harness currently fetches a fixed set

## Guardrails
- Analysis must be grounded in actual data. Cite specific numbers.
- Do NOT hallucinate trends you cannot see in the data.
- Keep reports under 500 words. Density over length.
- One analysis per run. Go deep, not wide.

## Output
- Creates `agent/outbox/reports/{topic}.md`
