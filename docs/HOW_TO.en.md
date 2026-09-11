# How to install and use Agent Pet

[中文](HOW_TO.zh-CN.md) · [Back to the project](../README.md)

This guide installs **Indigo · 靛蓝猫** (`indigo-cat`), **G.E.M.** (`gem-tang`), or both in a desktop app that supports Codex v2 custom pets. The packages contain ready-to-use images: no API key, image generation, or build tools are needed.

## 1. Download a pet

Open [Releases](https://github.com/Erizo0818/agent-pet/releases/latest) and download:

| File | Contents |
| --- | --- |
| `indigo-cat.zip` | Indigo only |
| `gem-tang.zip` | G.E.M. only |

Extract the ZIP. Keep `pet.json` and `spritesheet.webp` together inside the pet's folder. The included `LICENSE` and `CREDITS.md` describe reuse and attribution.

## 2. Install the folder

### Downloaded ZIP: no terminal required

Copy the extracted `indigo-cat` or `gem-tang` folder into the directory below. Create `pets` if it does not exist.

| System | Default directory | How to open it |
| --- | --- | --- |
| macOS | `~/.codex/pets/` | Finder → Go → Go to Folder (`⌘⇧G`) |
| Windows | `%USERPROFILE%\.codex\pets\` | Paste the path into File Explorer's address bar |

If the desktop app is configured with `CODEX_HOME`, use `<CODEX_HOME>/pets/` instead. The files must be on the computer running the desktop app; a copy inside WSL or a remote development machine does not install them in the Windows/macOS app.

For both pets, the resulting structure is:

```text
<CODEX_HOME or your home/.codex>/pets/
├── indigo-cat/
│   ├── pet.json
│   ├── spritesheet.webp
│   ├── LICENSE
│   └── CREDITS.md
└── gem-tang/
    ├── pet.json
    ├── spritesheet.webp
    ├── LICENSE
    └── CREDITS.md
```

There must be no extra wrapper such as `pets/agent-pet-main/pets/indigo-cat/` or `pets/indigo-cat/indigo-cat/`.

### Alternative: install from Git

Clone the public repository:

```sh
git clone https://github.com/Erizo0818/agent-pet.git
cd agent-pet
```

On macOS, run from the repository directory:

```sh
pet_dir="${CODEX_HOME:-$HOME/.codex}/pets"
mkdir -p "$pet_dir"
cp -R pets/indigo-cat pets/gem-tang "$pet_dir/"
```

On Windows, run in PowerShell from the repository directory:

```powershell
$petRoot = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $env:USERPROFILE '.codex' }
$petDir = Join-Path $petRoot 'pets'
New-Item -ItemType Directory -Force -Path $petDir | Out-Null
Copy-Item -Path 'pets\indigo-cat', 'pets\gem-tang' -Destination $petDir -Recurse -Force
```

To install only one pet, keep only its source path in the copy command. These commands replace files for the selected pets if already installed; back up any personal edits before running them.

## 3. Select and wake the pet

1. Open **Settings → Pets** in the desktop app.
2. Select **Refresh**, then choose **Indigo · 靛蓝猫** or **G.E.M.**
3. Enter `/pet` in the app, or choose **Wake Pet** from the command menu.

Enter `/pet` again to hide the floating pet. The app chooses animations as work progresses; the preview GIFs demonstrate the available artwork, not a separate animation-control interface. These controls follow the [official Pets guide](https://learn.chatgpt.com/docs/pets).

## 4. Update or remove

**Update:** download the new ZIP, or run `git pull --ff-only` in the repository. Back up the installed pet folder outside `pets`, then replace it with the new folder. Return to Settings → Pets and refresh/reselect the pet.

**Remove:** choose another pet or hide the current one, then remove only its `indigo-cat` or `gem-tang` folder from the installation directory and refresh. Other pets can stay in place.

## 5. Troubleshooting

| Symptom | Check |
| --- | --- |
| Pet is missing from the picker | Check the folder nesting, the app's `CODEX_HOME`, and that both required files exist. Refresh; if necessary reopen the app. |
| Image size/version error | Use an app version supporting v2 pets. Keep `spriteVersionNumber: 2` and the original 1536 × 2288 WebP; do not resize it. |
| Pet stays still | Check the operating system's reduced-motion setting. Idle movement is intentionally subtle. |
| Only a GIF is available | Download the pet ZIP. A preview GIF is not an installable spritesheet. |
| Pet does not appear on the web or another computer | Desktop custom pets are local and do not automatically sync. Install on each desktop computer. |

These are desktop v2 packages. The web uploader described in the current [official documentation](https://learn.chatgpt.com/docs/pets) accepts a different, 1536 × 1872 layout; these ZIPs are not web-upload packages. Installation has been checked on macOS; Windows copy instructions have not been tested in a Windows desktop session.

## 6. Understand or customize a package

Each pet's manifest identifies its image:

```json
{
  "id": "indigo-cat",
  "displayName": "Indigo · 靛蓝猫",
  "description": "A blue-violet pixel cat with a cyan terminal face.",
  "spriteVersionNumber": 2,
  "spritesheetPath": "spritesheet.webp"
}
```

The atlas uses 8 columns × 11 rows of 192 × 208 cells. Rows 0–8 contain idle, move right, move left, wave, jump, failure, waiting, working, and review. Rows 9–10 contain 16 clockwise look directions, starting at up and spaced by 22.5°. Preserve this layout when editing. Use a new folder name and matching `id` when creating a variant you want to keep alongside the original.

Before redistributing a variant, read [LICENSE](../LICENSE) and [CREDITS.md](../CREDITS.md), preserve the notices, and document your changes and any new references.
