# TERRON learning prerequisite CI

Added 2026-10-23 for development validation. AGPL-3.0.

This workflow runs the public repository's existing tests for game mechanics,
native bot behavior and navigation. It does **not** run an always-on training
worker, import demonstrations, upload private training inputs, or mutate a model.

## Bounds and privacy

- Only standard `ubuntu-24.04` GitHub-hosted runners in this public repository.
- Three parallel suites maximum, two Vitest workers per suite, 15 minutes per job.
- Locked npm installation without lifecycle scripts; pinned official Actions.
- Read-only repository token; checkout credentials are not retained.
- No deployment, secrets, externally supplied commands, input URLs, custom
  machine types, uploaded artifacts, caches or recurring schedules.
- A private repository copy is blocked until its free quota and billing stop
  controls are reviewed separately. Public-runner eligibility is not permission
  to use GitHub Actions as a general-purpose compute farm.

## Run and read results

After merge, use **Actions → TERRON learning prerequisites → Run workflow**.
Supply a unique diagnostic `request_id`. Pull requests touching the workflow,
native core or tests also run the bounded suites. A local deployment adapter can
submit a manually requested check through existing GitHub CLI authentication.

Results and logs are in GitHub Actions. The job summary records the exact tested
commit and suite. No artifacts are uploaded, so there is no trajectory or weight
download/import step. Do not count these jobs as training matches or PPO samples.

These tests execute this repository's public source revision, **not** a frozen
local TERRON training runtime. Passing them does not establish source parity,
replay reproducibility, full-match victory rate or learned gameplay strength.

## Future extensions

Additional regression tests can cover command/observation contracts and replay
parity using explicitly approved, nonsensitive fixtures. Full training data or
checkpoint distribution requires a separate private-data and free-budget review.
