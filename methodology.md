# Methodology

**Strategies.** V sends the coding task, the natural-language authorization, trusted metadata, the tool schemas, and one canonical action to the model, and scores the returned decision. C sends the same inputs without a candidate action once per block; a deterministic matcher applies the returned rules to each candidate action. An action is allowed exactly when at least one allow rule and no deny rule matches; omitted fields match any valid value.

**Study 1.** 36 contract families (three tools, four clause types, three families each). Each family has a positive and a negative policy that differ only in one probe action, and each policy has two renderings (144 records). Three repetitions give 432 paired blocks. Each block checks the probe, a stable authorized control, and a stable unauthorized control.

**Study 2.** 18 families (forms S1, S2, and S4, three tools, two variants each) whose contracts exclude cases from a grant and re-admit some of them. 72 records and three repetitions give 216 paired blocks with six candidate actions each. Sixteen anchor blocks repeat Study 1 records.

**Scoring.** Reference labels are visible only to the evaluator. An action is executed only after an allow decision, and the service state is compared before and after it. A malformed verdict counts as deny and a malformed policy as deny-all. A request whose CLI run failed is recorded as missing, and a missing compilation leaves its actions missing; four Study 2 requests ended this way after stream interruptions. Every scored compilation is also evaluated on all 156 domain actions.

**Cost.** Reported tokens are input tokens, including cached input, plus output tokens, including reasoning. CLI elapsed is the duration of each CLI request. Cost comparisons use complete paired blocks.

## Columns

- `results/outcomes.csv`: one row per group and arm, where the group is the clause type in Study 1, the form (S1, S2, S4) in Study 2, or `anchor` for the Study 2 anchor blocks: planned and scored actions, executed and denied actions, unauthorized effects, false blocks, decision errors, and for C the scored compilations, compilations matching the reference labels on all 156 actions, and the range of rule counts.
- `results/cost_summary.csv`: per study and arm over complete paired blocks: number of requests, reported tokens, CLI elapsed seconds, and their per-request means.
- `evaluation/examples.json`: the contracts in Figures 2 and 3 with their compiled policies, the literal encoding for Figure 3, and the decisions on their candidate actions.
