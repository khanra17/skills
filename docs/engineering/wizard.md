## What it does

`wizard` generates an interactive Bash script for steps only a human can perform. The script opens the relevant page, explains what to click, captures values, writes local environment variables, sets GitHub secrets or variables, confirms irreversible actions, and reports anything left unfinished.

The supplied template owns the user interface and helper functions. The agent scopes the procedure and writes only the stages below the `STAGES` marker.

## When to reach for it

Type `/wizard`, or let the agent reach for it when work is blocked on human-only actions such as provisioning an account, copying credentials, configuring a third-party dashboard, or approving a migration.

Do not use it for commands or API calls the agent can execute itself.

## Common questions

**Does the agent run the generated wizard?**

No. It checks Bash syntax and traces the stages, then tells the user how to run it. The user controls the browser and terminal input.

**How are secrets entered?**

`ask_secret` hides terminal input. `set_secret` passes the value to `gh secret set` through standard input, so the value does not appear in the command.

**Can I safely rerun a wizard?**

Yes. Saved environment values are offered as defaults, and `write_env` replaces the selected key without duplicating it. The template decodes ordinary single-line dotenv literals before reuse.

**What values need special handling?**

Escaped or multiline dotenv values must use the project's own environment tooling. The template stops instead of changing a value it cannot safely represent. Interrupted input also stops the script rather than writing an empty value.

**Should the generated script be committed?**

Only when it is a repeatable setup path the project should keep. One-off provisioning or migration wizards are temporary by default.

## It's working if

- The user approves the ordered stages and destinations before the script is written.
- Every captured value has a known source, destination, and secrecy level.
- The script opens a page before asking for a value from that page.
- Irreversible steps require confirmation.
- `bash -n` passes, and the final summary names skipped work without exposing secrets.
