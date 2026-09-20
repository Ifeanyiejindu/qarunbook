# qarunbook

A QA runbook your coding assistant can read and write.

Testers work through checks and raise what breaks. Your assistant reads what
failed, fixes it, and marks the issue resolved — and the pass underneath comes
back on its own, because status is derived rather than stored.

Sign up at **https://qarunbook.com** to get a workspace and your own token.

## Install (Claude Code)

```bash
claude plugin marketplace add Ifeanyiejindu/qarunbook
claude plugin install qarunbook@qarunbook
```

Then set your token — it is on your qarunbook home page, under **Your MCP
connection**:

```bash
export QARUNBOOK_TOKEN="qarb_…"
```

The token is yours, not the workspace's. It acts as you, with your role, and
removing you from a workspace revokes exactly it.

## What you get

| | |
|---|---|
| `/test-checklist` | Reads the app's code, works out every module, feature and journey worth testing, and creates the app in your runbook with the checks already in it. |
| `/qa-runbook` | Runs the testing. Establishes what is under test, creates real accounts, drives web and mobile, records each result with evidence, and verifies fixes. |
| MCP server | `list_checks`, `list_issues`, `set_result`, `add_issue`, `resolve_issue`, `update_check`, `import_plan` and the rest — the runbook as tools. |

## Other assistants

There is no plugin system outside Claude Code, so add the MCP server by hand
and copy the two `SKILL.md` files from `plugins/qarunbook/skills/` into wherever
your tool keeps its instructions.

**Codex** — `~/.codex/config.toml`

```toml
[mcp_servers.qa-runbook]
url = "https://qarunbook.com/api/mcp"
http_headers = { Authorization = "Bearer qarb_…" }
```

**Cursor** — `~/.cursor/mcp.json`

```json
{
  "mcpServers": {
    "qa-runbook": {
      "url": "https://qarunbook.com/api/mcp",
      "headers": { "Authorization": "Bearer qarb_…" }
    }
  }
}
```

## Roles

Everyone in a workspace has one, and it is enforced on both the web app and
the MCP tools.

- **tester** — record results, raise issues
- **admin** — the above, plus edit the plan, import, resolve issues, invite
- **owner** — the above, plus manage owners and delete the workspace

## Self-hosting

The server is a small Next.js app over MongoDB. Set `QA_MONGO_URI` and
`QA_SESSION_SECRET`, deploy, and point `QARUNBOOK_URL` at your own instance.
