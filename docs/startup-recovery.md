# Windows startup and safe recovery

## Alternative access routes (Windows)

If the normal desktop shortcut is unavailable or the browser dashboard is slow to open, the user has confirmed these two alternatives:

**Hermes CLI Desktop shortcut Target:**

```cmd
C:\Windows\System32\cmd.exe /k "hermes chat --cli"
```

This opens Command Prompt, runs the interactive Hermes CLI chat, and keeps the CMD window open.

**Open the dashboard from Command Prompt:**

```cmd
hermes dashboard
```

This starts the Hermes dashboard using the current installation/profile context. Check which profile is selected when multiple profiles are configured. The user's recent launch selected `jhermes`.

These are alternative interfaces, not gateway repairs. A slow or waiting dashboard command does not alone prove the gateway has failed. Allow time for initialisation, record the exact output and launch duration, and check gateway health separately with `hermes gateway status` before changing services or reinstalling.

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