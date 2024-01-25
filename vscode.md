- [short cuts](#short-cuts)
- [settings](#settings)

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
- show integrated terminal `` ctrl + \`  ``
- find `ctrl + f` replace `ctrl + h`
- markdown preview `ctrl + shift + v`
- split editor `ctrl+\`
  - focus into n `ctrl+ 1 / 2 / 3`

# settings

```json
{
  "workbench.colorTheme": "Dracula",
  "workbench.editor.enablePreviewFromQuickOpen": false,
  "workbench.editor.enablePreview": false,
  "workbench.editorAssociations": {
    "*.ipynb": "jupyter-notebook",
    "git-rebase-todo": "gitlens.rebase"
  },
  "workbench.colorCustomizations": {},
  "workbench.iconTheme": "vscode-icons",
  "editor.fontFamily": "'Operator Mono'",
  "editor.fontSize": 16,
  "editor.renderWhitespace": "all",
  "editor.minimap.enabled": false,
  "editor.rulers": [72, 79],
  "editor.accessibilitySupport": "off",
  "editor.tabSize": 2,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "editor.rename.enablePreview": false,
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": "active",
  "editor.wordWrap": "off",
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
    "typescriptreact"
  ],
  "notebook.cellToolbarLocation": {
    "default": "right",
    "jupyter-notebook": "left"
  },
  "python.defaultInterpreterPath": "/usr/bin/python3",
  "markdown.extension.toc.levels": "1..2",
  "security.workspace.trust.untrustedFiles": "open",
  "php-cs-fixer.executablePath": "${extensionPath}/php-cs-fixer.phar",
  "php-cs-fixer.lastDownload": 1704933751917,
  "sonarlint.ls.javaHome": "/usr/lib/jvm/jdk-21-oracle-x64",
  "opa.path": "/home/isaac/opa",
  "diffEditor.ignoreTrimWhitespace": false,
  "[html]": {
    "editor.defaultFormatter": "vscode.html-language-features"
  },
  "[markdown]": {
    "editor.wordWrapColumn": 80,
    "editor.wordWrap": "off",
    "editor.quickSuggestions": {
      "comments": "off",
      "strings": "off",
      "other": "off"
    },
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[python]": {
    "editor.defaultFormatter": "ms-python.autopep8"
  },
  "[json]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[jsonc]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[javascriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[typescriptreact]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[nginx]": {
    "editor.defaultFormatter": "raynigon.nginx-formatter"
  },
  "[dockerfile]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  },
  "[php]": {
    "editor.defaultFormatter": "bmewburn.vscode-intelephense-client"
  },
  "[sql]": {
    "editor.wordWrap": "off"
  },
  "[yaml]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "files.associations": {
    "*.yml": "yaml"
  },
  "[terraform]": {
    "editor.defaultFormatter": "hashicorp.terraform"
  },
  "[dotenv]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  },
  "[shellscript]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  },
  "[ignore]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  }
}
```
