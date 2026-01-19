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
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[markdown]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.wordWrap": "off",
    "editor.wordWrapColumn": 80
  },
  "[php]": {
    "editor.defaultFormatter": "bmewburn.vscode-intelephense-client"
  },
  "[terraform]": {
    "editor.defaultFormatter": "hashicorp.terraform"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[xml]": {
    "editor.defaultFormatter": "DotJoshJohnson.xml"
  },
  "[yaml]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "diffEditor.ignoreTrimWhitespace": false,
  "editor.defaultFormatter": null,
  "editor.fontFamily": "'Operator Mono'",
  "editor.fontSize": 16,
  "editor.formatOnSave": true,
  "editor.renderWhitespace": "all",
  "editor.rulers": [72, 79],
  "editor.wordWrap": "off",
  "editor.wordWrapColumn": 80,
  "explorer.confirmDragAndDrop": false,
  "git.confirmSync": false,
  "terminal.integrated.fontFamily": "MesloLGS NF",
  "terminal.integrated.fontSize": 16,
  "window.commandCenter": true,
  "workbench.colorTheme": "Dracula Theme",
  "workbench.editor.enablePreview": false,
  "workbench.iconTheme": "material-icon-theme"
}
```

## extensions

show: `ls -1 /home/isaac/.cursor/extensions | sort`

```
anysphere.cursorpyright-1.0.10
bmewburn.vscode-intelephense-client-1.16.2-universal
dbaeumer.vscode-eslint-3.0.16-universal
deerawan.vscode-faker-2.0.0-universal
dotjoshjohnson.xml-2.5.1-universal
dracula-theme.theme-dracula-2.25.1-universal
eamodio.gitlens-17.7.1-universal
esbenp.prettier-vscode-11.0.2-universal
extensions.json
getpsalm.psalm-vscode-plugin-2.7.0-universal
hashicorp.terraform-2.37.6-linux-x64
mechatroner.rainbow-csv-3.3.0-universal
ms-python.debugpy-2025.14.1-linux-x64
ms-python.python-2025.6.1-linux-x64
oderwat.indent-rainbow-8.3.1-universal
pkief.material-icon-theme-5.29.0-universal
```
