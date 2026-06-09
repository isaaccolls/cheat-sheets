- [short cuts](#short-cuts)
- [settings](#settings)
- [extensions](#extensions)
  - [ENABLED](#enabled)
  - [DISABLED](#disabled)

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
- show integrated terminal ``ctrl + \` ``
- find `ctrl + f` replace `ctrl + h`
- markdown preview `ctrl + shift + v`
- split editor `ctrl+\`
  - focus into n `ctrl+ 1 / 2 / 3`

# settings

```json
{
  "[c]": {
    "editor.defaultFormatter": "ms-vscode.cpptools"
  },
  "[dbml]": {
    "editor.defaultFormatter": "matt-meyers.vscode-dbml"
  },
  "[dockerfile]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  },
  "[dotenv]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  },
  "[html]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "[ignore]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
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
  "[nginx]": {
    "editor.defaultFormatter": "raynigon.nginx-formatter"
  },
  "[php]": {
    "editor.defaultFormatter": "bmewburn.vscode-intelephense-client"
  },
  "[properties]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  },
  "[python]": {
    "diffEditor.ignoreTrimWhitespace": true,
    "editor.defaultFormatter": "ms-python.autopep8"
  },
  "[shellscript]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  },
  "[sql]": {
    "editor.defaultFormatter": "bradymholt.pgformatter",
    "editor.wordWrap": "off"
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
  "chat.instructionsFilesLocations": {
    "../../../../tmp/postman-collections-post-response.instructions.md": true,
    "../../../../tmp/postman-collections-pre-request.instructions.md": true,
    "../../../../tmp/postman-folder-post-response.instructions.md": true,
    "../../../../tmp/postman-folder-pre-request.instructions.md": true,
    "../../../../tmp/postman-http-request-post-response.instructions.md": true,
    "../../../../tmp/postman-http-request-pre-request.instructions.md": true,
    ".claude/rules": true,
    ".github/instructions": true,
    "~/.claude/rules": true,
    "~/.copilot/instructions": true
  },
  "claudeCode.preferredLocation": "panel",
  "diffEditor.hideUnchangedRegions.enabled": true,
  "diffEditor.ignoreTrimWhitespace": false,
  "editor.accessibilitySupport": "off",
  "editor.bracketPairColorization.enabled": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": "explicit"
  },
  "editor.defaultFormatter": null,
  "editor.fontFamily": "'Operator Mono'",
  "editor.fontSize": 16,
  "editor.formatOnSave": true,
  "editor.guides.bracketPairs": "active",
  "editor.minimap.enabled": false,
  "editor.rename.enablePreview": false,
  "editor.renderWhitespace": "all",
  "editor.rulers": [72, 79],
  "editor.tabSize": 2,
  "editor.wordWrap": "off",
  "editor.wordWrapColumn": 80,
  "eslint.format.enable": true,
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ],
  "explorer.confirmDelete": false,
  "explorer.confirmDragAndDrop": false,
  "files.associations": {
    "*.yml": "yaml"
  },
  "git.confirmSync": false,
  "git.suggestSmartCommit": false,
  "github.copilot.enable": {
    "*": true,
    "markdown": false,
    "plaintext": false,
    "scminput": false
  },
  "github.copilot.nextEditSuggestions.enabled": true,
  "hediet.vscode-drawio.resizeImages": null,
  "markdown.extension.toc.levels": "1..2",
  "notebook.cellToolbarLocation": {
    "default": "right",
    "jupyter-notebook": "left"
  },
  "php-cs-fixer.executablePath": "${extensionPath}/php-cs-fixer.phar",
  "php-cs-fixer.lastDownload": 1753841651255,
  "python.defaultInterpreterPath": "/usr/bin/python3",
  "security.workspace.trust.untrustedFiles": "open",
  "terminal.integrated.defaultProfile.linux": "zsh",
  "terminal.integrated.fontFamily": "MesloLGS NF",
  "terminal.integrated.fontSize": 16,
  "terminal.integrated.fontWeightBold": "normal",
  "terminal.integrated.tabs.enabled": true,
  "window.commandCenter": true,
  "window.zoomLevel": 0,
  "workbench.colorCustomizations": {},
  "workbench.colorTheme": "Dracula Theme",
  "workbench.editor.enablePreview": false,
  "workbench.editor.enablePreviewFromQuickOpen": false,
  "workbench.editorAssociations": {
    "*.copilotmd": "vscode.markdown.preview.editor",
    "*.ipynb": "jupyter-notebook",
    "*.sql": "default",
    "git-rebase-todo": "gitlens.rebase"
  },
  "workbench.iconTheme": "material-icon-theme"
}
```

# extensions

## ENABLED

- adpyke.codesnap
- ahmadalli.vscode-nginx-conf
- anthropic.claude-code
- astro-build.astro-vscode
- atdushi.conky
- bmewburn.vscode-intelephense-client
- bradymholt.pgformatter
- dbaeumer.vscode-eslint
- deerawan.vscode-faker
- docker.docker
- dotjoshjohnson.xml
- dracula-theme.theme-dracula
- eamodio.gitlens
- esbenp.prettier-vscode
- firsttris.vscode-jest-runner
- foxundermoon.shell-format
- github.vscode-github-actions
- hashicorp.terraform
- hediet.vscode-drawio
- junstyle.php-cs-fixer
- matt-meyers.vscode-dbml
- mechatroner.rainbow-csv
- mikestead.dotenv
- mrmlnc.vscode-apache
- ms-azuretools.vscode-containers
- ms-azuretools.vscode-docker
- ms-kubernetes-tools.vscode-kubernetes-tools
- ms-python.autopep8
- ms-python.debugpy
- ms-python.isort
- ms-python.python
- ms-python.vscode-pylance
- ms-python.vscode-python-envs
- ms-toolsai.jupyter
- ms-toolsai.jupyter-keymap
- ms-toolsai.jupyter-renderers
- ms-toolsai.vscode-jupyter-cell-tags
- ms-toolsai.vscode-jupyter-slideshow
- ms-vscode.cmake-tools
- ms-vscode.cpp-devtools
- ms-vscode.cpptools
- ms-vscode.cpptools-extension-pack
- ms-vscode.cpptools-themes
- ms-vscode.makefile-tools
- ms-vscode.vscode-speech
- nhoizey.gremlins
- nicolas-liger.dbml-viewer
- octref.vetur
- pkief.material-icon-theme
- raynigon.nginx-formatter
- tobermory.es6-string-html
- vscode-icons-team.vscode-icons
- yzhang.markdown-all-in-one

## DISABLED

- codestream.codestream
- genieai.chatgpt-vscode
- getpsalm.psalm-vscode-plugin
- gitduck.code-streaming
- humao.rest-client
- mintlify.document
- ms-vscode-remote.remote-containers
- ms-vscode-remote.remote-ssh-edit
- mtxr.sqltools
- nrwl.angular-console
- oderwat.indent-rainbow
- perkovec.emoji
- postman.postman-for-vscode
- redhat.vscode-yaml
- sonarsource.sonarlint-vscode
- tsandall.opa
- unifiedjs.vscode-mdx
- yzane.markdown-pdf
