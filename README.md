# Hermes Reliability Desk

A separate, evidence-first handbook for Hermes operations, gateway recovery, cron failures and manual daily logs.

Website: https://jazblue.github.io/hermes-reliability/

## Principles
- Preserve working projects and the shared gateway; diagnose before restarting.
- Separate verified facts from hypotheses.
- Verify side effects independently: execution status, output file, remote commit and live deployment are different checks.
- Never publish credentials, tokens, private URLs or unredacted configuration.
- Keep logs manual until the process is reliable enough to automate.

## Contents
- `docs/startup-recovery.md` — safe Windows startup checklist.
- `docs/known-errors.md` — observed error patterns and cautious next steps.
- `docs/radar-quality.md` — freshness and verification checklist for Tech Reddit Radar.
- `logs/` — dated operational notes and a reusable template.

This site is documentation only. It does not change Hermes configuration or run commands on the PC.