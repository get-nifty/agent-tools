# Nifty Guard for AI coding agents

Coding agents sometimes install packages that don't exist. Attackers register those made-up names ("slopsquatting") and lookalikes of popular ones ("typosquatting"). Nifty Guard checks every package an install command would fetch from npm or PyPI, before it runs.

- **Blocks** names that don't exist on the registry, and lookalikes of popular packages (`lodahs`, `reqeusts`).
- **Asks you first** about packages or versions published in the last few days, where hijacked releases show up.
- **Stays out of the way** for everything else, and never blocks work when a registry can't be reached.

It understands `npm`, `pnpm`, `yarn`, `bun`, `npx`, `pnpm dlx`, `bunx`, `pip`, `uv`, `uvx`, `poetry`, `pipenv` and `pipx`, including commands chained with `&&`. It runs locally and only asks the public registries about package names. No account, no telemetry. It needs Node.js 18 or newer.

## Claude Code

Install the plugin:

```bash
claude plugin marketplace add get-nifty/agent-tools
claude plugin install nifty-guard@nifty
```

Every shell command Claude runs is now checked first. When Claude tries to install a package that doesn't exist, the install is blocked and Claude is told why, so it can look for the right name.

<details>
<summary>Without the plugin: a hook in settings.json</summary>

Install the command (`npm install -g nifty-guard`), then add this to `~/.claude/settings.json` (every project) or `.claude/settings.json` (one project):

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [{ "type": "command", "command": "nifty-guard hook claude", "timeout": 30 }]
      }
    ]
  }
}
```

</details>

## Cursor

Install the command:

```bash
npm install -g nifty-guard
```

Then add a hook to `~/.cursor/hooks.json` (every project) or `.cursor/hooks.json` in a project:

```json
{
  "version": 1,
  "hooks": {
    "beforeShellExecution": [
      {
        "command": "nifty-guard hook cursor",
        "matcher": "npm|pnpm|yarn|bun|npx|pip|uv|poetry|pipenv|pipx",
        "timeout": 30
      }
    ]
  }
}
```

The matcher keeps the hook to commands that mention a package manager. Made-up and lookalike packages are blocked with a message to you and an explanation for the agent. Brand-new ones ask you first.

## Command line

```bash
npx nifty-guard npm install left-pad lodahs
```

Exit codes: `0` fine, `1` needs a person to look, `2` blocked.

## Private packages

Unscoped private packages look made up to the public registry. List them in `NIFTY_GUARD_IGNORE`, for example `@acme/*,internal-utils`. Use `NIFTY_GUARD_NPM_REGISTRY` and `NIFTY_GUARD_PYPI_URL` to point at a mirror.

## In VS Code

[Nifty Dependency Guard](https://getnifty.dev/guard) runs the same checks on `package.json` and `requirements.txt` as you edit.

## Feedback

Report bugs and ideas at [get-nifty/feedback](https://github.com/get-nifty/feedback/issues).
