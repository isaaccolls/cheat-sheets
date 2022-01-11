- [short cuts](#short-cuts)
- [btw my settings.json](#btw-my-settingsjson)

# short cuts

- command palette `ctrl + shift + p`
- multi-cursor editing

  - add a cursor `shift + alt + up/down`
  - add cursor anywhere `alt + click`
  - cursors on all occurrences of a string `ctrl + shift + l`
  - insert cursor at end of each line selected `shift+alt+i`

- intellisense

  - trigger suggestion `ctrl + space`
  - trigger parameter hints `ctrl + shift + space`
  - go to definition `f12`
  - show references `shift+f12`

- line actions

  - move a entire line or selection `alt + up/down`
  - delete entire line `ctrl + shift + k`
  - comment block of code `ctrl + /`
  - delete line `ctrl+shift+k`

- formatting `ctrl + shift + i`

- code folding `ctrl + k + ctrl + 0` `ctrl + k + ctrl + 1` ... to unfold `ctrl + k + ctrl + j`

- errors and warnnings navigate `f8`

- custom

  - icons `file icon theme`

- show integrated terminal `ctrl + 😉`

- find `ctrl + f` replace `ctrl + h`

- markdown preview `ctrl + shift + v`

- split editor `ctrl+\`

  - focus into n `ctrl+ 1 / 2 / 3`

# btw my settings.json

```json
{
  "workbench.iconTheme": "material-icon-theme",
  "workbench.colorTheme": "Dracula",
  "workbench.editor.enablePreviewFromQuickOpen": false,
  "workbench.editor.enablePreview": false,
  "workbench.editorAssociations": {
    "*.ipynb": "jupyter-notebook"
  },
  "editor.fontFamily": "'Operator Mono'",
  "editor.fontSize": 17,
  "editor.renderWhitespace": "all",
  "editor.minimap.enabled": false,
  "editor.rulers": [
    72,
    79
  ],
  "editor.accessibilitySupport": "off",
  "editor.tabSize": 2,
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "editor.rename.enablePreview": false,
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": "active",
  "terminal.integrated.fontFamily": "MesloLGS NF",
  "terminal.integrated.fontWeightBold": "normal",
  "terminal.integrated.fontSize": 14,
  "terminal.integrated.tabs.enabled": true,
  "terminal.integrated.defaultProfile.linux": "zsh",
  "git.confirmSync": false,
  "git.suggestSmartCommit": false,
  "explorer.confirmDelete": false,
  "explorer.confirmDragAndDrop": false,
  "eslint.format.enable": true,
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact",
  ],
  "eslint.alwaysShowStatus": true,
  "redhat.telemetry.enabled": false,
  "notebook.cellToolbarLocation": {
    "default": "right",
    "jupyter-notebook": "left"
  },
  "python.defaultInterpreterPath": "/usr/bin/python3",
  "python.pythonPath": "/usr/bin/python3",
  "diffEditor.ignoreTrimWhitespace": false,
  "markdown.extension.toc.levels": "1..1",
  "[html]": {
    "editor.defaultFormatter": "vscode.html-language-features"
  },
  "[markdown]": {
    "editor.wordWrapColumn": 80,
    "editor.wordWrap": "off",
    "editor.quickSuggestions": false,
    "editor.defaultFormatter": "tehnix.vscode-tidymarkdown"
  },
  "[python]": {
    "editor.defaultFormatter": "ms-python.python"
  },
  "[json]": {
    "editor.defaultFormatter": "vscode.json-language-features"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "vscode.json-language-features"
  },
  "[javascript]": {
    "editor.defaultFormatter": "dbaeumer.vscode-eslint"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "dbaeumer.vscode-eslint"
  },
  "[typescript]": {
    "editor.defaultFormatter": "vscode.typescript-language-features"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "dbaeumer.vscode-eslint"
  },
  "[nginx]": {
    "editor.defaultFormatter": "raynigon.nginx-formatter"
  },
  "[dockerfile]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  },
  "files.associations": {
    "*.yml": "yaml"
  },
  "security.workspace.trust.untrustedFiles": "open",
  "sonarlint.ls.javaHome": "/home/isaac/.vscode/extensions/sonarsource.sonarlint_managed-jre/jre/jdk-11.0.13+8-jre"
}
```
