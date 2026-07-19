# NECS validator example

[![Validate retrieval evidence](https://github.com/Madhvansh/necs-validator-example/actions/workflows/validate.yml/badge.svg)](https://github.com/Madhvansh/necs-validator-example/actions/workflows/validate.yml)

A minimal, runnable reference consumer for the
[`necs-validate`](https://github.com/Madhvansh/Neural-E-Commerce-Search/blob/v0.3.1/docs/validation.md)
TREC-style retrieval-evidence preflight.

This repository is owned and maintained by the NECS maintainer as a
maintainer-controlled demonstration of cross-repository invocation of the
validator action. It is a reference integration, **not** evidence of
independent, third-party adoption.

## What the workflow proves

On every push and pull request, GitHub Actions runs two jobs that check the
sample qrels and run files with the `v0.3.1` release. Both supported pin styles
are exercised so either can be copied with confidence:

- **`validate-pinned-sha`** pins the action to the immutable release commit
  (`@6fefdad10b60e71eedfcedee1491d6e043ebe670`, i.e. `v0.3.1`) — the
  recommended, tamper-evident style.
- **`validate-tag`** pins the action to the readable `@v0.3.1` tag.

```yaml
# Recommended: immutable SHA pin
- uses: Madhvansh/Neural-E-Commerce-Search@6fefdad10b60e71eedfcedee1491d6e043ebe670 # v0.3.1
  with:
    qrels: evaluation/sample.qrels
    run: evaluation/sample.run
    expected-task: task1_ranking

# Readable tag pin
- uses: Madhvansh/Neural-E-Commerce-Search@v0.3.1 # readable tag
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
python -m pip install "https://github.com/Madhvansh/Neural-E-Commerce-Search/releases/download/v0.3.1/neural_ecommerce_search_madhvansh-0.3.1-py3-none-any.whl"
necs-validate \
  --qrels evaluation/sample.qrels \
  --run evaluation/sample.run \
  --expected-task task1_ranking
```

Compatibility reports are welcome through the
[dedicated issue form](https://github.com/Madhvansh/Neural-E-Commerce-Search/issues/new?template=validator_report.yml).
