- [enable console](#enable-console)
- [configs](#configs)
- [video](#video)
  - [mouse](#mouse)
  - [commands](#commands)
  - [launch options](#launch-options)
- [1.6](#16)
- [display](#display)
  - [crosshair](#crosshair)

# enable console

- settings + game + enable developer console (`~`)

# configs

# video

- display mode: _fullscreen_

## mouse

- mouse acceleration: off
- [crosshair](https://tools.dathost.net)
  - `ccl_crosshairalpha "200";cl_crosshaircolor "1";cl_crosshaircolor_b "50";cl_crosshaircolor_r "50";cl_crosshaircolor_g "250";cl_crosshairdot "0";cl_crosshairgap "0";cl_crosshairsize "5";cl_crosshairstyle "4";cl_crosshairusealpha "1";cl_crosshairthickness "1.5";cl_fixedcrosshairgap "0";cl_crosshair_outlinethickness "0";cl_crosshair_drawoutline "0";`

## commands

- show fps: (in game) `cl_showfps 1` 👈
- show fps and net: `net_graph 1`
- show mouse sensitivity: `sensitivity`
- set mouse sensitivity: `sensitivity 2.5`
- off menu music: `snd_menumusic_volume 0`
- centerd radar: `cl_radar_always_centered 1`

## launch options

`-novid -high -fullscreen`

# 1.6

# display

- show fps and net: `net_graph 3`

## crosshair

- color: `cl_crosshair_color "255 0 255"`
- size: `cl_crosshair_size small`
- controls transparency: `cl_crosshair_translucent 0`

#### userconfig.cfg

create file `/home/isaac/.local/share/Steam/steamapps/common/Half-Life/cstrike/` with the commands:

```
developer 1
echo "starting to load userconfig..."
// Crosshair configuration
cl_crosshair_color "255 0 255"
cl_crosshair_size "small"
cl_crosshair_translucent "0"
cl_dynamiccrosshair "0"
echo "userconfig loaded successfully!!"
```

made it executable by running: `chmod +x userconfig.cfg`
