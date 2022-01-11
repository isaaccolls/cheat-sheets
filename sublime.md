<!-- MarkdownTOC autolink="true" levels="1,2" -->

- [short cuts](#short-cuts)
- [sublime projects location](#sublime-projects-location)
- [settings](#settings)
  - [settings for python syntax](#settings-for-python-syntax)
  - [settings for php syntax](#settings-for-php-syntax)
  - [key bindings](#key-bindings)
- [installed packages](#installed-packages)
  - [packages config](#packages-config)

<!-- /MarkdownTOC -->
# short cuts

- auto complete `alt + /`
- delete line `ctrl + shift + k`
- folding selected text `ctrl + shift + [`
- fold multiple blocks at once `ctrl + k, ctrl + 2`
- converting case `ctrl + k, ctrl u or l.`
- js_prettier `ctrl+alt+f`

# sublime projects location

- Mac OSX
` ~/Library/Application Support/Sublime Text 3/Local/Session.sublime_session`
- Linux
`~/.config/sublime-text-3/Local/Session.sublime_session`
  - Remove the unwanted project(s) from "recent_workspaces"

# settings

```json
{
  "always_show_minimap_viewport": true,
  "auto_complete": true,
  "auto_complete_commit_on_tab": true,
  "auto_complete_cycle": true,
  "auto_complete_triggers":
  [
    {
      "characters": "<",
      "selector": "text.html"
    },
    {
      "characters": ".",
      "selector": "source, text.html"
    },
    {
      "characters": ".",
      "selector": "source.js"
    },
    {
      "characters": ".",
      "selector": "source.py"
    }
  ],
  "auto_complete_with_fields": true,
  "bold_folder_labels": true,
  "caret_style": "phase",
  "color_scheme": "Packages/Material Theme/schemes/Material-Theme-Palenight.tmTheme",
  "detect_indentation": true,
  "draw_white_space": "all",
  "fade_fold_buttons": false,
  "font_face": "Operator Mono",
  "font_size": 12,
  "highlight_line": true,
  "ignored_packages":
  [
    "Vintage"
  ],
  "indent_guide_options":
  [
    "draw_normal",
    "draw_active"
  ],
  "preview_on_click": false,
  "rulers":
  [
    72,
    79
  ],
  "shift_tab_unindent": true,
  "show_encoding": true,
  "tab_size": 2,
  "theme": "Adaptive.sublime-theme",
  "translate_tabs_to_spaces": true,
  "word_wrap": "false"
}
```

## settings for python syntax

```json
{
  "tab_size": 4,
}
```

## settings for php syntax

```json
{
  "tab_size": 2,
}
```

## key bindings

```json
[
  { "keys": ["/"], "command": "close_tag", "args": { "insert_slash": true }, "context":
    [
      { "key": "selector", "operator": "equal", "operand": "(text.html, text.xml, meta.jsx.js) - string - comment", "match_all": true },
      { "key": "preceding_text", "operator": "regex_match", "operand": ".*<$", "match_all": true },
      { "key": "setting.auto_close_tags" }
    ]
  },
  { "keys": ["ctrl+alt+f"], "command": "js_prettier" }
]
```

# installed packages

- sublime
    - Side​Bar​Enhancements ✔️
    - Autofilename ✔️
    - TerminalView (dependency for JavaScript Enhancements) ✔️
- Markdown
    - MarkdownTOC ✔️
- json
    - Pretty JSON ✔️
- docker
    - Dockerfile Syntax Highlighting ✔️
- Nodejs
    - DotENV ✔️
- js
    - babel ✔️
    - JavaScript Enhancements ✔️
    - JsPrettier ✔️
      - `npm install --global prettier`
      - `npm install --global prettier @prettier/plugin-php`
- php
  - Apache​Conf ✔️
- python
    - anaconda ✔️

## packages config

### Java​Script Enhancements

```json
{
  "PATH": ":/home/isaac/.nvm/versions/node/v12.16.1/bin",
  "node_js_custom_path": "node",
  "npm_custom_path": "npm",
  "yarn_custom_path": "yarn",
  "debug_mode": false
}
```

### JsPrettier

```json
{
  "singleQuote": true,
  "prettier_cli_path": "/home/isaac/.nvm/versions/node/v12.16.1/lib/node_modules/prettier/bin-prettier.js",
  "node_path": "/home/isaac/.nvm/versions/node/v12.16.1/bin/node",
  "debug": true,
  "trailingComma": "all",
  "arrowParens": "avoid",
}
```
