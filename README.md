# Netsum for AI agents

Netsum keeps a business's books together with its accounting firm: the money view, invoices and bills, documents, the bank, VAT and deadlines.
This kit connects any AI agent that speaks MCP to it, with ready-made templates for the work people ask an agent for most.

> This repository is generated from [netsum-ai/netsum](https://github.com/netsum-ai/netsum) by `make agent-kit`. Do not edit it by hand: changes go there, and the next render replaces everything here.

## Connect

Give your agent one address: `https://mcp.netsum.ai/mcp` (or your firm's own, `https://<your firm's domain>/mcp`, shown in Netsum under Profile, AI agents). The agent finds Netsum's sign-in by itself (OAuth): you sign in to Netsum, choose the companies and what the agent may do, and it stays connected for 90 days (or 30, or 7) without signing in again. There is no key to copy and nothing to put in a header.

Only an agent that runs alone, with no person there to sign in (a script, a scheduled job, an API call), uses a personal agent key instead: make it in Netsum under Profile, AI agents, "Connect an agent with a key". It starts `nsk_`, is shown once, and goes as `Authorization: Bearer nsk_…`. A key is yours alone: keep it in an environment variable, never in code, and never in a shared or organisation-wide header (it would act as you for everyone there).

### Claude (claude.ai, the desktop and phone apps, Cowork)

1. Customize → Connectors → **+ Add** → **Add custom connector**.
2. Name it Netsum, paste `https://mcp.netsum.ai/mcp`, click Add. Leave the advanced settings empty.
3. Click **Connect**: Netsum opens; sign in, tick, Allow.

On a Team or Enterprise plan an Owner adds it once (Organization settings → Connectors); each person then clicks Connect and signs in.

As a plugin, with the templates as skills (Claude Code; the same plugin for Cowork):

```sh
claude plugin marketplace add netsum-ai/netsum-agent-kit
claude plugin install netsum@netsum-agent-kit
# then, in Claude Code: /mcp → netsum → Authenticate
```

The connector alone, in Claude Code:

```sh
claude mcp add --transport http --scope user netsum https://mcp.netsum.ai/mcp
claude mcp login netsum
```

### ChatGPT

1. Go to chatgpt.com/plugins, click **+**, then **Add custom MCP server**.
2. Name it Netsum, paste `https://mcp.netsum.ai/mcp` as the Server URL, choose **OAuth** and leave the client fields empty, then **Create as a plugin**.
3. Install it: Netsum opens; sign in, tick, Allow. In a Work chat, type `@` and pick Netsum.

In a Business or Enterprise workspace the admin adds it once; each person then installs it and signs in.

### Codex (and the ChatGPT desktop app)

```sh
codex plugin marketplace add netsum-ai/netsum-agent-kit
```

Then install Netsum from this marketplace in the Plugins Directory, and sign in when it asks.

### Cursor

[![Add Netsum to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](cursor://anysphere.cursor-deeplink/mcp/install?name=netsum&config=eyJ1cmwiOiJodHRwczovL21jcC5uZXRzdW0uYWkvbWNwIn0=)

If the button does not open Cursor, paste this link into your browser's address bar:

```text
cursor://anysphere.cursor-deeplink/mcp/install?name=netsum&config=eyJ1cmwiOiJodHRwczovL21jcC5uZXRzdW0uYWkvbWNwIn0=
```

Or add it to `~/.cursor/mcp.json` yourself:

```json
{ "mcpServers": { "netsum": { "url": "https://mcp.netsum.ai/mcp" } } }
```

Cursor opens Netsum's sign-in the first time. The plugin (the connector and the templates as skills): copy this repository into `~/.cursor/plugins/local/netsum` and reload the window.

### VS Code (GitHub Copilot)

[Add Netsum to VS Code](https://vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%257B%2522name%2522%253A%2522netsum%2522%252C%2522type%2522%253A%2522http%2522%252C%2522url%2522%253A%2522https%253A%252F%252Fmcp.netsum.ai%252Fmcp%2522%257D) (opens VS Code's review screen; nothing installs until you confirm). The link itself:

```text
vscode:mcp/install?%7B%22name%22%3A%22netsum%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.netsum.ai%2Fmcp%22%7D
```

Or in `~/.copilot/mcp-config.json`, or `.mcp.json` at the workspace root:

```json
{ "mcpServers": { "netsum": { "type": "http", "url": "https://mcp.netsum.ai/mcp" } } }
```

### Gemini CLI

In `~/.gemini/settings.json`:

```json
{ "mcpServers": { "netsum": { "httpUrl": "https://mcp.netsum.ai/mcp" } } }
```

Gemini CLI finds Netsum's sign-in on the first answer and opens the browser.

### Grok

On grok.com: Connectors → **New Connector** → **Custom**, paste `https://mcp.netsum.ai/mcp`, then sign in, tick, Allow.

On Grok Business or Enterprise, the team admin adds it once in console.x.ai (Grok Business → Connectors → Other, the address above); it then appears for each person, who clicks it and signs in once.

### A script that runs alone (a key)

Make a personal key in Netsum (Profile, AI agents, "Connect an agent with a key") and keep it in an environment variable, here `NETSUM_KEY`.

Claude API (Messages, with the MCP connector and the header `anthropic-beta: mcp-client-2025-11-20`):

```json
"mcp_servers": [{ "type": "url", "name": "netsum", "url": "https://mcp.netsum.ai/mcp", "authorization_token": "$NETSUM_KEY" }],
"tools": [{ "type": "mcp_toolset", "mcp_server_name": "netsum" }]
```

OpenAI Responses API:

```json
"tools": [{ "type": "mcp", "server_label": "netsum", "server_url": "https://mcp.netsum.ai/mcp",
            "authorization": "$NETSUM_KEY", "require_approval": "always" }]
```

## What an agent can never do in Netsum

Whatever the person's role and whatever they ticked when connecting you:

- approve a month (it needs the person's passkey, which no agent holds);
- file a return or a statement with the authority;
- pay anything, or move money;
- erase or delete anything;
- invite anyone, or change anyone's access;
- send anything outside Netsum by itself (an invoice you may ask to send waits for a person's review).

When the person asks for one of these, say so plainly and tell them where to do it in Netsum.

(Only a demo server in test mode lists some of these steps to agents, so a whole journey can be tested: `guide://testing`. A production server never does.)

## Templates

Each is served by Netsum's server as an MCP prompt, and is here as a skill (`skills/<name>/SKILL.md`), in the Claude, Codex and Cursor plugins alike.

- **Answer my accountant** (`skills/answer-my-accountant/SKILL.md`): Go through the questions the accounting firm is waiting on, one at a time, and help the person answer each.
- **Bank review** (`skills/bank-review/SKILL.md`): The bank lines that are not matched yet, with what would settle each, and for the firm's staff the matching itself.
- **Inbox triage** (`skills/inbox-triage/SKILL.md`): Sort the documents received into booked, waiting for a reading, unclear and duplicates, say what each unclear one needs, and for the firm's staff book them.
- **Invoice runner** (`skills/invoice-runner/SKILL.md`): Prepare this period's invoices as drafts from what the person says, and ask to send them for review.
- **Morning queue** (`skills/morning-queue/SKILL.md`): For the firm's bookkeeper, the queue across clients in the order to take it, with the deadlines that are near.
- **VAT prep** (`skills/vat-prep/SKILL.md`): Before a VAT return is due, what is left to make the period's figures complete, the VAT so far, and for the firm's staff the return's figures and file.
- **Weekly money brief** (`skills/weekly-money-brief/SKILL.md`): Where the money stands this week, what comes in and goes out in the next weeks, and what is late, in a few lines for the owner.

## Security

- You sign in yourself; the agent gets its own pass, never your password. See and disconnect every agent on Profile, AI agents; you get an email when one is connected.
- An agent starts with "look only", on the companies you choose; everything it does is recorded as the agent's, on your behalf.
- Keys are personal. Never paste a key into a shared or organisation-wide header (a Claude organisation's connector, a team's MCP settings, a shared repository): it would act as you for everyone there. A key goes in an environment variable, never in code.
- This repository holds no key, token or secret, and never will.

## What is in this repository

| File | What it is |
|---|---|
| `AGENTS.md` | How an agent works with Netsum: the instructions its server gives, what it can never do, the templates |
| `skills/<name>/SKILL.md` | The templates as skills |
| `plugin.json`, `mcp.json` | The plugin in the Agent Plugins format (Codex and ChatGPT, Cursor) |
| `.claude-plugin/plugin.json`, `.mcp.json` | The Claude plugin (Claude Code, Cowork) |
| `.claude-plugin/marketplace.json` | This repository as a Claude plugin marketplace |
| `.agents/plugins/marketplace.json` | This repository as a Codex and ChatGPT plugin marketplace |
| `server.json` | The entry in the MCP Registry |
