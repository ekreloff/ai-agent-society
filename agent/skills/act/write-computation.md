# Skill: Write Computation
Phase: act

## When to Use
When you need real computation that text-processing tools can't handle:
- Mathematical modeling (compound interest, statistical analysis, Monte Carlo)
- Data transformation (parsing, sorting, aggregating)
- Algorithmic work (searching, optimizing, simulating)
- Numerical verification (checking your own math)
- Fermi estimations with real numbers

## Development Practice: Red-Green-Refactor
Follow test-first development. Safety before speed.

1. **RED — Write the test first.** Before writing any computation logic, define what "correct" looks like. Include assertions or expected-value checks in your script. If you don't know what the answer should be, you don't understand the problem yet.

2. **GREEN — Make it work.** Write the simplest code that passes your tests. Don't optimize. Don't be clever. Just make the assertions pass.

3. **REFACTOR — Clean it up.** Only after tests pass, simplify. Remove dead code. Rename variables for clarity. But don't change behavior — the tests should still pass.

Example:
```python
import json, math

# RED: Define expected behavior
def test():
    assert compound_interest(1000, 0.05, 10) == 1628.89, "10yr compound interest"
    assert compound_interest(1000, 0.05, 0) == 1000.00, "zero years"
    assert compound_interest(0, 0.05, 10) == 0.00, "zero principal"

# GREEN: Simplest implementation
def compound_interest(principal, rate, years):
    return round(principal * (1 + rate) ** years, 2)

# Run tests first, then compute
test()
result = compound_interest(10000, 0.07, 30)
print(json.dumps({"result": result, "tests": "passed"}))
```

If your script has no assertions, ask yourself: "How will I know if this is wrong?"

## Instructions
1. Define what you need to compute. Be specific about inputs and expected output.
2. Write assertions/tests FIRST — what should the answer look like? Include edge cases.
3. Write a Python script to `agent/sandbox/scripts/{name}.py`
4. The script MUST:
   - Print results to stdout (this is what gets captured)
   - Use JSON output format when possible (easier to parse next run)
   - Embed all data directly in the script (no file I/O)
   - Stay under 10KB
5. The script MUST NOT use these (blocked by harness safety scan):
   - `import os`, `sys`, `subprocess`, `shutil`, `pathlib`, `socket`, `http`, `urllib`, `requests`, `ctypes`, `signal`
   - `open()`, `eval()`, `exec()`, `__import__()`, `compile()`, `globals()`, `getattr()`
6. Safe imports you CAN use:
   - `math`, `json`, `random`, `datetime`, `decimal`, `statistics`
   - `collections`, `itertools`, `functools`, `heapq`, `bisect`, `operator`
   - `re`, `string`, `textwrap`, `copy`, `dataclasses`, `enum`, `typing`
7. Structure your script as: imports → test functions → implementation → run tests → compute → print results
8. Note in your journal that you submitted a computation
9. Results appear in `agent/sandbox/results/{name}.result.json` next run
10. If tests fail (stderr shows AssertionError), fix the logic and resubmit next run

## Embedding Data
Since you cannot use `open()`, embed data directly:
```python
import json, statistics

scores = [3, 4, 4, 3, 3, 4, 4, 3]
mean = statistics.mean(scores)
stdev = statistics.stdev(scores)
print(json.dumps({"mean": mean, "stdev": round(stdev, 3), "n": len(scores)}))
```

## Limits
- Max 3 scripts per run
- 30-second timeout per script
- 50KB stdout cap, 10KB stderr cap
- Scripts that violate safety policy get a result file explaining why

## Output
- Creates `agent/sandbox/scripts/{name}.py`
- Results arrive in `agent/sandbox/results/{name}.result.json` next run
