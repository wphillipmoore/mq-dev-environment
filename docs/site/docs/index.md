# mq-rest-admin-dev-environment

Shared dockerized IBM MQ test environment for use across multiple
repositories. Provides container lifecycle scripts, seed data, and
a reusable GitHub Actions composite action for integration testing
against a real MQ queue manager.

## Consuming repositories

- [pymqrest](https://github.com/wphillipmoore/pymqrest) — Python
  wrapper for the MQ administrative REST API
- [mq-rest-admin](https://github.com/wphillipmoore/mq-rest-admin) —
  Java port of pymqrest
- pymqpcf — Python wrapper for the MQ PCF API (planned)

## What this repo provides

- **Two queue managers** (QM1 and QM2) running in Docker containers
  with REST API access enabled
- **Seed data** covering all major MQ object types (queues, channels,
  topics, namelists, processes, listeners)
- **Cross-QM routing** with bidirectional sender/receiver channel
  pairs and gateway QM aliases for REST API command routing
- **Lifecycle scripts** for starting, seeding, verifying, resetting,
  and stopping the environment
- **CI composite action** for use in GitHub Actions workflows

## Quick links

- [Getting Started](getting-started.md) — prerequisites and quick
  start
- [Environment Contract](architecture/environment-contract.md) —
  stable ports, credentials, and URLs
- [CI Integration](ci-integration.md) — composite action usage
- [Lifecycle Scripts](lifecycle-scripts.md) — script reference
