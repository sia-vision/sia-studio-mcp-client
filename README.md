# Sia Studio MCP

Sia Studio is a hosted MCP server for creating images, developing reusable creative
assets and producing scenes into retained working cuts. Connect your agent to
search saved work, create Characters, Locations, Artifacts and Character Looks,
plan shots with Director AI, inspect storyboards and takes, and review a Production.
Access is limited to the signed-in account's permitted Storyworlds and Productions.

This public companion repository contains setup instructions, MCP client
configuration and the `sia-studio-workflows` skill. The hosted service runs at
`https://mcp.sia.vision/studio`; cloning this repository does not run a local server.

## Connect from GitHub Copilot

Add a remote **HTTP** MCP server with:

- **Server ID:** `sia-studio`
- **URL:** `https://mcp.sia.vision/studio`
- **Authentication:** OAuth through Studio's Google sign-in and consent screen.

For a VS Code workspace, `.vscode/mcp.json` can contain:

```json
{
  "servers": {
    "sia-studio": {
      "type": "http",
      "url": "https://mcp.sia.vision/studio"
    }
  }
}
```

Start the server in your client, open the sign-in link, and review the requested
Studio permissions. No API key, npm package or locally hosted Studio backend is
required. Configuration formats vary between clients; see the
[VS Code MCP setup guide](https://code.visualstudio.com/docs/agent-customization/mcp-servers)
and [GitHub Copilot MCP guide](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers).

## Try the connected workflow

Start with a read-only prompt:

> Show the Sia Studio workflow guide for Production, then find my saved Productions
> and tell me which have a retained working cut. Do not change anything.

The agent should request `workflow_guide_get` with `{"workflow":"production"}`,
then search work accessible to your connected account. Further examples:

- “Show my Character's saved references and voice audition.”
- “Create a Location from these references, including layout and lighting views.”
- “Produce this saved Scene as a widescreen first cut using my saved cast and Location.”
- “Show the storyboard, retained takes and review link for this Production.”

Creating or changing saved work needs the relevant write permission. Requested
image, voice or video generation uses Studio credits. Previewing saved media
does not launch a replacement generation or approve an output.

## Other supported client setup

- **Cursor.** Copy the package, including `.cursor-plugin`, into `~/.cursor/plugins/local/sia-studio` for local testing. Reload Cursor, find `sia-studio` in **Customize**, and authenticate the MCP server with Sia Studio. See [Cursor’s plugin guide](https://cursor.com/docs/plugins).
- **Grok Bot.** Open the [Sia community app](https://grok-bot.directory/apps/sia) or use **Connect apps → Add a custom connector → Remote HTTPS**. For manual setup, use `Sia Studio` and the hosted MCP URL above. Complete sign-in and try an existing saved image preview.
- **ChatGPT and Codex plugin directory.** Sia Studio uses the same hosted endpoint. Directory distribution follows [OpenAI’s plugin ZIP submission process](https://developers.openai.com/plugins/deploy/submission).

Each client connects with its own OAuth grant. Review the requested permissions in Sia Studio. Edits require the applicable write permission and Storyworld access. Generation requires its own permission and uses available Studio credits. Manage grants in [Studio Connect](https://studio.sia.vision/dashboard/?tab=connect).

To verify a connection without changing Studio data, use `workflow_guide_get` with `{"workflow":"image"}`. Saved images can appear as interactive cards or image attachments depending on the host.

This client package is available under the [MIT License](LICENSE).


## Saved-media previews and Production review

Version **0.2.5** includes the branded Cursor package and guidance for explicit format selection (`16:9`, `1:1`,
`9:16`), multi-batch non-destructive 3D staging, interactive 3D stage and
bounded inline video MCP cards, prepared shot input inspection and exact cut
provenance. Start with `workflow_guide_get` for the requested workflow; it
supplies current tools and state requirements from the hosted server.

- Preview Character references, auditions and casting with saved-media tools.
- Complete and inspect a Location's required establishing, layout and lighting
  roles, keeping inferred layout labelled as inferred.
- Preview reusable Artifact/Look images before selecting them.
- Choose `aspectRatio` (`16:9` widescreen, `1:1` square/Instagram, or `9:16`
  vertical/mobile) when starting a Production or standalone generation, use
  Director AI to plan coverage from the saved Scene, optionally block and
  preview non-destructive 3D stage studies across full storyboards
  (`production_stage_*` and `production_stage_media_preview`), inspect prepared
  shot references (`production_inputs_get`), then inspect starting frames,
  retained takes and the completed working cut (with deterministic provenance
  via `production_export_provenance_get`).

Compatible MCP Apps hosts display read-only saved-media cards (images, bounded
retained audition audio and bounded inline video) and interactive 3D stage
viewports. Cards can show planned shot context and open Studio at the relevant
stage. Other clients retain native image/audio attachments or the returned
authenticated Studio link when inline video is oversized or unsupported by the
host.

Keep the returned `shotId`, `takeId` and `renderId` URL parameters when sharing a
Production preview. They open the intended shot, retained take or saved cut,
including historical cut versions. Opening a preview does not select a take,
rebuild a cut or approve an output. Studio Review keeps picture, optional
side-by-side 3D blocking (**Show 3D**), cue tracks and planned rhythm together;
planned timing is distinct from observed footage.

The client contains configuration and workflow guidance, not server credentials
or private creative assets. Its version is independent of the hosted gateway,
the MCP Registry metadata version and marketplace approval. Existing account
billing applies only when requested generation is actually launched. No new
Registry publication or marketplace submission is implied by this release.

See the [media and recovery guide](https://docs.sia.vision/media-and-recovery) for
preview fallbacks, interrupted jobs and review boundaries.


## Registry metadata

[`server.json`](server.json) records the remote server's public MCP Registry
metadata, including server name `vision.sia/studio` and this public repository.
The Registry metadata version is separate from the client package and hosted
service versions. Official MCP Registry publication and GitHub-verified Copilot
connector approval are separate review states.
