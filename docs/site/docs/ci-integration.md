# CI Integration

This repository provides a composite action at
`.github/actions/setup-mq/action.yml` for use in GitHub Actions
workflows. The action starts the MQ containers, seeds them with
test objects, and optionally verifies the environment.

## Usage

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup MQ
        id: mq
        uses: wphillipmoore/mq-rest-admin-dev-environment/.github/actions/setup-mq@main
        with:
          verify: 'true'

      # Use the outputs in subsequent steps
      # ${{ steps.mq.outputs.qm1-rest-url }}
      # ${{ steps.mq.outputs.qm2-rest-url }}
```

## Inputs

| Input | Required | Default | Description |
| --- | --- | --- | --- |
| `project-name` | No | `mq-dev` | COMPOSE_PROJECT_NAME for container isolation |
| `qm1-rest-port` | No | `9443` | Host port for QM1 REST API |
| `qm2-rest-port` | No | `9444` | Host port for QM2 REST API |
| `verify` | No | `true` | Run `mq_verify.sh` after seeding |

## Outputs

| Output | Value |
| --- | --- |
| `qm1-rest-url` | `https://localhost:<qm1-rest-port>/ibmmq/rest/v2` |
| `qm2-rest-url` | `https://localhost:<qm2-rest-port>/ibmmq/rest/v2` |

## What the action does

1. **Start containers** — runs `scripts/mq_start.sh` with the
   configured ports and project name
2. **Seed objects** — runs `scripts/mq_seed.sh` to create all
   `DEV.*` objects on both queue managers
3. **Verify** (optional) — runs `scripts/mq_verify.sh` to confirm
   all expected objects exist via the REST API

## Port customization

Use the `qm1-rest-port` and `qm2-rest-port` inputs to avoid port
conflicts when running multiple MQ environments in the same
workflow:

```yaml
- name: Setup MQ
  id: mq
  uses: wphillipmoore/mq-rest-admin-dev-environment/.github/actions/setup-mq@main
  with:
    project-name: 'my-tests'
    qm1-rest-port: '19443'
    qm2-rest-port: '19444'
```
