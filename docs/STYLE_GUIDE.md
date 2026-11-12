# Style Guide

Folder structure and naming conventions for this project.

**Stack:** Godot 4.x · GDScript · ENet · GodotSteam

Git rules (commits, branches, PRs, releases) are in [CONTRIBUTING.md](CONTRIBUTING.md).

---

## 1. General Rules

- Use **English** for all names.
- Use **lowercase `snake_case`** for every file and folder name. No spaces, no capitals, no special characters, no `ä ö å`. (Godot is case-sensitive on export, and Windows/macOS hide the problem until then.)
- Names describe *what the thing is*, not *when it was made*: `player_idle.png`, not `new_final_v2.png`.
- A scene and its main script share a name and live in the same folder: `player.tscn` + `player.gd`.

---

## 2. Folder Structure Inside Godot (`res://`)

```
res://
├── addons/                  # third-party plugins only (godotsteam, gdUnit4...)
├── assets/                  # raw content, no scripts
│   ├── art/
│   │   ├── characters/
│   │   ├── environment/
│   │   ├── ui/
│   │   └── vfx/
│   ├── audio/
│   │   ├── music/
│   │   └── sfx/
│   ├── fonts/
│   └── shaders/
├── autoload/                # singletons: net, steam_manager, log...
├── net/                     # networking code not tied to a scene
├── scenes/                  # scenes with their scripts
│   ├── game/
│   ├── lobby/
│   ├── menus/
│   ├── player/
│   ├── enemies/
│   ├── levels/
│   └── ui/
├── resources/               # custom .tres files (items, stats, themes)
├── scripts/                 # shared scripts that belong to no scene
├── tests/
├── steam_appid.txt          # dev only
└── project.godot
```

### Rules

- **Group by feature, not by file type.** `scenes/player/` holds the player's `.tscn`, `.gd` and local sub-scenes together.
- Anything used by only one scene stays next to that scene. Anything shared goes to `assets/`, `resources/` or `scripts/`.
- Folder names are **plural** for collections (`enemies`, `levels`) and **singular** for a single thing (`player`, `lobby`).
- `addons/` is third-party only. Do not edit it except to update it.
- Do not put loose files in `res://` root, except `project.godot` and `steam_appid.txt`.
- Maximum nesting depth: about 4 levels.
- Folders that must not be imported (docs, source files) get an empty `.gdignore` file.

---

## 3. Naming Inside Godot

### 3.1 Files

| Thing | Convention | Example |
|---|---|---|
| Scene | `snake_case.tscn` | `main_menu.tscn` |
| Script | `snake_case.gd`, same as scene | `main_menu.gd` |
| Resource | `snake_case.tres` | `sword_stats.tres` |
| Shader | `snake_case.gdshader` | `dissolve.gdshader` |
| Autoload script | `snake_case.gd` | `steam_manager.gd` |
| Constants-only script | `snake_case.gd` | `net_channels.gd` |

### 3.2 Assets

Pattern: `<thing>_<variant>_<state>.<ext>`

| Type | Example |
|---|---|
| Sprite / texture | `player_idle.png`, `player_run_01.png` |
| Animation frames | numbered with two digits: `_01`, `_02` |
| Tileset | `tileset_forest.png` |
| UI icon | `icon_sword.png`, `icon_settings.png` |
| Music | `music_menu.ogg`, `music_level1.ogg` |
| Sound effect | `sfx_jump.wav`, `sfx_button_click.wav` |
| Font | `font_main_bold.ttf` |

Prefixes `icon_`, `music_`, `sfx_`, `font_`, `tileset_` make files easy to search.

### 3.3 Code

| Thing | Convention | Example |
|---|---|---|
| Class (`class_name`) | `PascalCase` | `PlayerController` |
| Function | `snake_case` | `spawn_player()` |
| Variable | `snake_case` | `max_health` |
| Private member | leading `_` | `_peer`, `_update_ui()` |
| Constant | `CONSTANT_CASE` | `MAX_PLAYERS` |
| Enum name | `PascalCase` | `enum State` |
| Enum value | `CONSTANT_CASE` | `IDLE`, `RUNNING` |
| Signal | `snake_case`, past tense | `player_joined`, `lobby_created` |
| Signal handler | `_on_<source>_<signal>` | `_on_start_button_pressed()` |
| Autoload name | `PascalCase` | `Net`, `SteamManager`, `Log` |
| Group | `snake_case` | `"enemies"`, `"players"` |
| Input action | `snake_case` | `move_left`, `jump`, `ui_confirm` |
| Collision layer | `PascalCase` name in project settings | `World`, `Player`, `Enemy` |

