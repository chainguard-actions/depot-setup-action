<!-- markdownlint-disable -->

# Hardening Report: depot--setup-action/v1.7.2

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **depot--setup-action/v1.7.2** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files reference external actions using mutable tags or version strings instead of full 40-character SHA commit hashes. This exposes the workflow to supply-chain attacks where a tag could be silently moved to point to malicious code.

.github/workflows/check-dist.yml:
  - actions/checkout@v7
  - pnpm/action-setup@v6
  - actions/setup-node@v7

.github/workflows/release.yml:
  - actions/publish-action@v0.4.0

.github/workflows/release-drafter.yml:
  - release-drafter/release-drafter@v7

All of these should be pinned to their full 40-character commit SHA (e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`).

Locations:

- `.github/workflows/check-dist.yml:14`
- `.github/workflows/check-dist.yml:18`
- `.github/workflows/check-dist.yml:21`
- `.github/workflows/release.yml:18`
- `.github/workflows/release-drafter.yml:13`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all 5 unpinned action references to full commit SHAs:
- check-dist.yml: actions/checkout@v7 → @3d3c42e5aac5ba805825da76410c181273ba90b1 # v7
- check-dist.yml: pnpm/action-setup@v6 → @0977fd99725f1db4007ccb2928dbb4e90d06cc86 # v6
- check-dist.yml: actions/setup-node@v7 → @820762786026740c76f36085b0efc47a31fe5020 # v7
- release.yml: actions/publish-action@v0.4.0 → @23f4c6f12633a2da8f44938b71fde9afec138fb4 # v0.4.0
- release-drafter.yml: release-drafter/release-drafter@v7 → @34d80673e067bdc0c24568d3af899c216adcfaa9 # v7
All original tags are preserved as inline comments for readability.

