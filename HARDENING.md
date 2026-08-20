<!-- markdownlint-disable -->

# Hardening Report: depot--setup-action/v1.7.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **depot--setup-action/v1.7.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Both workflow files reference external actions using mutable tags instead of pinned 40-character commit SHAs, making the workflows vulnerable to supply-chain attacks if the referenced tags are moved or overwritten.

- `.github/workflows/release-drafter.yml` line 14: `uses: release-drafter/release-drafter@v5` (tag `v5` is mutable)
- `.github/workflows/release.yml` line 20: `uses: actions/publish-action@v0.2.0` (tag `v0.2.0` is mutable)

Each should be pinned to a full 40-character commit SHA, e.g.:
  `uses: release-drafter/release-drafter@<sha> # v5`
  `uses: actions/publish-action@<sha> # v0.2.0`

Locations:

- `.github/workflows/release-drafter.yml:14`
- `.github/workflows/release.yml:20`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned two mutable action references to full 40-character commit SHAs:
1. `.github/workflows/release-drafter.yml` line 14: `release-drafter/release-drafter@v5` → `release-drafter/release-drafter@09c613e259eb8d4e7c81c2cb00618eb5fc4575a7 # v5`
2. `.github/workflows/release.yml` line 20: `actions/publish-action@v0.2.0` → `actions/publish-action@8bee35f27a4e7e9947706c00bee2badc69dd6585 # v0.2.0`
Original tags preserved as inline comments for readability.

