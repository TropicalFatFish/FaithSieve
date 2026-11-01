# FaithSieve Supplementary Materials

This repository contains the archived paper PDF and benchmark files for FaithSieve.

## Contents

- `paper/LeanEvaluation.pdf`: archived submission PDF.
- `datasets/proofloc_olympiad/`: 350 Olympiad-style problem-proof pairs with first-error labels.
- `datasets/proofloc_university/`: 200 university-level problem-proof pairs with first-error labels.

Each dataset directory contains:

- `data/test.jsonl`: benchmark data.
- `README.md`: dataset card and field definitions.
- `manifest.json`: record count, fields, and file layout.
- `BENCHMARK_FORMALIZATION_REQUIREMENTS.md`: formatting and label requirements used when preparing the benchmark.

## Data Format

Each line in `data/test.jsonl` is a JSON object with four fields:

- `id`: benchmark instance identifier.
- `problem`: mathematical problem statement.
- `steps`: ordered list of proof steps.
- `first_error_step`: `"correct"` if all steps are judged correct; otherwise the one-based index of the first erroneous proof step.
