# desktop entry

```sh
[Desktop Entry]
Version=1.0
Encoding=UTF-8
Type=Application
Terminal=false
Exec=/opt/cursor/Cursor-1.5.9-x86_64.AppImage --no-sandbox
Name=Cursor
Comment=Text Editor
Icon=/opt/cursor/app-logo.svg
Categories=TextEditor;Development;IDE;
```

# factory reset

remove:

- `~/.cursor`
- `~/.config/Cursor`

# Keyboard Shortcuts

- `Ctrl+I`: Toggle Sidepanel (unless bound to mode)
- `tab`: Accept suggestion
- `Ctrl+K`: Open terminal prompt bar

# preferences

1. Open _Command Palette_: `Ctrl + Shift + P`
1. write: `Preferences: Open Settings (JSON)`

last settings:

```json
{
  "window.commandCenter": true,
  "workbench.colorTheme": "Dracula Theme",
  "editor.fontSize": 16,
  "terminal.integrated.fontSize": 16,
  "terminal.integrated.fontFamily": "MesloLGS NF",
  "editor.fontFamily": "'Operator Mono'"
}
```

## extensions

show: `ls -1 /home/isaac/.cursor/extensions | sort`

```
dracula-theme.theme-dracula-2.25.1-universal
```
