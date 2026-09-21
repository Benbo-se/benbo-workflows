# benbo-workflows

Reusable GitHub Actions workflows for the **public** repositories in the
estate.

## Why this exists separately

[`BenboStandard`](https://github.com/Benbo-se/BenboStandard) holds the
engineering handbook and the reusable workflows most projects call. It is
private, deliberately, because it describes where production runs.

**A public repository cannot call a reusable workflow in a private one.** No
setting changes it, and the failure is unhelpful: the run fails before any job
is created, so there are no logs — only "workflow file issue". Three `LEAD*`
repositories were made private to work around it, which is not an option for a
project whose point is being open source.

So the workflows public projects need live here, in public. This repository
holds no secret, names no host, and describes no production system. That is the
condition of it being public, and it is also why it is a separate repository
rather than BenboStandard being opened up.

BenboStandard remains the source of truth for the *decisions*. When the two
disagree, BenboStandard is right and this repository has drifted.

## Workflows

| Workflow | For |
|---|---|
| `go-ci.yml` | a Go project with a PostgreSQL-backed test suite |

Pin to `@v1`:

```yaml
jobs:
  ci:
    uses: Benbo-se/benbo-workflows/.github/workflows/go-ci.yml@v1
    with:
      go-version: "1.27"
      test-db-env: REDASMS_TEST_DATABASE_URL
```

A change here must not break every caller at once, which is what the tag is
for. `v1` moves only for changes that cannot break a caller.

## Callers

- [`RedaEkengren/RedaSMS`](https://github.com/RedaEkengren/RedaSMS)

`Benbo-se/ArgusmetricsSH` carries its own copies and stays that way until this
pattern has proven itself on one project. One at a time, when the worst case is
"something stops working".
