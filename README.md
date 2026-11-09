# Keep a customer contact handoff tidy

**Xero + your AI assistant · powered by PipMCP**

You want to keep a customer contact handoff tidy, using the account your team has actually connected.

**Made for:** Bookkeepers

For real use, you will need PipMCP and access to Xero.

## Ask your AI to set this up

Paste this into a coding assistant that can open project files and run commands, such as Codex, Claude Code or Grok Build. You do not need to understand the code first.

```text
Help me use this project: https://github.com/jannikco/xero-mcp

I'm not a programmer. My goal is: Keep a customer contact handoff tidy.

Read the project instructions and set it up in a new folder without overwriting my work.
Guide me through PipMCP and its private key setup; never ask me to paste secrets into this
chat. Run a documented sample-data demo if available, then help me get a first small
result from my connected app. Explain the result in plain English. Ask before changing
records, sending messages or publishing anything.
```

## Three useful things to ask for

```text
Show contacts in my authorized organization and inspect the one I choose.
```

```text
Prepare a contact for review and ask before saving it in the selected organization.
```

```text
Create a short contact-review note for our bookkeeping handover, using the organization
and contact details returned.
```

## Your path to a real result

```mermaid
flowchart LR
  A["Ask your AI"] --> B["Connect PipMCP"] --> C["Keep a customer<br/>contact handoff tidy"] --> D["Review together"]
```

1. [Open PipMCP setup](https://pipmcp.com/github/start?app=xero&integration=xero-mcp&flow=xero-contact-tax-review&utm_source=github&utm_campaign=github-xero-mcp&utm_content=people-first-readme) and sign in or create your account.
2. Connect the app in PipMCP with the permissions you want to grant.
3. Create the product API key through the official setup, add it privately to your AI project's environment, and ask your AI to try a small read.

**What to expect:** Connect Xero in your PipMCP account, then use your PipMCP key for the supported actions. Review proposed changes before they are sent. Results depend on the connected account and its permissions; check the returned outcome before relying on it.

Add your PipMCP key privately in your project settings. Keep keys out of chat and public repositories.

## Keep going

- [Find another useful integration](https://github.com/jannikco/pipmcp-connectors)
- [Connect an API you control](https://github.com/jannikco/openapi-to-mcp)
- [Try the GitHub project](https://github.com/jannikco/github-mcp)

<details>
<summary>Technical reference: installation commands, exact capabilities and troubleshooting</summary>

<!-- people-first:technical:start -->
# Xero MCP server

## Review Xero contact tax details

Prepare a checklist of contacts missing a tax number, without altering accounting records.

### Try the task with synthetic data

No product key is needed for this demo. Requires Node.js 22+.

```sh
npm ci --ignore-scripts
npm run demo
# Optional: save a private report to a new file.
npm run demo -- --output ./synthetic-report.json
```

Output: a task-specific JSON review report selecting 1 of 2 invented records. It includes the completed fixture receipt and a request trace; no provider request or write occurs.

The synthetic records use normalized review fields. Review and map your actual provider schema before applying the same selection to live data.

### Use your authorized account

[Activate this task](https://pipmcp.com/github/start?integration=xero-mcp&app=xero&flow=xero-contact-tax-review&utm_source=github&utm_campaign=github-xero-mcp&utm_content=task-demo), then set **PIPMCP_API_KEY** in your process environment. Provider credentials stay in PipMCP. Configure the provider connection and explicitly select integration/connection IDs when your account has several.

```sh
npm run preflight
```

Preflight checks access/discovery only; it does not count as a completed provider task. For an explicitly reviewed read, use the returned live schema and the exact operation/tool, arguments and stable idempotency key:

```sh
npm run verify:read -- --tool '<actual discovered read-only tool>' --arguments '<reviewed argument JSON>' --idempotency-key '<stable request key>' --confirm-read-only
```

Discovery/calls require connectors:read and connectors:call on the PipMCP key. The verification command performs only the selected authorized read; it refuses writes and never selects a customer operation automatically. Only a completed receipt establishes a live read. Missing access, pending jobs and uncertain outcomes remain explicit blockers. Reports contain receipt digests rather than customer payloads. No prices, trials or account allowances are changed.


**Use Xero from Claude Code, Codex, Grok Build and MCP clients through PipMCP. One PipMCP API key connects this package to private execution.**

[Activate with PipMCP](https://pipmcp.com/github/start?integration=xero-mcp&app=xero&utm_source=github&utm_campaign=github-xero-mcp) · [Integration directory](https://jannikco.github.io/pipmcp-connectors/integrations/xero/)

## Build something useful

Review contacts in one authorized Xero organization and add contacts after approval.

The package is an authenticated client: discovery, schemas, policy decisions and execution come from PipMCP. Provider implementation remains on the server.

## Quick start

Requires Node.js 22+. Clone this repository, then:

```sh
npm ci --ignore-scripts
npm test
npm start
# After configuring your provider in PipMCP and setting PIPMCP_API_KEY:
npm start -- --live
# Launch the stdio MCP bridge:
npm run server
```

Create a PipMCP API key with explicit connectors:read and connectors:call scopes. Set PIPMCP_API_KEY in the calling process environment. Provider credentials are configured in PipMCP. Multiple accounts require explicit PIPMCP_INTEGRATION_ID and PIPMCP_CONNECTION_ID from discovery. Existing keys do not gain scopes automatically.

## Built for coding agents

Install this repository's skill into your project:

```sh
node lib/cli.mjs agents install --client codex --scope project --project /path/to/project
# Use claude or grok for those clients.
```

Connect AI agents to Xero using one PipMCP API key and actual hosted tool discovery. Native AGENTS.md, CLAUDE.md and project skills support the current coding session. No additional AI model key is required. [capabilities.json](capabilities.json) describes the package; [llms.txt](llms.txt) indexes its instructions.

## Inspect actual tools before calling

```js
import {PipMCPGatewayClient} from './lib/index.mjs';
const client = new PipMCPGatewayClient(); // PIPMCP_API_KEY
const inventory = await client.getTools("xero");
console.log(inventory.data.tools);
// Select a real tool and validate your arguments against its returned schema.
// client.callTool(provider, actualToolName, reviewedArguments, {idempotencyKey});
```

PipMCP enforces workspace, role, connection, policy/approval and usage controls. Preserve the original idempotency key when retrieving/resuming a receipt. Pending and confirmation_required are not completed provider results; uncertain writes are held for reconciliation. The bridge never auto-approves a hosted action.

## Version 1 migration

This release uses the authenticated PipMCP gateway for real discovery/execution. Upgrade your MCP launch command and configure PIPMCP_API_KEY before reconnecting. Historical local runtimes remain available under their original MIT license in Git history. 

## Evidence and support

Transport, package and agent fixtures are tested. Authentication/provider access must be checked in your own configured workspace; synthetic fixtures do not establish live provider execution. Do not include credentials or customer records in public issues. MIT covers this public client.

## Provider setup reference

[Official provider documentation](https://raw.githubusercontent.com/XeroAPI/Xero-OpenAPI/master/xero_accounting.yaml). Credentials are entered in PipMCP; this package does not accept or store provider secrets.

<!-- people-first:technical:end -->

</details>
