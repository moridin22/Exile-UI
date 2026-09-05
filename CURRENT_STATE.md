# Exile-UI Local State

Last audited: 2026-09-05

## Repository

- Local branch: `main`
- Personal remote (`origin`): <https://github.com/moridin22/Exile-UI>
- Original project remote (`upstream`): <https://github.com/Lailloken/Exile-UI>
- Before the backup commits, `main` was 60 commits ahead of `origin/main` and 223 commits behind the freshly fetched `upstream/main`.
- One saved Git stash exists: `stash@{0}: autostash`. It has not been dropped or reapplied. It contains an older copy of the interlude-order edit plus official/runtime data changes.

## Local Changes

### PoE 2 interlude order

File: `modules/leveling tracker.ahk`

- The displayed and internal interlude sequence has been reversed from `1-2-3` to `3-2-1`.
- The guide editor labels now follow the same `III-II-I` order.
- This mapping also makes the final King's March / Hooded One step display as Interlude 1 rather than Interlude 3.
- This is intentional source work and should be retained in branch history.

### PoE 1 skill-gem purchase display

File: `modules/leveling tracker.ahk`

- The existing gem-shop regex generation and clipboard behavior are unchanged.
- When a guide step contains generated `buy gem:` entries, the guide now displays each gem's readable name.
- Each displayed gem includes its Path of Building loadout name in parentheses, for example `Faster Attacks Support (Early Maps)`.
- A gem present in multiple loadouts lists each unique loadout once.
- This is intentional source work and should be retained in branch history.

### 2088-pixel vertical resolution

File: `data/Resolutions.ini`

- Added a `[2088p]` resolution profile with game-screen coordinates `13,70` and font size `20`.
- This should prevent the unsupported-resolution shutdown path for a 2088-pixel PoE client area.
- The height likely comes from a 2160p display minus a 72-pixel taskbar or other reserved desktop space.
- On first use, Exile-UI may create `img/Recognition (2088p)`. Image-based checks may still need calibration at this client height.
- This profile is local-project compatibility data, not a credential or private machine path, and should be retained in branch history.

### Announcements data

File: `data/announcements.json`

- The app automatically refreshed this tracked file with newer Allflame league announcement text.
- The refreshed file's content hash exactly matched `upstream/main` at audit time.
- It is generated/runtime-refreshed data and is deliberately excluded from the local feature commits. Its presence may leave the working tree dirty until a future upstream merge makes the branch version identical.

## Behavior Notes

### Area tracking

- The act tracker primarily follows area transitions reported in Path of Exile's client log.
- It compares the detected area against guide steps and advances when it finds the expected matching destination or trigger.
- Going out of order does not necessarily break tracking permanently: entering a later recognizable guide area can allow it to catch up.
- Recovery depends on the guide having an unambiguous area or trigger to match. Repeated area names, optional detours, unusual waypoint travel, and steps driven by manual interactions can require manual correction.

### Closing Path of Exile

- Exile-UI can be configured to terminate when the PoE process closes; disabling that setting should keep it running.
- If it still exits, confirm that the running script is this checkout rather than another installed copy, and check whether another launcher or wrapper is managing its lifetime.

### Updates

- Exile-UI has its own release updater and an optional automatic update check in the updater settings.
- That updater downloads official packaged releases; it is separate from Git and does not merge local source edits.
- To bring original-project Git changes into this clone, fetch or pull from `upstream`, then merge into `main` and resolve any overlap with these local changes.

## Verification Still Recommended

Completed during the 2026-09-05 backup:

- The full `Exile UI.ahk` entry point compiled successfully with AutoHotkey v1.1.37.02 and the 64-bit v1 base.
- All repository JSON files parsed successfully.
- The resolution file had unique sections and a complete `[2088p]` entry.
- CRLF-aware Git whitespace checks passed, and no unresolved conflict markers were found.

Manual checks still recommended:

- Start Exile-UI with PoE reporting a 2088-pixel client height and confirm there is no unsupported-resolution shutdown.
- Open a PoE 1 gem-purchase step and confirm gem names and loadout labels fit in the guide window.
- Confirm clicking the gem-purchase prompt still pastes the same regex into the vendor search field.
- Run through the PoE 2 interludes and confirm the tracker and guide editor both show `3`, `2`, `1`, including the final King's March step.
- Keep `data/announcements.json` out of feature commits unless it is intentionally being updated as release data.
- Review `stash@{0}` separately before ever applying or dropping it; much of it is redundant or runtime-generated, but it has intentionally been preserved.
