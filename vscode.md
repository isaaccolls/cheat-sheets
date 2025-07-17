- [short cuts](#short-cuts)
- [settings](#settings)
- [extensions](#extensions)

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
  "workbench.colorTheme": "Dracula Theme",
  "workbench.editor.enablePreviewFromQuickOpen": false,
  "workbench.editor.enablePreview": false,
  "workbench.editorAssociations": {
    "*.copilotmd": "vscode.markdown.preview.editor",
    "*.ipynb": "jupyter-notebook",
    "git-rebase-todo": "gitlens.rebase",
    "*.sql": "default"
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
  "php-cs-fixer.lastDownload": 1750807991304,
  "sonarlint.ls.javaHome": "/usr/lib/jvm/jdk-21-oracle-x64",
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
    "editor.defaultFormatter": "ms-python.autopep8",
    "diffEditor.ignoreTrimWhitespace": true
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
    "editor.wordWrap": "off",
    "editor.defaultFormatter": "bradymholt.pgformatter"
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
  },
  "[dbml]": {
    "editor.defaultFormatter": "matt-meyers.vscode-dbml"
  },
  "hediet.vscode-drawio.resizeImages": null,
  "diffEditor.ignoreTrimWhitespace": false,
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": false,
    "scminput": false
  },
  "[properties]": {
    "editor.defaultFormatter": "foxundermoon.shell-format"
  },
  "github.copilot.editor.enableAutoCompletions": true,
  "diffEditor.hideUnchangedRegions.enabled": true,
  "[c]": {
    "editor.defaultFormatter": "ms-vscode.cpptools"
  },
  "chat.instructionsFilesLocations": {
    ".github/instructions": true,
    "/tmp/postman-http-request-post-response.instructions.md": true,
    "/tmp/postman-http-request-pre-request.instructions.md": true,
    "/tmp/postman-collections-post-response.instructions.md": true,
    "/tmp/postman-collections-pre-request.instructions.md": true,
    "/tmp/postman-folder-post-response.instructions.md": true,
    "/tmp/postman-folder-pre-request.instructions.md": true
  }
}
```

# extensions

backup: `code --list-extensions | xargs -L 1 echo code --install-extension`

```sh
code --list-extensions | xargs -L 1 echo code --install-extension
code --install-extension adpyke.codesnap
code --install-extension ahmadalli.vscode-nginx-conf
code --install-extension astro-build.astro-vscode
code --install-extension atdushi.conky
code --install-extension bmewburn.vscode-intelephense-client
code --install-extension bradymholt.pgformatter
code --install-extension codestream.codestream
code --install-extension dbaeumer.vscode-eslint
code --install-extension deerawan.vscode-faker
code --install-extension docker.docker
code --install-extension dracula-theme.theme-dracula
code --install-extension eamodio.gitlens
code --install-extension esbenp.prettier-vscode
code --install-extension firsttris.vscode-jest-runner
code --install-extension foxundermoon.shell-format
code --install-extension genieai.chatgpt-vscode
code --install-extension getpsalm.psalm-vscode-plugin
code --install-extension gitduck.code-streaming
code --install-extension github.copilot
code --install-extension github.copilot-chat
code --install-extension github.vscode-github-actions
code --install-extension hashicorp.terraform
code --install-extension hediet.vscode-drawio
code --install-extension humao.rest-client
code --install-extension junstyle.php-cs-fixer
code --install-extension matt-meyers.vscode-dbml
code --install-extension mechatroner.rainbow-csv
code --install-extension mikestead.dotenv
code --install-extension mintlify.document
code --install-extension mrmlnc.vscode-apache
code --install-extension ms-azuretools.vscode-containers
code --install-extension ms-azuretools.vscode-docker
code --install-extension ms-kubernetes-tools.vscode-kubernetes-tools
code --install-extension ms-python.autopep8
code --install-extension ms-python.debugpy
code --install-extension ms-python.isort
code --install-extension ms-python.python
code --install-extension ms-python.vscode-pylance
code --install-extension ms-toolsai.jupyter
code --install-extension ms-toolsai.jupyter-keymap
code --install-extension ms-toolsai.jupyter-renderers
code --install-extension ms-toolsai.vscode-jupyter-cell-tags
code --install-extension ms-toolsai.vscode-jupyter-slideshow
code --install-extension ms-vscode-remote.remote-containers
code --install-extension ms-vscode-remote.remote-ssh-edit
code --install-extension ms-vscode.cmake-tools
code --install-extension ms-vscode.cpptools
code --install-extension ms-vscode.cpptools-extension-pack
code --install-extension ms-vscode.cpptools-themes
code --install-extension ms-vscode.makefile-tools
code --install-extension ms-vscode.vscode-speech
code --install-extension mtxr.sqltools
code --install-extension nhoizey.gremlins
code --install-extension nicolas-liger.dbml-viewer
code --install-extension nrwl.angular-console
code --install-extension octref.vetur
code --install-extension oderwat.indent-rainbow
code --install-extension perkovec.emoji
code --install-extension postman.postman-for-vscode
code --install-extension raynigon.nginx-formatter
code --install-extension redhat.vscode-yaml
code --install-extension sonarsource.sonarlint-vscode
code --install-extension tobermory.es6-string-html
code --install-extension tsandall.opa
code --install-extension unifiedjs.vscode-mdx
code --install-extension vscode-icons-team.vscode-icons
code --install-extension yzane.markdown-pdf
code --install-extension yzhang.markdown-all-in-one
```
