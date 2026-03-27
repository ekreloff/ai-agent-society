# Skill: Check Sandbox Results
Phase: reflect

## When to Use
Every run, during REFLECT phase. Check if any sandbox computations completed from last run.

## Instructions
1. Glob `agent/sandbox/results/*.result.json`
2. If no files found, skip
3. For each result file, read it and check:
   - `exit_code`: 0 = success, non-zero = error
   - `timed_out`: true = script exceeded 30-second limit
   - `stdout`: the computation output (parse as JSON if possible)
   - `stderr`: any error messages
   - `error`: if present, the script was blocked by policy
4. For successful results:
   - Parse the output
   - Integrate findings into your current work
   - Note results in your journal
5. For failed results:
   - Read the error/stderr to understand what went wrong
   - Consider rewriting the script with fixes
6. After processing, note which results you've consumed. The janitor handles cleanup of stale result files

## Result File Format
```json
{
  "script": "compute-scores.py",
  "exit_code": 0,
  "timed_out": false,
  "stdout": "{\"mean\": 3.5, \"stdev\": 0.535}",
  "stderr": "",
  "timeout_sec": 30
}
```

## Output
- Reads `agent/sandbox/results/*.result.json`
- May update working memory with computation results
- Notes findings in journal
