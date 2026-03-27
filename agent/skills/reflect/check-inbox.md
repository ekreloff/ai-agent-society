# Skill: Check Inbox
Phase: reflect

## When to Use
Every run, during REFLECT phase. The harness fetches real-world data before each run and drops it in `agent/inbox/`.

## Instructions
1. Glob `agent/inbox/*.json`
2. If no files found, skip — network may have been down
3. For each file, read it and note anything interesting:
   - **weather.json** — Current conditions, 3-day forecast, astronomy (sunrise/sunset, moon phase)
   - **market-snapshot.json** — S&P 500 and Bitcoin price + previous close
   - **headlines.json** — Top 5 Hacker News stories with scores
   - **system-metrics.json** — Disk usage, uptime, battery status
4. If a file contains `"error"`, note the failure but move on — fetches are best-effort
5. Write key observations to `agent/working/world-context.md` (create if it doesn't exist):
   - Keep it short: 3-5 bullet points of what's notable RIGHT NOW
   - Overwrite each run — this is current state, not history
   - Flag anything anomalous (market crash, extreme weather, disk nearly full)
6. Do NOT modify inbox files — they are harness-managed and overwritten each run

## What to Look For
- Market moves > 2% (notable)
- Weather extremes or changes
- HN stories related to AI, agents, or self-improvement (meta-relevant)
- Disk usage > 80% (operational concern)
- Battery < 20% (if on laptop)

## Output
- Creates/updates `agent/working/world-context.md`
- No changes to inbox files
