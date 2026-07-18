# NECS validator example

[![Validate retrieval evidence](https://github.com/Madhvansh/necs-validator-example/actions/workflows/validate.yml/badge.svg)](https://github.com/Madhvansh/necs-validator-example/actions/workflows/validate.yml)

A minimal, runnable reference consumer for the
[`necs-validate`](https://github.com/Madhvansh/Neural-E-Commerce-Search/blob/v0.3.0/docs/validation.md)
TREC-style retrieval-evidence preflight.

This repository is maintained by the NECS maintainer to demonstrate the
cross-repository setup. It is a reference integration, not evidence of
independent adoption.

## What the workflow proves

On every push and pull request, GitHub Actions checks the sample qrels and run
files with the immutable `v0.3.0` release tag:

```yaml
- uses: Madhvansh/Neural-E-Commerce-Search@v0.3.0
  with:
    qrels: evaluation/sample.qrels
    run: evaluation/sample.run
    expected-task: task1_ranking
```

Copy [`.github/workflows/validate.yml`](.github/workflows/validate.yml) and
replace the two paths with your own evaluation artifacts.

The validator fails on structural integrity errors such as malformed values,
duplicate rows, non-finite scores, and configured task mismatches. Coverage,
unjudged-document, and advisory-rank differences warn by default; strict inputs
can promote them to errors.

## Run the same check locally

```bash
python -m pip install "https://github.com/Madhvansh/Neural-E-Commerce-Search/releases/download/v0.3.0/neural_ecommerce_search_madhvansh-0.3.0-py3-none-any.whl"
necs-validate \
  --qrels evaluation/sample.qrels \
  --run evaluation/sample.run \
  --expected-task task1_ranking
```

Compatibility reports are welcome through the
[dedicated issue form](https://github.com/Madhvansh/Neural-E-Commerce-Search/issues/new?template=validator_report.yml).
