# Xero MCP server

Review contacts in one authorized Xero organization and add contacts after approval.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `XERO_ACCESS_TOKEN`
- `XERO_TENANT_ID`

For local OAuth, use node local-auth/cli.mjs login ./connector.json with your own provider app; see AUTH.md. Your tokens remain in the native OS credential store.

Credential help: https://developer.xero.com/documentation/guides/oauth2/custom-connections/

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call xero_list_contacts '{}'
```

## Use with an MCP client

Launch `node /absolute/path/xero-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| xero_list_contacts | Read | xero list contacts |
| xero_get_contact | Read | xero get contact |
| xero_create_contacts | Explicit approval required | xero create contacts |

## Concrete workflow

Review contacts in one authorized Xero organization and add contacts after approval.

1. xero_list_contacts
2. xero_get_contact
3. xero_create_contacts

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=xero&integration=xero-mcp&utm_source=github&utm_campaign=github-xero-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/xero/).

## Provenance and maintenance

- https://raw.githubusercontent.com/XeroAPI/Xero-OpenAPI/master/xero_accounting.yaml

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
