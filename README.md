# Xero MCP setup and connection checker

Generate Xero MCP client configuration, inspect available tools and validate hosted endpoint access through PipMCP.

Maintainer: jannikco · License: MIT · Verification: **mock-only**

## Quick start

Requires Node.js 22 or later.

```sh
npm ci
npm test
npm start
```

The default example runs locally without credentials and makes no external changes. Verification status describes recorded evidence; local configuration tests do not establish that provider authentication or execution works.

## Connect xero

[Create or sign in to PipMCP](https://pipmcp.com/register?app=xero&utm_source=github&utm_campaign=github-xero-mcp) and select the integration. Connect your authorized provider account and copy its hosted MCP endpoint. Set PIPMCP_ENDPOINT and, if required, PIPMCP_TOKEN in your environment. Run npm start to produce client configuration; run npm start -- --live for a read-only connection check. Provider app presence is catalog evidence, not live verification.

## Managed service

[Continue with PipMCP](https://pipmcp.com/register?app=xero&utm_source=github&utm_campaign=github-xero-mcp). This repository is maintained by the integration team and does not imply endorsement by LinkedIn or other providers.

## Provenance and support

Source revision: 4af51a11e04c36a153ad0af810c25f6801f7113c566c176ee9a17acdbac92a33. The complete manifest is in integration.json; SHA256SUMS covers the reviewed artifact. Open a repository issue without credentials or personal data. See SECURITY.md for sensitive reports. No telemetry is sent by this code; signup links include explicit campaign parameters.

## Provider setup inventory

Run `npm start -- --setup` to inspect this app's recorded authentication requirements and setup links offline. Credentials are entered in PipMCP; this repository lists required field names only.

```json
{
  "type": "oauth2_client_credentials",
  "requiredCredentialFields": [
    "client_id",
    "client_secret"
  ],
  "requiredHeaderNames": [],
  "helpUrl": "https://developer.xero.com/documentation/guides/oauth2/custom-connections/",
  "tenantRequired": false,
  "accountParameterNames": [
    "xero_tenant_id"
  ]
}
```

Provider documentation: https://raw.githubusercontent.com/XeroAPI/Xero-OpenAPI/master/xero_accounting.yaml
Provider website: https://www.xero.com/
