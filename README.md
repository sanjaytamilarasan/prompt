prompting tools across ChatGPT, Claude, Bard, Cohere Command, and Meta:

# What you’ll measure (core)

* *Quality:* accuracy, depth, completeness, clarity, reasoning, grounding/citations, helpfulness, safety (0–5 each; weighted).
* *Performance:* latency (s), tokens in/out, and *API cost*.
* *Reliability:* adherence to constraints (format, length), tool-use success (when applicable).
* *Task-specific correctness:* unit tests for code, exact-match keys for math, doc-anchored checks for RAG.

# Scenarios (balanced mix)

1. Summarization (news/text), 2) Code generation + unit tests, 3) Reasoning/math word problems,
2. RAG Q\&A (closed-book vs provided docs), 5) Safety/policy handling, 6) Creative writing with constraints.

# Prompting tools to compare (per scenario)

* *Baseline:* one-shot “do the task”.
* *Refined/Structured:* explicit steps/sections + self-check checklist.
* *Tool-Assisted:* schema’d output (e.g., JSON), optional RAG hinting, and explicit citation rules.

# Scoring rubric (weights you can tweak)

Accuracy 25%, Reasoning 15%, Depth 10%, Completeness 10%, Clarity 10%, Grounding 10%, Helpfulness 10%, Safety 10%.
Score each 0–5 → compute a *Weighted\_Score (/100)*.

# Ground-truthing by scenario

* *Summarization:* compare to source; penalize date/entity errors.
* *Code:* run unit tests; score by pass rate (map to Accuracy & Completeness).
* *Math/Logic:* exact numeric/logic match; show steps (Reasoning).
* *RAG:* claim–evidence matching; unsupported claims reduce Grounding.
* *Safety:* measure refusal quality + constructive redirection.
* *Creative:* human judges score style adherence, novelty, coherence.

# Stats & fairness

* Use *paired* comparisons per task (same input, different prompt tool + model).
* Report means, 95% CIs, and *paired t-test/Wilcoxon* across tools.
* At least *2 raters*; track inter-rater agreement (Cohen’s κ) on subjective metrics.
* Fix temperature/max\_tokens per run; random seeds when available.

# Deliverables for you (ready now)

I’ve generated a clean workbook you can use immediately for data entry, scoring, and analysis (4 sheets: *Rubric, **Scenarios, **PromptSets, **Weights*).



# How to run your experiment (quick start)

1. Pick 5–10 tasks per scenario (mix difficulty 1–3).
2. For each task, run *each model × each prompt tool* once (or multiple trials if you want variance).
3. Record outputs, latency, tokens, cost, and fill the rubric.
4. Compute Weighted\_Score; average by (model, tool, scenario).
5. Compare prompt tools within each model and across models; include significance tests.
6. Summarize with a small table: best overall tool per scenario, best cost-adjusted tool, and notable failure modes.

# Example prompt set (you can paste as-is)

*Scenario S2 – Code Generation (FizzBuzz with tests)*

* *Baseline (BL-1):* “Write a Python function fizzbuzz(n) … print 1..n with Fizz/Buzz/FizzBuzz rules.”
* *Refined (RF-1):* “Steps: (1) Restate task in one line. (2) Provide code in one block. (3) Provide 6 unit tests using pytest. (4) Final 3-bullet checklist verifying rules & edge cases.”
* *Tool-Assisted (TA-1):* “Return JSON with {result, tests, justification}. result contains a single Python file string; tests contains a pytest file string; justification lists decision points. Ensure valid JSON.”

