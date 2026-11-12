# eDEX-UI on an Apple Silicon MacBook

Upstream eDEX-UI was archived in 2021 (Electron 12, x64-only macOS build). This branch
(`macbook-apple-silicon`) makes it run natively on arm64 macOS.

## What changed
- Electron 12 -> 45 (native arm64, Metal rendering, current Chromium).
- node-pty 0.10 -> 1.1.0: N-API with a prebuilt `darwin-arm64` binary, so no Xcode/node-gyp build.
- `@electron/remote` 2.x and removal of the dropped `electron.remote` / `new-window` APIs.
- systeminformation updated (knows Apple M-series chips); Intel-only `osx-temperature-sensor` dropped.
- macOS defaults: your login shell (zsh) instead of bash, home directory as start folder.
- Foreground-process detection uses node-pty instead of GNU-only `ps` flags (tab titles now work on macOS).
- 3 system-info helper processes on macOS instead of 7.
- New: startup command (`EDEX_STARTUP_CMD` / `"startupCommand"` in settings.json), used by `edex nvim`.

## Use
- Double-click `eDEX-UI.app` (it can be dragged to the Dock; it must stay inside this folder).
- Or from any terminal: `bin/edex`, `bin/edex nvim`, `bin/edex nvim file.txt`.
- Quit: type `exit` in the main tab, or Cmd+Q.
- Settings: Ctrl+Shift+S inside eDEX, or `~/Library/Application Support/eDEX-UI/settings.json`
  (`"forceFullscreen": false` + `"allowWindowed": true` for a normal window).

## Reinstall dependencies
`npm run install-darwin` (needs Node 20+), then `chmod +x src/node_modules/node-pty/prebuilds/darwin-arm64/spawn-helper`.