### 3.4 Nodes in a scene

- Node names are `PascalCase`: `PlayerSprite`, `HealthBar`, `HitboxArea`.
- The root node is named after the scene: `player.tscn` → `Player`.
- Name nodes by role, not type: `HealthBar`, not `ProgressBar2`.
- Nodes accessed from script get a **unique name** (`%HealthBar`).

### 3.5 Networking names

| Thing | Convention | Example |
|---|---|---|
| RPC, client asks server | `server_` prefix | `server_request_shoot()` |
| RPC, server tells clients | `client_` prefix | `client_spawn_bullet()` |
| RPC, symmetric | `rpc_` prefix | `rpc_chat_message()` |
| Network channel constant | `CHANNEL_<NAME>` | `CHANNEL_EVENTS`, `CHANNEL_STATE` |
| Replicated spawn scenes | in `scenes/`, suffix none | `bullet.tscn` |

### 3.6 Steam names

| Thing | Convention | Example |
|---|---|---|
| Steam wrapper autoload | `SteamManager` | only place that calls `Steam.*` |
| Lobby data key | string constant in `steam_keys.gd`, `snake_case` value | `KEY_GAME_VERSION = "game_version"` |
| Achievement ID | constant in `achievements.gd` | `Achievements.FIRST_WIN` |
| Game-level signals re-emitted by wrapper | past tense | `lobby_ready`, `member_joined` |

---

## 4. Naming Outside Godot (Repository)

### 4.1 Repository root

```
repo/
├── .github/                 # issue/PR templates, workflows
├── docs/                    # design docs, diagrams (kept outside res://)
├── source_art/              # .psd .kra .blend .aseprite (outside res://)
├── tools/                   # build and export scripts
├── builds/                  # local build output, git-ignored
├── godot_project/           # contains project.godot (if the repo is split)
├── .editorconfig
├── .gitattributes
├── .gitignore
├── CONTRIBUTING.md
├── LICENSE
├── README.md
└── STYLE_GUIDE.md
```

If `project.godot` sits directly in the repo root, drop `godot_project/` and keep the other folders as they are. Mark `docs/`, `source_art/` and `tools/` with `.gdignore` if they are inside the Godot project folder.

### 4.2 Repository files

| Thing | Convention | Example |
|---|---|---|
| Standard project docs | `UPPER_CASE.md` | `README.md`, `CONTRIBUTING.md`, `STYLE_GUIDE.md`, `LICENSE` |
| Other docs | `snake_case.md` | `docs/network_design.md` |
| Source art files | same name as the exported asset | `player_idle.aseprite` → `player_idle.png` |
| Scripts in `tools/` | `snake_case` with extension | `export_windows.sh` |
| Workflows | `kebab-case.yml` | `.github/workflows/lint.yml` |

The only exception to `snake_case` is the standard uppercase project docs and files that tools require to have a fixed name (`.gitignore`, `project.godot`).

### 4.3 Builds and releases

| Thing | Convention | Example |
|---|---|---|
| Git tag | `v<MAJOR>.<MINOR>.<PATCH>` | `v0.3.0` |
| Build archive | `<game>_<version>_<platform>.zip` | `mygame_0.3.0_windows.zip` |
| Export preset | `<Platform>` | `Windows`, `Linux`, `macOS` |

Builds go to GitHub Releases. Do not commit them.

### 4.4 Branches, commits, PRs, issue labels

All defined in [CONTRIBUTING.md](CONTRIBUTING.md). Branch names there are `lowercase-with-hyphens` with a type prefix (`feature/12-double-jump`).

---

## 5. Quick Reference

| Where | Style |
|---|---|
| Files and folders (everything) | `snake_case` |
| Classes, nodes, autoloads | `PascalCase` |
| Functions, variables, signals, actions | `snake_case` |
| Constants and enum values | `CONSTANT_CASE` |
| Private members | `_leading_underscore` |
| Standard repo docs | `UPPER_CASE.md` |
| Git branches | `type/short-name` |
| Git tags | `vMAJOR.MINOR.PATCH` |
