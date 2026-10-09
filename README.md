# Nifty tools for AI coding agents

Small, local tools that make coding agents safer to work with. No account, no telemetry.

- **[nifty-guard](plugins/nifty-guard)** 0.2.0: Stops your coding agent from installing made-up (hallucinated), lookalike and brand-new npm and PyPI packages. Runs locally, no account.

## Install in Claude Code

```bash
claude plugin marketplace add get-nifty/agent-tools
claude plugin install nifty-guard@nifty
```

Each plugin's README covers Cursor and command-line use too.

More Nifty tools for VS Code and the browser: [getnifty.dev](https://getnifty.dev). Bugs and ideas: [get-nifty/feedback](https://github.com/get-nifty/feedback/issues).
