---
pretty_name: ProofLoc-Olympiad (paper label version)
language:
- en
license: apache-2.0
tags:
- math
- reasoning
- step-level supervision
- olympiad
task_categories:
- question-answering
- text-classification
size_categories:
- n<1K
configs:
- config_name: paper-20260502
  default: true
  data_files:
  - split: test
    path: data/test.jsonl
---

# ProofLoc-Olympiad

This dataset contains 350 Olympiad-style math problem-proof pairs with step-level process labels.

## Fields

- `id`: formal benchmark ID, from `Olympiad001` to `Olympiad350`.
- `problem`: problem statement.
- `steps`: list of proof steps, one step per string.
- `first_error_step`: `correct` when all proof steps are correct; otherwise the one-based index of the first incorrect proof step.

## Label semantics

`first_error_step = "correct"` means all proof steps are judged correct.
`first_error_step = n` means the first incorrect proof step is step `n`, using one-based indexing over the `steps` list.

## Split

Use the test split for the published evaluation and report the label version.
