# Codex Repository Guide

## Project overview

Exile-UI is an AutoHotkey v1 overlay and quality-of-life toolkit for Path of Exile 1 and 2. `Exile UI.ahk` is the main entry point and includes the feature modules used by the overlay.

## Important directories

- `modules/`: AutoHotkey feature implementations. Most behavior changes belong here.
- `data/`: tracked static data, translations, defaults, and helper libraries. `data/announcements.json` is tracked, but the running app can refresh it automatically from the official repository.
- `img/`: tracked UI assets. Recognition captures and several feature-generated images are ignored by Git.
- `ini/` and `ini 2/`: ignored, machine-specific settings and runtime state. These may contain local paths, character/build information, and UI preferences; do not commit them.
- `exports/`: ignored user-generated exports; do not commit them by default.
- `cheat-sheets/` and `cheat-sheets 2/`: ignored user-created feature data; do not commit them by default.

## Editing guidance

- Preserve the existing AutoHotkey v1 style and CRLF line endings where practical.
- Read both staged and unstaged diffs before editing; a file may contain user work in both places.
- Never discard, reset, overwrite, or clean local changes unless the user explicitly authorizes the exact operation.
- Treat ignored runtime folders as private/machine-specific even when they are useful for local testing.
- Before committing `data/announcements.json`, check whether it was merely refreshed at runtime and whether its content already exists on `upstream/main`.

## Validation

There is no comprehensive automated test suite in this checkout. For AutoHotkey changes:

1. Run `git -c core.whitespace=cr-at-eol diff --check` and search changed files for unresolved conflict markers. The override prevents the repository's CRLF lines from being reported as trailing whitespace.
2. Parse every changed JSON file and inspect changed INI sections for duplicate or malformed entries.
3. Compile `Exile UI.ahk` with AutoHotkey v1's `Ahk2Exe.exe` and the v1 `AutoHotkeyU64.exe` base. The main script includes the modules, so this provides a useful whole-project syntax check.
4. Manually exercise affected overlays in Path of Exile when behavior depends on client logs, screen recognition, clipboard input, window dimensions, or game UI state. Compilation cannot validate those integrations.

## Git safety

- `origin` is the user's fork and is the normal push target.
- `upstream` is the original project. Never push to `upstream` without explicit permission for that specific push.
- Never force-push unless the user explicitly requests it after reviewing the risk.
- Fetch before reporting divergence, and keep unrelated changes in separate commits.
