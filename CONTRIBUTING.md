# Git & GitHub Guidelines

These rules keep the history clean, reduce merge conflicts and make collaboration easier.

---

## 1. Commit Messages

We use the [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>(<scope>): <short description>

[optional longer explanation]

[optional footer, e.g. Closes #12]
```

### Types

| Type       | Use for                                                        |
|------------|----------------------------------------------------------------|
| `feat`     | New feature (mechanic, enemy, UI screen...)                    |
| `fix`      | Bug fix                                                        |
| `refactor` | Code restructuring without changing behavior                  |
| `art`      | Graphics, sprites, animations, 3D models                       |
| `audio`    | Sound effects and music                                        |
| `level`    | Level design, tilemaps, scene layouts                          |
| `balance`  | Gameplay tuning: numbers, speeds, damage                       |
| `ui`       | Menus, HUD, fonts                                              |
| `perf`     | Performance improvement                                        |
| `docs`     | Documentation                                                  |
| `chore`    | Project settings, export presets, plugins                      |
| `test`     | Tests                                                          |

### Scope examples
`player`, `enemy`, `ui`, `audio`, `level1`, `save`, `input`, `camera`

### Good examples
```
feat(player): add double jump
fix(enemy): stop enemies getting stuck in walls
balance(player): lower dash cooldown from 1.2s to 0.8s
art(level1): add new parallax background layers
chore: upgrade Godot 4.3 to 4.4
```

### Bad examples
```
fixes
asdf
WIP
update
```

### Rules
- Subject line **max ~72 characters**, no trailing period.
- Use the imperative mood: *"add"*, not *"added"* or *"adds"*.
- **One logical change per commit.** Don't mix a bug fix with a new feature.
- Explain **why** in the body, not just what - the code already shows what.
- Reference issues: `Closes #23` or `Refs #23`.
- Commit often, but only working code: the game launches and doesn't crash.
- Put `project.godot` changes (input map, autoloads, settings) in their own `chore` commit.

---

## 2. Branches

```
main            always playable, release-ready
dev             integration branch for features (optional)
feature/...     new features
fix/...         bug fixes
art/...         larger art drops
exp/...         experiments, can be thrown away
```

**Naming:** lowercase with hyphens, ideally including the issue number:
```
feature/12-double-jump
fix/31-enemy-wall-stuck
exp/procedural-dungeon
```

### Rules
- **Never push directly to `main`.** All changes go through a Pull Request.
- Keep branches **short-lived** (a few days at most). Long branches mean big conflicts.
- Update your branch regularly: `git pull --rebase origin main`.
- Delete the branch after merging.

---

## 3. Pull Requests

### PR title
Same format as a commit message: `feat(player): add double jump`

### PR description (template)
```markdown
## What changed
-

## Why
-

## How to test
1. Open scene `res://scenes/...`
2. Press F6 / F5
3. ...

## Screenshot / GIF
(required for visual changes)

Closes #
```

### Rules
- Keep PRs **small and focused** - three small PRs beat one giant one.
- The game **launches and works** before you request a review.
- Always include a screenshot or GIF for visual changes.
- At least **1 approval** before merging (if there's more than one person on the team).

---

## 4. Merging

- Use **Squash and merge** to keep the `main` history clean.
- The squashed commit message follows the commit message format.
- Resolve conflicts in your own branch (rebase onto `main`), not in `main`.
- After resolving conflicts, open the game and check that the affected scenes still work.

### Avoiding scene conflicts
`.tscn` files are text, but their conflicts are painful to resolve.

- **One person edits a scene at a time.** Let the team know if you're working on a shared scene like `main.tscn`.
- Don't save a scene unnecessarily if you didn't change anything - Godot may shuffle IDs.
- Before committing, check `git status` and discard changes to scenes you didn't mean to touch.

---

## 5. Issues

### Bug report template
```markdown
**Description:**
**Steps to reproduce:**
1.
2.
**Expected behavior:**
**Actual behavior:**
**Godot version / platform:**
**Screenshot / video:**
```

### Labels
`bug`, `feature`, `art`, `audio`, `level`, `balance`, `ui`, `good first issue`, `priority: high`, `blocked`

---

## 6. Versions and Releases

We use [Semantic Versioning](https://semver.org/) `MAJOR.MINOR.PATCH`:
- `0.x.y` - development / prototype stage
- `MINOR` goes up when adding content or features
- `PATCH` goes up for bug fixes
- `1.0.0` - first official release

Releasing:
```bash
git tag -a v0.3.0 -m "v0.3.0: double jump and level 2"
git push origin v0.3.0
```
Create a GitHub **Release** from the tag and attach the builds (.zip) to it. **Don't commit builds to the repo.**

Also update the version in `project.godot` (`application/config/version`).

---

## 7. Don'ts

- No force pushing (`git push --force`) to shared branches. `--force-with-lease` on your own branch is fine.
- No passwords, API keys or keystores in the repo.
- No broken code in `main`.
- Don't edit other people's scenes without agreeing on it first.

---

## 8. Pre-Push Checklist

- [ ] The game launches without errors (check **Debugger > Errors**)
- [ ] Commit message follows the format
- [ ] No unwanted files (`git status`)
- [ ] No accidental changes to scenes you didn't touch
- [ ] Branch is up to date with `main`
