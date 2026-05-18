# ResurgenceStation game config

Operator-owned game configuration. Synced into TGS `Configuration/GameStaticFiles/config/`
every PreCompile event by `update-config.sh` (lives in
[infrastructure/tgs/EventScripts/resurgencestation/update-config.sh](https://github.com/ResurgenceStation/infrastructure/blob/main/tgs/EventScripts/resurgencestation/update-config.sh)).

## Layout
- Top-level files: global defaults, included by every server.
- `owo/` — per-server overrides for the reduxstation.com instance. `update-config.sh` does
  `git sparse-checkout set owo/ title_screens/` then symlinks per-server files
  to the top of the active config dir.
- `title_screens/` — shared art (small enough to commit).

## Adding a new server
Create `<servername>/` subdir mirroring `owo/`. Update parse-server.sh in the
infrastructure repo to discriminate.

## What's NOT here
- **Secrets**: `comms.txt`, `dbconfig.txt`, `webhooks.txt`, `tts_secrets.txt` live on the
  host at `/etc/resurgence/secrets/*`. `update-config.sh` symlinks them in at sync time.
- **Large media**: `jukebox_music/`, `title_music/`, `reboot_themes/` live on the host at
  `Configuration/GameStaticFiles/config/<media>/`. Operator manages directly via scp.
