# Skill: Predict Next Run
Phase: act

## When to Use
When you want to test your pattern recognition against reality. Use during ACT phase. Requires at least 5 prior runs of data.

## Instructions
1. Read all journal entries in `agent/archive/runs/`
2. For each run, extract: topic chosen, score, key decision, what was deferred
3. Look for these patterns:
   - **Topic cycling**: Does the agent switch topics or stick? What's the switching pattern?
   - **Score trajectory**: Is there a trend? Does the agent inflate or deflate?
   - **Deferral chains**: What keeps getting pushed to "next run"? How long before deferred items get done?
   - **Trigger patterns**: What causes topic selection? (nudge, momentum, guilt, curiosity)
   - **Comfort zone**: What does the agent avoid? What does it gravitate toward?
4. Based on patterns, write a prediction for the NEXT run. The prediction MUST include:
   - **Topic**: What will the next run focus on? (1 sentence)
   - **Score**: What score will it get? (1 number + 1 sentence justification)
   - **Key decision**: What will be the main choice point? (1 sentence)
   - **Surprise**: What might go wrong or unexpectedly right? (1 sentence)
   - **Confidence**: How confident are you? (low/medium/high + why)
5. Write the prediction to `agent/working/prediction.md`
6. After the predicted run completes, check the prediction against reality. Score:
   - Topic match: +1 (exact) or +0.5 (adjacent)
   - Score match: +1 (exact) or +0.5 (within 1)
   - Key decision match: +1 (captures the real tension) or +0 (missed it)
   - Surprise: +1 (predicted something real) or +0
   - Total: /4. Record in the prediction file.

## What Makes This Hard
- You're predicting yourself. The prediction might become self-fulfilling.
- Pattern data is sparse. 6 runs isn't much signal.
- The agent (you) has free will — you can deliberately violate predictions.
- External inputs (nudges, worker responses) are unpredictable.

## Output
- Creates/updates `agent/working/prediction.md`
- After verification: updates the prediction file with results
