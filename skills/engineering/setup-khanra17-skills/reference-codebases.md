# Reference codebases

Prepare or update reference collections for `/reference-codebases`. Use Codebase Memory MCP; keep clones and indexes outside the working project.

## Reuse before downloading

Use MCP's `list_projects` to find suitable reference collections wherever they live. Inspect candidate reference collections only, not other consuming projects or their configuration. Ask when an index's purpose is unclear.

Reuse collections that fit the question and target versions. Shortlist only missing coverage. Collections follow the user's interests and may overlap: Laravel applications, Filament projects, or offline-sync implementations across languages.

If MCP is unavailable, don't install but ask the user for installation, [codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp).

## Select sources

Shortlist remotely before cloning. Require **at least 500 stars**, then judge adoption relative to the ecosystem. Popularity gets a candidate considered; inspected engineering earns its place:

- Identify the relevant implementation and inspect its failure handling and tests. A framework, a production application, and a teaching example provide different kinds of evidence.
- Check dependency versions and maintenance of the relevant code. A recent automated commit is not evidence of current practices. Exclude abandoned projects and obsolete API examples from current-practice collections.
- Check whether the useful implementation is actually available to inspect.

Present each candidate's URL, contribution, target-version fit, engineering evidence, caveats, and proposed revision. Prefer complementary examples; report a shortfall rather than padding a requested collection size.

Suggest `~/.reference-codebases/<collection>/`, with real repository checkouts beneath it. The user chooses names (you too suggest) and location outside the project; existing collections need not move.

Get approval for the sources and revisions, storage, connection changes, indexing, and project-configuration writes before applying them. Reusing an unchanged collection needs no new downloads or index.

## Prepare and verify

Prefer `git clone --depth 1 --single-branch` at the approved branch or tag. For existing checkouts, check remotes and revisions before using them. Approved updates use shallow fetches where possible. Ignore local reference checkout changes. Reindex only affected collections. Keep a shared collection within its intended version range; use a separate collection for incompatible targets. Indexing does not require installing dependencies or running repository scripts.

**Index the whole collection.** Check the installed tool schemas and verify support for the nested-repository layout. After indexing completes, verify a relevant source lookup from every member, checking skipped files and member revisions rather than trusting the parent directory's status.

If coverage fails, explain the limitation and ask before changing tools or storage. Per-repository indexes, source exports, and synthetic Git repositories are not substitutes for the requested layout. Leave setup pending unless the user accepts its limits.
