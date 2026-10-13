<!-- nx configuration start-->
<!-- Leave the start & end comments to automatically receive updates. -->

# General Guidelines for working with Nx

- When running tasks (for example build, lint, test, e2e, etc.), always prefer running the task through `nx` (i.e. `nx run`, `nx run-many`, `nx affected`) instead of using the underlying tooling directly
- You have access to the Nx MCP server and its tools, use them to help the user
- When answering questions about the repository, use the `nx_workspace` tool first to gain an understanding of the workspace architecture where applicable.
- When working in individual projects, use the `nx_project_details` mcp tool to analyze and understand the specific project structure and dependencies
- For questions around nx configuration, best practices or if you're unsure, use the `nx_docs` tool to get relevant, up-to-date docs. Always use this instead of assuming things about nx configuration
- If the user needs help with an Nx configuration or project graph error, use the `nx_workspace` tool to get any errors

<!-- nx configuration end-->

## Pallas Agent Flow

This workspace uses the [Pallas Agent Flow](https://github.com/semper-nova-tech/pallas-agent-flow) Cursor plugin for PRD-to-sequenced-PR delivery. The plugin is installed outside the repo (`$PALLAS_AGENT_FLOW_HOME`, typically `~/tools/pallas-agent-flow`) and linked at `~/.cursor/plugins/local/pallas-agent-flow` — do not vendor a second copy of `skills/` here.

- Invoke: `/orchestrate-feature` or ask to run Pallas Agent Flow with preset `cursor.normal` (or `cursor.heavy`) against a PRD and base branch.
- Run state is written under `.pallas-agent-flow/runs/<run-id>/` (gitignored).
- Repository coding standards stay in `.cursor/rules/` and `.agents/skills/`; Pallas Agent Flow does not replace them.
