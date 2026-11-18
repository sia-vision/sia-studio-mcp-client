---
name: sia-studio-workflows
description: Create or continue SIA Studio Characters, Locations, Artifacts, Character Looks and Scene-first Productions through the connected MCP account, inspect saved media, and recover original jobs.
---

Use the existing SIA Studio MCP connection. Start with `workflow_guide_get` for
the requested workflow, then `account_get` and saved-work search. Reuse the
Storyworld and exact assets from context; ask only when the destination or intent
is ambiguous. The guide supplies current tools, permissions and workflow details.

Handle the request in one conversation with sensible creative defaults and brief
progress. Share actual image previews and retained audition audio or the returned
Studio viewer link. Inspect the actual media before declaring agent review.
The saved audition voice and provider-native casting speech are different; explain
that limitation when sharing a casting preview.

- Character: reuse a saved identity reference, complete missing reference views,
  choose a provisional voice when needed, and retain the original audition/casting
  jobs. Preserve an existing identity and voice unless a change was requested.
- Location: accept text or saved references, establish the visual anchor, then
  continue all missing layout and lighting views. Read the current required roles,
  inspect each saved image, assign the intended role and read back completeness.
  One establishing image is not a complete Location. Label inferred geometry as inferred.
- Artifact: save a reusable prop, clothing item or accessory, create a design when
  requested, inspect it, and select the intended reference.
- Look: combine the exact Character and selected Artifact versions, inspect the
  generated fit image, and save it. Reuse both ingredients; do not recreate them.

For an incoming image, use the `sia-reference-intake` skill only when this host has
a supported local file handoff. Otherwise use an existing saved reference or
Studio's authenticated upload UI. Do not put image bytes/base64 in model arguments,
read OAuth stores, copy another client's credentials or invent source rights.

Persist operation IDs and exact inputs before mutations. After interruption read
current state and recover the original request; never automatically buy another
generation or repeat an uncertain upload. Existing Studio billing applies to
requested generation; do not add a second quote workflow.

Agent inspection, selected references, completed setup, human approval, canon and
Production pins are distinct. Changing saved assets must not silently change old
shots. Finish with saved results, returned Studio links and honest remaining work.

For a Production, request the `production` guide. Start from an inspected Scene,
choose format once, reuse pinned assets/Looks, and continue Director planning →
(optional non-destructive 3D staging via `production_stage_*`) → frames → takes →
scoped retakes → working cut → exact-output review (with deterministic cut
provenance via `production_export_provenance_get` when needed). Inspect prepared
shot references and omissions before quoting via `production_inputs_get`, and use
`production_inputs_save` when explicit reference purposes or required pins must
change within provider limits. Preserve earlier cuts and distinguish agent
inspection from final creator approval.

Share previews at meaningful workflow checkpoints using the current guide:
`reference_image_preview` for identity references, `location_reference_get` for
Location views, `artifact_image_preview` / `look_image_preview` for reusable
assets, `character_media_preview` for auditions/casting,
`production_media_preview` for each saved frame, retained take and completed cut,
and `production_stage_media_preview` for completed 3D stage study frames or
blockouts (`pending_client_render` exports render in Studio first).
Compatible MCP Apps hosts show a read-only saved-media card; other clients retain
native image/audio content or the authenticated Studio link. Do not promise that
a client supports inline video. Keep the returned shot/take/render URL parameters:
they open Storyboard, Video or Review at the intended saved work. Previewing is
separate from reference assignment, take selection and output approval.

Inspect the Director proposal before saving. For a first shot plan, omit
`basedOnRevision` and `correctionReason`; corrections require both. Read the latest
Production version between dependent writes. For continuous geography, inspect
and choose an anchor frame with its preview receipt before generating dependent
frames with continuity references. A queued dispatch is not completed media;
poll the original operation and retain earlier takes and cuts.
