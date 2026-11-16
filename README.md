# Sia Studio MCP Client

Connect Sia Studio from your agent to find saved creative assets, preview saved images and auditions, and work on Storyworlds and Productions you can access. This Agent Plugin includes the Sia Studio MCP configuration and the `sia-studio-workflows` skill.

- **Cursor.** Copy the package into `~/.cursor/plugins/local/sia-studio` for local testing. Reload Cursor, open **Customize → Plugins → Sia Studio**, and authenticate the MCP server. See [Cursor’s plugin guide](https://cursor.com/docs/plugins).
- **Grok Bot.** In **Connect apps**, select **Add a custom connector → Remote HTTPS**. Use `Sia Studio` as the name and `https://mcp.sia.vision/studio` as the Server URL. Follow Grok Bot’s sign-in flow. See [Grok Bot’s connector guide](https://docs.x.ai/grok-bot/computer-and-apps).
- **GitHub Copilot.** Add an HTTP server named `sia-studio` using `https://mcp.sia.vision/studio`, then sign in through your client. For the CLI, run `copilot mcp add --transport http sia-studio https://mcp.sia.vision/studio`. See [GitHub’s MCP guide](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers).
- **ChatGPT and Codex plugin directory.** Sia Studio uses the same hosted endpoint. Directory distribution follows [OpenAI’s plugin ZIP submission process](https://developers.openai.com/plugins/deploy/submission).

Each client connects with its own OAuth grant. Review the requested permissions in Sia Studio. Edits require the applicable write permission and Storyworld access. Generation requires its own permission and uses available Studio credits. Manage grants in [Studio Connect](https://studio.sia.vision/dashboard/?tab=connect).

To verify a connection without changing Studio data, use `workflow_guide_get` with `{"workflow":"image"}`. Saved images can appear as interactive cards or image attachments depending on the host.

This client package is available under the [MIT License](LICENSE).


## Saved-media previews and Production review

Version **0.2.2** includes guidance for the complete Location and Scene-first
Production workflows. Start with `workflow_guide_get` for the requested workflow;
it supplies current tools and state requirements from the hosted server.

- Preview Character references, auditions and casting with saved-media tools.
- Complete and inspect a Location's required establishing, layout and lighting
  roles, keeping inferred layout labelled as inferred.
- Preview reusable Artifact/Look images before selecting them.
- Use Director AI to plan coverage from the saved Scene, then inspect starting
  frames, retained takes and the completed working cut.

Compatible MCP Apps hosts display saved-media cards with images or bounded
retained audition audio. Cards can show planned shot context and open Studio at
the relevant stage. Other clients retain native image/audio attachments or the
returned authenticated Studio link. Host support varies; private video playback
uses Studio and is not promised inline in chat.

Keep the returned `shotId`, `takeId` and `renderId` URL parameters when sharing a
Production preview. They open the intended shot, retained take or saved cut,
including historical cut versions. Opening a preview does not select a take,
rebuild a cut or approve an output. Studio Review keeps picture, cue tracks and
planned rhythm together; planned timing is distinct from observed footage.

The client contains configuration and workflow guidance, not server credentials
or private creative assets. Its version is independent of the hosted gateway,
the MCP Registry metadata version and marketplace approval. Existing account
billing applies only when requested generation is actually launched. No new
Registry publication or marketplace submission is implied by this release.

See the [media and recovery guide](https://docs.sia.vision/media-and-recovery) for
preview fallbacks, interrupted jobs and review boundaries.
