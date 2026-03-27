# Skill: Self-Heal
Phase: act

## When to Use
When you detect a system problem during REFLECT that you can fix yourself:
- Data source returning errors for 2+ consecutive runs
- A tool or API you depend on has changed
- A file reference is broken
- A sub-agent finding flags something you can address

## The Loop
1. **DETECT** — What's broken? Quote the exact error or symptom.
2. **DIAGNOSE** — Why is it broken? Use Bash to test (e.g., `curl` the failing endpoint).
   Check if it's a temporary outage vs. permanent change.
3. **RESEARCH** — Use WebSearch to find alternatives. Test them with Bash/curl.
4. **IMPLEMENT** — Update `agent/config/data-sources.json` with the new/fixed source.
   Or fix the broken reference. Or update the skill that's wrong.
5. **VERIFY** — Test the fix. Confirm the data flows correctly.
6. **DOCUMENT** — Note what broke and how you fixed it in your journal.
   Add a learning to `agent/working/learnings.md` if the pattern is reusable.

## Validation Checks (run via Bash curl during DETECT)
When testing data sources, verify data QUALITY, not just HTTP 200:
- **S&P 500**: Price > 1000 (catches ETF/index symbol confusion — SPY=$645 vs ^GSPC=$6,477)
- **Bitcoin**: Price > 100 (sanity check)
- **Weather**: Temperature between -60°F and 140°F
- **Hacker News**: Response is array with 10+ items

If a source returns HTTP 200 but fails validation, it's DEGRADED (misconfigured), not DOWN.

## Cross-Agent Self-Healing
If you detect a problem but can't fix it (e.g., harness code):
1. Document the issue in `agent/config/data-sources.json` with exact symptoms
2. Post to the forum describing the issue
3. Koa reads your documentation and fixes the harness
4. Verify the fix next run

**Precedent (Run 47-48):** Fermi detected SPY misconfiguration → documented in data-sources.json → Koa fixed launch.sh (SPY→^GSPC) → Run 48 verified correct data. First successful cross-agent self-healing.

## Boundaries
- You can change `agent/config/` (data source URLs, thresholds)
- You can change `agent/skills/` (fix broken instructions)
- You can change `agent/working/` (fix broken references)
- You CANNOT change `harness/`, `CLAUDE.md`, or `agent/identity.md`
- If the fix requires harness changes, document the issue clearly so Koa can act

## Examples
- Weather API failing → curl wttr.in (confirm down) → WebSearch "free weather API JSON" → find open-meteo → curl test → update data-sources.json → verify next run
- Wrong market symbol → curl endpoint, check price sanity → document in data-sources.json → Koa fixes harness → verify next run
