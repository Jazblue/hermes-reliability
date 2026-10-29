# Windows startup and safe recovery

## First checks after powering on
1. Open Command Prompt.
2. Run `hermes gateway status`.
3. Record whether the shared gateway is running, the PID, heartbeat age and callback URLs.
4. Run `hermes cron status` to inspect scheduler health and late jobs.
5. For a specific job, use `hermes cron runs JOB_ID`, replacing JOB_ID with its real ID.
6. For Git publication, compare `git rev-parse HEAD`, `git rev-parse origin/master` (or the actual remote branch), and `git status --short`.

## Decision rules
- **Gateway healthy, one job failing:** diagnose that job first. Don't restart the shared gateway just to clear one status.
- **Heartbeat stale or gateway unavailable:** capture the status and exact error before a restart. Check whether other profiles share the listener.
- **Execution stays running:** query the job again after a short interval. Don't immediately launch a duplicate.
- **Execution says completed:** this confirms Hermes recorded a terminal state, not that every output or publication step succeeded.
- **Local and remote Git commits match:** that verifies the branch tip, not GitHub Pages deployment.
- **Live site:** open the actual URL and confirm the expected date/content.

## If a restart seems necessary
1. Save exact output and timestamp.
2. Check `hermes gateway --help` and installed-version documentation; don't guess commands.
3. Confirm whether restart affects the shared gateway and other profiles.
4. Restart only when evidence points to gateway health.
5. Re-run gateway and cron status, test one known job and record before/after evidence.

## Avoid
- Posting API keys, tokens or private configuration in public logs.
- Deleting/recreating jobs as a first response.
- Treating an old output file as proof a new run wrote it.
- Claiming a fix worked before the post-check passes.

## Incident template
- Date/time and timezone:
- Job/profile:
- Expected behaviour:
- Observed behaviour (exact error):
- Checks performed:
- Change made:
- Verification:
- Remaining uncertainty: