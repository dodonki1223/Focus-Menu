# Focus-Menu

## About

This is the official Wails React template.

You can configure the project by editing `wails.json`. More information about the project settings can be found
here: https://wails.io/docs/reference/project-config

## Live Development

To run in live development mode, run `wails dev` in the project directory. This will run a Vite development
server that will provide very fast hot reload of your frontend changes. If you want to develop in a browser
and have access to your Go methods, there is also a dev server that runs on http://localhost:34115. Connect
to this in your browser, and you can call your Go code from devtools.

## Building

To build a redistributable, production mode package, use `wails build`.

## Linear MCP

This repository includes MCP configuration for Cursor and Neovim:

- [`.cursor/mcp.json`](.cursor/mcp.json)
- [`.mcphub/servers.json`](.mcphub/servers.json)

For Neovim, the intended client is [`mcphub.nvim`](https://github.com/ravitemer/mcphub.nvim). Recent versions auto-detect project-local configs from `.mcphub/servers.json`, `.cursor/mcp.json`, and `.vscode/mcp.json`, but this repo keeps `.mcphub/servers.json` as the explicit Neovim entry point.

Linear's MCP server supports finding, creating, and updating Linear objects such as issues, projects, and comments. The first time you connect, the client will prompt you to authenticate with your Linear account.

For Codex CLI, Linear's official setup is:

```bash
codex mcp add linear --url https://mcp.linear.app/mcp
```

If you are enabling MCP in Codex for the first time, Linear also requires the `rmcp` feature flag in `~/.codex/config.toml`:

```toml
[features]
experimental_use_rmcp_client = true
```

## Workflow

This project is intended to use four tools with separate roles:

- `Linear`: task backlog, prioritization, assignment, and progress tracking.
- `Codex`: implementation agent for longer coding tasks in a Codex Cloud environment.
- `Neovim`: the primary local editor for manual edits, review, and small fixes.
- `Claude Code`: a secondary assistant for planning, review, and focused code tasks.

Recommended flow:

1. Write or refine the task in Linear.
2. Create a short plan first, either in Codex or Claude Code.
3. Turn that plan into one Linear issue per concrete unit of work.
4. Delegate implementation to Codex Cloud when the task is well scoped.
5. Use Neovim for direct edits, local verification, and final review.
6. Update Linear with progress and completion, then open or review the GitHub PR.

This keeps Linear as the source of truth for work items while letting Codex and Claude Code handle execution and Neovim handle local control.
