# wizard

## What it does

`wizard` generates an interactive Bash script for steps only a human can perform. The script opens each page, says what to click and copy, captures the values, writes them to `.env` and to GitHub secrets or variables, asks for confirmation before anything irreversible, and ends with a summary of what was set and what was skipped.

A fixed template supplies the interface and helper functions. The agent scopes the procedure and writes only the stages.

## When to reach for it

Type `/wizard`, or let the agent reach for it, when work is blocked on something only you can do: creating an account, copying credentials, configuring a third-party dashboard, approving a migration step.

For commands or API calls the agent can run, it runs them and no wizard is needed.

## Common questions

**Who runs the script?**

You do, with `bash <script>` (from Git Bash or WSL on Windows). The agent checks the syntax and traces the stages but doesn't run it, because it opens a browser and waits for your input.

**How are secrets handled?**

Secret prompts hide what you type, and values go to `gh secret set` through standard input, so they never appear in a command line.

**Can I rerun it?**

Yes. Values already saved are offered as defaults, and each key is replaced in `.env`, never duplicated. A value the template can't represent safely (multiline, or needing escapes) stops the script with a message pointing at your project's own env tooling.

**Should the script be committed?**

Only when it is a setup path the project will reuse. A one-off provisioning or cutover wizard is deleted when the job is done.

## It's working if

- You approved the list of stages and where each value goes before the script was written.
- Each stage opens its page before it asks for a value from that page.
- `bash -n` passes on the script.
- The closing summary lists anything it could not set.
