# CurseForge Modpack Setup (Minecraft 1.20.1 + Forge)

This folder is a ready-to-edit **CurseForge modpack skeleton** for Minecraft **1.20.1** using **Forge**.

## Quick answer: how to use this modpack

1. **Edit `manifest.json`**:
   - set your pack metadata (`name`, `version`, `author`)
   - replace placeholder entries in `files` with real CurseForge `projectID` + `fileID`
2. **Put your custom files in `overrides/`** (`config/`, `defaultconfigs/`, scripts, packs, etc.).
3. **Zip the pack** so the ZIP root contains exactly:
   - `manifest.json`
   - `overrides/`
4. **Import ZIP in CurseForge App** and launch the created profile.
5. **For Exaroton**, upload matching server files (`mods/`, `config/`, `defaultconfigs/`) to a Forge 1.20.1 server.

## What this setup currently includes (out of the box)

- ✅ A valid `manifest.json` template for **Minecraft 1.20.1** and **Forge 47.2.0**
- ✅ A ready `overrides/` directory structure
- ✅ Documentation for packaging and Exaroton upload
- ❌ **No actual mods are included yet** (you must add real CurseForge IDs in `files`)
- ❌ No prefilled configs/content beyond empty placeholder directories

## 1) Folder layout

```text
curseforge-modpack/
├─ manifest.json
└─ overrides/
   ├─ config/
   ├─ defaultconfigs/
   ├─ kubejs/
   ├─ scripts/
   ├─ resourcepacks/
   └─ shaderpacks/
```

### What each part does

- `manifest.json`: Required by CurseForge import/export. Declares Minecraft version, loader, and project/file IDs for mods.
- `overrides/`: Files copied directly into the instance when imported.
  - `config/`: Client/server config defaults.
  - `defaultconfigs/`: Forge defaultconfigs distributed with the pack.
  - `kubejs/`, `scripts/`: Optional scripting/customization directories.
  - `resourcepacks/`, `shaderpacks/`: Optional bundled visual assets.

## 2) `manifest.json` structure

The included `manifest.json` has all required sections:

- `minecraft.version`: `1.20.1`
- `minecraft.modLoaders[0].id`: `forge-47.2.0`
- `manifestType`: `minecraftModpack`
- `manifestVersion`: `1`
- `name`, `version`, `author`: Pack metadata
- `files`: CurseForge mod references (replace placeholder IDs)
- `overrides`: Folder to merge into the instance (`overrides`)

### How to fill `files`

For each mod, add one object:

```json
{
  "projectID": 238222,
  "fileID": 4574206,
  "required": true
}
```

- `projectID`: CurseForge project ID
- `fileID`: Specific file/build ID compatible with Forge 1.20.1
- `required`: Usually `true` for core mods

> Tip: Exporting a profile from CurseForge once is an easy way to generate and verify IDs.

## 3) Packaging instructions

1. Update `manifest.json` metadata and mod `files` IDs.
2. Place configs/scripts/assets in `overrides/`.
3. From inside `curseforge-modpack/`, create a zip that contains `manifest.json` and `overrides/` at the root.

Example commands:

```bash
cd /workspace/minecraft-modpack/curseforge-modpack
zip -r ../my-forge-1.20.1-modpack.zip manifest.json overrides
```

4. Test import the zip in CurseForge App:
   - **Create Custom Profile** (or import)
   - **Import** -> select `my-forge-1.20.1-modpack.zip`

## 4) Upload to an Exaroton server

Exaroton does not install a CurseForge client zip directly as a launcher would; you prepare the server with matching Forge + mod/config files.

1. In Exaroton panel, stop the server.
2. Set software/version to **Forge 1.20.1** (use the same Forge branch as the pack, e.g., 47.x).
3. From your modpack instance or exported server files, upload:
   - `mods/` (required server-side mods)
   - `config/`
   - `defaultconfigs/`
   - optional: datapacks/world content as needed
4. Keep only server-safe mods on the server (remove client-only mods such as minimaps/shaders/GUI-only mods).
5. Start server and watch console for missing dependencies.
6. Join using the same modpack on your client.

### Practical sync workflow

- Maintain one client profile in CurseForge.
- After updates, copy changed `mods/`, `config/`, and `defaultconfigs/` to Exaroton.
- Restart and validate logs after each change.

## 5) Validation checklist

- Minecraft version is exactly `1.20.1`.
- Forge loader is pinned in `manifest.json`.
- All mod IDs resolve correctly (`projectID` + `fileID`).
- Zip root contains `manifest.json` and `overrides/` (not an extra parent folder).
- Exaroton server mod list matches the client pack's required server mods.
