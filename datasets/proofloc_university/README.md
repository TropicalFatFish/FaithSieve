---
pretty_name: University Proof Benchmark 200
language:
- en
license: apache-2.0
tags:
- math
- reasoning
- step-level supervision
- university-math
task_categories:
- question-answering
- text-classification
size_categories:
- n<1K
---

# University Proof Benchmark 200

This dataset contains 200 university-level math problem-proof pairs with step-level process labels.

## Fields

- `id`: formal benchmark ID, continuous within each subject, e.g. `Topology001`, `LinearAlgebra001`, `AbstractAlgebra001`, `RealAnalysis001`, `ConvexAnalysis001`, and `ConvexOptimization001`.
- `problem`: problem statement.
- `steps`: list of proof steps, one step per string.
- `first_error_step`: `correct` when all proof steps are correct; otherwise the one-based index of the first incorrect proof step.

## Label semantics

`first_error_step = "correct"` means all proof steps are judged correct.
`first_error_step = n` means the first incorrect proof step is step `n`, using one-based indexing over the `steps` list.

## Split

The benchmark is intended as a held-out evaluation set. Use the `test` split.

## Subject counts

- Topology: 20
- Linear Algebra: 40
- Abstract Algebra: 40
- Real Analysis: 50
- Convex Analysis: 30
- Convex Optimization: 20
