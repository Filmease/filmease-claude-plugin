# Claude Directory submission

This document records the FilmEase Claude Directory submission completed on
2026-10-08 and the process to use for later versions. It intentionally excludes
reviewer credentials, tokens, webhook secrets, and other private values.

## What was submitted

FilmEase was submitted to Anthropic in two related forms:

1. A remote MCP connector backed by the production Streamable HTTP endpoint at
   `https://filmease-mcp.fancy-fire-1eba.workers.dev/mcp`.
2. A plugin bundle sourced from the public
   `Filmease/filmease-claude-plugin` repository. The bundle contains one skill,
   one remote MCP server, shared assets, and no local executable code.

The connector and plugin are separate Directory submissions. The plugin can
refer to the same MCP endpoint, but Anthropic reviews and tracks the two entries
independently. Until the connector is approved and matched, the plugin preview
may label the MCP server as unregistered.

The submission used a personal Claude Pro account while identifying the
publisher as Filmease LLC. The proprietary license in `LICENSE` remains in
effect; publishing the repository does not make the package open source.

## Preparation and verification

Before submission we:

- Kept the application source private and published only this minimal plugin
  package in the FilmEase GitHub organization.
- Pointed `.mcp.json` at the production remote MCP server.
- Verified all 25 advertised MCP tools against production, including OAuth,
  read operations, reversible write/delete pairs, and the app-card event.
- Seeded a synthetic reviewer account and supplied its credentials and a demo
  video directly to Anthropic. Those credentials are not stored in this
  package.
- Reworded MCP tool descriptions as factual capability descriptions, removing
  cross-tool orchestration instructions and model-behavior directives.
- Ran the MCP unit and integration suites, TypeScript checks, a Cloudflare
  deployment dry run, a production deployment, and a live health check.
- Added the Claude manifest, shared skill, production MCP configuration,
  icons, README, privacy/support links, and proprietary license.

## Connector submission

The connector submission declared:

- OAuth 2.0 with Dynamic Client Registration.
- 25 tools.
- Publisher: Filmease LLC.
- Data is handled by the FilmEase API.
- No health-data use and no sponsored content.
- A synthetic reviewer account and hosted demonstration video.

All required connector policy acknowledgements were accepted. Anthropic showed
the connector with slug `filmease` and status `In review` after submission.

## Plugin-bundle validation

Anthropic validated the public repository's `main` branch at commit `b74da03`.
The validation passed all seven checks and reported:

- 11 files totaling approximately 284.4 kB.
- One skill and one remote MCP server.
- Directory lints, name checks, and publisher checks passed.
- No local code execution.
- Five non-blocking warnings: `documentationUrl`, `privacyPolicyUrl`,
  `supportUrl`, and `termsOfServiceUrl` are Directory metadata ignored by
  released Claude Code builds, and `icon` is used by the Directory but ignored
  by Claude Code. These fields are intentional and should remain.
- The PNG assets passed as well-formed images; the validator did not treat them
  as executable code.

The plugin was listed for Claude Code, Cowork, and Claude apps on web, desktop,
and mobile.

## Submitted disclosures and settings

The plugin data-handling answers were:

- Personal data: reads and stores.
- A skill sends data outside declared connectors: no.
- Service retention: longer than 30 days.
- Intended for users under 18: no.

The submitter also confirmed the Directory terms and policy, the accuracy of
FilmEase's privacy disclosure, that the plugin does not exfiltrate credentials
or execute code outside its declared MCP server, and that Anthropic may contact
the account about the submission and policy changes.

The first plugin version was submitted for review with:

- Auto-publish for later passing versions enabled.
- GitHub push webhook selected for update detection.

Anthropic confirmed `Plugin submitted for review`. The first version still
requires Anthropic approval before it can be published. Auto-publish applies to
later passing versions, not to this initial review.

The GitHub webhook is **not configured yet**. Its setup creates a webhook URL
and secret and requires repository-admin access. Do not record that secret in
Git, logs, screenshots, or this document. Without the webhook, Anthropic still
checks the tracked branch about every six hours.

## Lessons learned

- Submit the MCP connector before the plugin bundle when the bundle embeds a
  remote server. Approval and automatic matching can lag behind the bundle
  submission.
- A public plugin repository need contain only the distributable manifest,
  skill, assets, license, and MCP configuration. The product and server source
  can remain private.
- Directory-only manifest fields can trigger harmless Claude Code warnings.
  Read the warning details before removing useful listing metadata.
- Tool descriptions should describe inputs, outputs, and side effects. Put
  workflow advice in the skill rather than telling the model how to combine
  tools inside each tool description.
- Validate every advertised production tool with a synthetic account and
  restore state after reversible write tests before giving reviewers access.
- Review data-handling answers separately for the connector and the plugin;
  Anthropic asks similar but not identical questions in each flow.
- Check the final-review defaults. Auto-publish and webhook delivery can be
  enabled even though the first version still needs approval.
- Never commit reviewer credentials, access tokens, OAuth secrets, or webhook
  secrets. Keep local provisioning helpers ignored as well.

## Updating the Directory entry

1. Make changes in this package and increment the manifest version when the
   user-facing bundle changes.
2. Validate `.claude-plugin/plugin.json`, `.mcp.json`, the skill, asset paths,
   public links, and the production MCP endpoint.
3. Run the MCP contract and live integration tests when tools or the endpoint
   changed.
4. Commit and push the package to the public repository's tracked `main`
   branch.
5. If the webhook has not been configured, allow up to roughly six hours for
   Anthropic's scheduled check or trigger a manual re-validation in the plugin
   settings.
6. Review the new version's scan results. With auto-publish enabled, a later
   version that passes may go live without a separate Publish click.

