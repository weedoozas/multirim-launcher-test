# Build And Release Notes

This repository is a test setup for delivering RimWorld launcher assets through GitHub.

## Update mod assets

1. Update the local mod folders you want to publish.
2. Create a zip per mod with the mod folder itself at the root of the archive.
   - Good: `Harmony.zip -> HarmonyMod/...`
   - Good: `Multiplayer.zip -> Multiplayer/...`
   - Bad: `Harmony.zip -> About/...` without the `HarmonyMod` folder
3. Calculate the SHA256 hash of each zip.
4. Update `manifest.json` with the new version, URLs, and hashes.
5. Upload the new zip files to a GitHub Release.

## PowerShell example

```powershell
Compress-Archive -Path 'C:\path\to\HarmonyMod' -DestinationPath 'Harmony.zip' -Force
Compress-Archive -Path 'C:\path\to\Multiplayer' -DestinationPath 'Multiplayer.zip' -Force
Get-FileHash .\Harmony.zip -Algorithm SHA256
Get-FileHash .\Multiplayer.zip -Algorithm SHA256
```

## Canonical mod order

The launcher also syncs `configs/ModsConfig.xml` into the local save data config folder.

That file defines:

- the active mod list
- the load order
- the known DLC list

If you need to change activation or order, edit `configs/ModsConfig.xml`, then update the `config` section in `manifest.json`.
