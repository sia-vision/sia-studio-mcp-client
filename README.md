# Sia Studio MCP Client

Connect Sia Studio from your agent to find saved creative assets, preview images, and work on Storyworlds and Productions you can access. This Agent Plugin includes the Sia Studio MCP configuration and the `sia-studio-workflows` skill.

- **Cursor.** Copy the package into `~/.cursor/plugins/local/sia-studio` for local testing. Reload Cursor, open **Customize → Plugins → Sia Studio**, and authenticate the MCP server. See [Cursor’s plugin guide](https://cursor.com/docs/plugins).
- **Grok Bot.** In **Connect apps**, select **Add a custom connector → Remote HTTPS**. Use `Sia Studio` as the name and `https://mcp.sia.vision/studio` as the Server URL. Follow Grok Bot’s sign-in flow. See [Grok Bot’s connector guide](https://docs.x.ai/grok-bot/computer-and-apps).
- **GitHub Copilot.** Add an HTTP server named `sia-studio` using `https://mcp.sia.vision/studio`, then sign in through your client. For the CLI, run `copilot mcp add --transport http sia-studio https://mcp.sia.vision/studio`. See [GitHub’s MCP guide](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers).
- **ChatGPT and Codex plugin directory.** Sia Studio uses the same hosted endpoint. Directory distribution follows [OpenAI’s plugin ZIP submission process](https://developers.openai.com/plugins/deploy/submission).

Each client connects with its own OAuth grant. Review the requested permissions in Sia Studio. Edits require the applicable write permission and Storyworld access. Generation requires its own permission and uses available Studio credits. Manage grants in [Studio Connect](https://studio.sia.vision/dashboard/?tab=connect).

To verify a connection without changing Studio data, use `workflow_guide_get` with `{"workflow":"image"}`. Saved images can appear as interactive cards or image attachments depending on the host.

This client package is available under the [MIT License](LICENSE).
