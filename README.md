# Luci model list

`model-manifest.json` is the model catalog Luci Desktop's model picker reads at
startup, from
`https://raw.githubusercontent.com/Memories-ai-labs/Luci-model-list/main/model-manifest.json`.

It is [t3code's manifest](https://github.com/pingdotgg/t3code/blob/main/apps/server/src/provider/model-manifest.json)
copied verbatim, same schema. The `Sync from t3code` workflow re-copies it every
six hours, so a model t3code adds shows up in Luci without a Luci release.

Luci reads `providers.claudeAgent`: each model's `status` (only `current` is
listed), `badge`, `profile` (reasoning efforts and context windows), and
`adapter.claudeCode.minVersion` (hidden when the user's `claude` is older).
Codex and Grok models come from the CLIs themselves, not from this file.

Luci keeps the newer of its bundled copy and this file by `updatedAt`, and the
last good download is cached on disk, so a bad or missing file never empties
the picker.

To change something by hand, edit `model-manifest.json` and bump `updatedAt`.
The next sync overwrites hand edits whenever t3code's copy changes.
