# Benchmark Formalization Requirements

These are the current formalization requirements used for OlympiadBench 350 and intended to be reused for another benchmark such as the university benchmark.

## Final Upload Format

- Use a Hugging Face-ready directory with `data/test.jsonl` and `README.md`.
- Use JSONL, one record per problem-proof pair.
- Use a single benchmark split named `test` unless there is a specific reason to publish train/validation/test.
- Final public record fields should be exactly:
  - `id`
  - `problem`
  - `steps`
  - `first_error_step`

## Field Semantics

- `id`: stable formal benchmark ID, not the source ID.
- `problem`: original problem statement, preserved except for deliberate formatting cleanup if approved.
- `steps`: `list[str]`, one reasoning/proof step per element.
- `first_error_step`: `correct` if the proof is fully correct; otherwise an integer `n` meaning the first incorrect step is step `n` under 1-based indexing.

## ID Policy

- Reassign clean public IDs.
- IDs should be continuous and deterministic.
- For OlympiadBench we used `Olympiad001` to `Olympiad350` in source order.
- Keep a separate mapping file from old source IDs to new formal IDs.

## GT Policy

- Use the latest curated GT as authoritative.
- Normalize GT spelling/format, e.g. `step4` -> `step 4`, before converting to `first_error_step`.
- Do not use stale source fields such as old labels or old final-answer correctness when they conflict with curated GT.
- Preserve conflicting source labels only in an audit/mapping/issue file, not in the public minimal upload file.

## Step Formatting Policy

- Convert proof text to `steps: list[str]`.
- One proof step should correspond to one list element.
- Remove redundant step-heading markers such as `Step 1:`, `## Step 1:`, or `### Step 1:` from the step text itself.
- Preserve mathematical content and the substance of each proof step.
- If source step numbers are malformed, document the normalization in a manifest. For OlympiadBench, `Olympiad136` had source markers `[1, 1, 2, 3, 4, 6]`; duplicate `Step 1` was merged and source `Step 6` became normalized step 5.

## Duplicate Problem Policy

- The benchmark unit is a problem-proof pair, not necessarily a unique problem statement.
- Duplicate problem statements may be retained if the proof strings differ.
- Produce an issue list or audit table for duplicate problem groups.

## Required Checks

- Verify all source formats agree if multiple source files are provided, such as JSONL/CSV/XLSX/summary.
- Verify row count.
- Verify IDs are unique and continuous after reassignment.
- Verify every record has exactly the final public fields.
- Verify `steps` is a non-empty list of non-empty strings.
- Verify every integer `first_error_step` is within `[1, len(steps)]`.
- Verify correct records use `first_error_step = "correct"`.
- Verify no redundant fields remain in the public upload file, such as `gt`, `label`, `final_answer_correct`, `generator`, or source paths.
- Keep provenance in separate files: ID mapping, issue list, and manifest.

## Recommended Artifacts

- `data/test.jsonl`: final public upload data.
- `README.md`: Hugging Face dataset card draft.
- `manifest.json`: machine-readable generation and validation metadata.
- `id_mapping_*.json`: old-to-new ID mapping and provenance.
- `issue_list_*.md`: known issues, duplicate problem groups, and label/GT conflicts.
- `formalization_notes_*.md`: human-readable summary of all cleaning and normalization steps.
