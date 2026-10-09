# FilmEase plugin

This package connects an AI host to the FilmEase remote MCP server and supplies orchestration guidance for movie discovery and personal tracking.

The checked-in `.mcp.json` targets the production Streamable HTTP endpoint. FilmEase OAuth 2.1 protects personal tools and uses the FilmEase web app for login and explicit consent.

Supported capabilities:

- Structured semantic discovery without a second intent-parser LLM call
- Title resolution
- Ratings and reviews
- Watchlist reads and writes
- Actual viewing history and rewatches
- Private companion labels
- Taste profile access
- Region and streaming-service preferences
- Existing FilmEase personalized recommendations

Public distribution still requires platform review and any platform-specific connector registration or test-account details.

## Connect and use FilmEase

Install the plugin, open its Connectors tab, and connect the bundled FilmEase
connector. FilmEase opens its own sign-in and consent screen. After you approve
access, ask Claude to find a movie, inspect your FilmEase library, or update your
movie state. Team and Enterprise organizations may require an owner to approve
the connector before members can connect their individual FilmEase accounts.

Example prompts:

- “Find five uplifting movies under two hours that I can stream tonight.”
- “Show the highest-rated films in my FilmEase library.”
- “Add Perfect Days to my watchlist.”
- “I watched After Yang last night and would give it a 9.”

## Troubleshooting

If FilmEase tools are unavailable, open the plugin's Connectors tab and confirm
that the FilmEase connector is connected and enabled for the conversation. If a
tool reports that authorization expired, disconnect and reconnect FilmEase. For
incorrect streaming availability, include the movie, country, and provider when
contacting support.

Support: https://www.filmease.net/support or info@filmease.net

## Privacy and data handling

FilmEase receives only the tool inputs needed to answer the user's request. It
may read or update the connected user's FilmEase ratings, private reviews,
watchlist, viewing history, taste profile, region, and streaming-service
preferences after authorization. Authentication determines the account; the
plugin does not ask Claude to provide a raw FilmEase user ID.

FilmEase's privacy policy explains data collection, use, retention, deletion,
and service providers: https://www.filmease.net/privacy. Terms of service are at
https://www.filmease.net/terms.

## Package maintenance

The Claude manifest lives at `.claude-plugin/plugin.json`; the Codex manifest
lives at `.codex-plugin/plugin.json`. Both packages reuse `.mcp.json`, the skill,
and the assets in this directory. Refresh or reconnect the MCP connection after
server deployments, and reinstall the plugin when testing a new manifest,
skill, or bundled asset version.

The Claude Directory submission record, validation notes, and update runbook
are in [`docs/CLAUDE_DIRECTORY_SUBMISSION.md`](docs/CLAUDE_DIRECTORY_SUBMISSION.md).
