# Mandarin Human Review Dataset — Task A

This repository contains the implementation and outputs for **Task A: Prepare a Mandarin Dataset for Human Review**.

The goal is to create a new, traceable Mandarin translation dataset that can be sent to human reviewers to obtain fresh labels for Mandarin judge calibration/evaluation.

## Final Dataset

The final human-review set contains:

- **100 EN → ZH examples**
- **100 ZH → EN examples**
- **200 examples total**
- Dataset version: **v1.0**
- Human scoring scale: **0–4**
- Human scores are intentionally blank before review

## Data Source

The Task A examples were sourced independently from:

`FradSer/OpenSubtitles-en-zh-cn-20m`

Previously borrowed judge-calibration sources were excluded from the Task A source pool.

The pipeline preserves the original dataset row ID and provenance information for every selected example.

## Dataset Construction

The pipeline:

1. Loads the independent bilingual source.
2. Cleans and validates candidate source/reference pairs.
3. Builds a 2,000-example eligible pool.
4. Selects 100 EN→ZH and 100 ZH→EN base examples.
5. Creates a controlled range of translation quality.
6. Blinds and shuffles the human-review dataset.
7. Defines a self-contained 0–4 human scoring rubric.
8. Exports reviewer-facing and internal traceability files.
9. Generates SHA-256 hashes and a final manifest.

## Quality Coverage

For construction purposes, each translation direction contains:

| Internal quality bucket | Count |
|---|---:|
| High | 25 |
| Medium | 25 |
| Low | 25 |
| Very low | 25 |

These are **internal construction buckets, not human labels**.

Reviewers do not see the bucket or candidate-generation method.

## Human Review Scale

- **4 — Excellent:** Accurate, complete, and natural.
- **3 — Good:** Main meaning preserved with a minor issue.
- **2 — Fair:** Noticeable translation error, omission, addition, or fluency issue.
- **1 — Poor:** Major errors or substantial meaning loss.
- **0 — Failed:** Unusable translation, wrong language, source copying, unrelated output, or severe meaning loss.

Reviewers judge the candidate primarily against the source. The reference translation is supporting context.

## Reviewer-Facing Files

- `mandarin_human_review_reviewer.csv`
- `mandarin_human_review_reviewer.jsonl`
- `reviewer_instructions.txt`
- `human_review_rubric.json`

## Internal Files

The following files are for traceability and reproducibility and should **not be sent to reviewers**:

- `mandarin_human_review_internal_metadata.csv`
- `mandarin_human_review_internal_metadata.jsonl`
- `task_config.json`
- `task_a_manifest.json`


