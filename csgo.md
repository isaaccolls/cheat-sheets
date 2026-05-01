- [enable console](#enable-console)
- [configs](#configs)
- [video](#video)
  - [mouse](#mouse)
  - [commands](#commands)
  - [launch options](#launch-options)
    - [autoexec.cfg (CS:GO / CS2)](#autoexeccfg-csgo--cs2)
- [1.6](#16)
- [display](#display)
  - [crosshair](#crosshair)
    - [userconfig.cfg](#userconfigcfg)

# enable console

- settings + game + enable developer console (`~`)

# configs

# video

- display mode: _fullscreen_

## mouse

- mouse acceleration: off
- [crosshair](https://tools.dathost.net)
  - `cl_crosshairalpha "200";cl_crosshaircolor "1";cl_crosshaircolor_b "50";cl_crosshaircolor_r "50";cl_crosshaircolor_g "250";cl_crosshairdot "0";cl_crosshairgap "0";cl_crosshairsize "5";cl_crosshairstyle "4";cl_crosshairusealpha "1";cl_crosshairthickness "1.5";cl_fixedcrosshairgap "0";cl_crosshair_outlinethickness "0";cl_crosshair_drawoutline "0";`

## commands

- show fps: (in game) `cl_showfps 1`
- show fps and net: `net_graph 1` on Valve MM (max allowed); `net_graph 3` often works offline/bots 👈
- show mouse sensitivity: `sensitivity`
- set mouse sensitivity: `sensitivity 2.5`
- off menu music: `snd_menumusic_volume 0`
- centerd radar: `cl_radar_always_centered 1`

## launch options

`-novid -high -fullscreen -exec autoexec`

To load the autoexec on launch, add `-exec autoexec` (or `+exec autoexec`).

### autoexec.cfg (CS:GO / CS2)

Use `autoexec.cfg` in the **`cfg` folder of the build you actually launch**. Steam ships two installs: **Counter-Strike 2** and **CS:GO Legacy**; they do **not** share the same `cfg` path.

- **CS2:** `~/.local/share/Steam/steamapps/common/Counter-Strike Global Offensive/game/csgo/cfg/autoexec.cfg`
- **CS:GO Legacy** : `~/.local/share/Steam/steamapps/common/csgo legacy/csgo/cfg/autoexec.cfg` 👈

Legacy still runs `exec autoexec.cfg` from `valve.rc` when that file exists in **`csgo legacy/csgo/cfg`**. If you only create it under CS2, Legacy never loads it.

Keep **`-exec autoexec`** (or `+exec autoexec`) in launch options if you want a guaranteed run on startup.

**It did load:** if the console prints your `echo` lines (e.g. `loading autoexec...`), the file ran. Lines like **`Server does not allow net_graph values above 1`** or **`Server does not allow developer values above 0`** mean Valve (or similar) **clamped or rejected** those cvars after connect—they are not proof the autoexec failed.

- **`net_graph`:** on official matchmaking, **`1`** is usually the max; **`3`** works more on local/offline.
- **`developer 1`:** often forced back to **`0`** on official servers.

```cfg
// === autoexec.cfg CS:GO ===
// developer 1 — fine offline; Valve MM resets to 0 (console spam)
developer 0
echo "loading autoexec...🚀"

// Mouse: disable acceleration in OS (no cvar in CS:GO)
// Crosshair
cl_crosshairalpha "255"
cl_crosshaircolor "4"
cl_crosshaircolor_b "50"
cl_crosshaircolor_r "50"
cl_crosshaircolor_g "250"
cl_crosshairdot "1"
cl_crosshairgap "0"
cl_crosshairsize "5"
cl_crosshairstyle "5"
cl_crosshairusealpha "1"
cl_crosshairthickness "1.5"
cl_fixedcrosshairgap "0"
cl_crosshair_outlinethickness "0"
cl_crosshair_drawoutline "0"

// FPS and net (net_graph 3 only where allowed; MM uses 1)
cl_showfps 1
net_graph 1

// Sensitivity
sensitivity 2.5

// Menu music off
snd_menumusic_volume 0

// Centered radar
cl_radar_always_centered 1

echo "autoexec loaded.🔥"
```

# 1.6

# display

- show fps and net: `net_graph 3`

## crosshair

- color: `cl_crosshair_color "255 0 255"`
- size: `cl_crosshair_size small`
- controls transparency: `cl_crosshair_translucent 0`

#### userconfig.cfg

create file `userconfig.cfg` on `/home/isaac/.local/share/Steam/steamapps/common/Half-Life/cstrike/` with content:

```sh
developer 1
echo "starting to load userconfig..."
// Crosshair configuration
cl_crosshair_color "255 0 255"
cl_crosshair_size "small"
cl_crosshair_translucent "0"
cl_dynamiccrosshair "0"
// show fps
net_graph 3
echo "userconfig loaded successfully!!"
```

made it executable by running: `chmod +x userconfig.cfg`
