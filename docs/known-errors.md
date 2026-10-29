# Known Hermes error patterns

These are incident patterns observed in this environment, not proof of one root cause. Confirm the installed version and command help before applying a fix.

## `GatewayUnavailableError: Gateway starting: deadline`
**Observed meaning:** the job could not obtain a usable gateway before its startup deadline. The reason startup took too long is not established.

Next steps: capture `hermes gateway status`; note PID and heartbeat; check `hermes cron status`; confirm previous execution state before retrying. If it recurs after cold boots, record timestamps across several boots before changing startup configuration.

## Stale heartbeat / parked profile
A stale heartbeat is a symptom, not a diagnosis. Check the expected profile and whether the shared gateway reports it. Don't start a second gateway instance without confirming how this Hermes version manages profiles.

## Execution remains `running`
Use `hermes cron runs JOB_ID` again and note the execution ID. If it changes to `completed`, record that transition. If it remains running, inspect the matching output file and process before terminating anything. A foreground terminal command may also be waiting independently of scheduler status.

## `Scheduler restarted after this execution's owner exited before a durable terminal state` (`unknown`)
The scheduler cannot confirm a durable terminal state. Side effects may or may not have happened. Inspect files, repository state and external notifications before rerunning to avoid duplicates.

## `lost its durable fire claim ownership`
The execution lost ownership of the scheduled trigger and its result may have been discarded. Record execution ID and timestamps. Check whether files, commits or notifications were already created before triggering another run.

## `Operation interrupted: waiting for model response`
The model wait was interrupted, but the cause may be provider latency, connectivity, timeout settings or another issue. Capture the full error and provider/model; avoid retry loops that don't change the conditions.

## Debugging discipline
1. Capture exact output and timestamp.
2. Identify whether the failure is scheduler, gateway, model, tool, filesystem, Git or Pages.
3. Change one thing at a time.
4. Verify with a post-check tied to the failure.
5. Add a dated log entry and label hypotheses clearly.