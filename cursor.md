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

# References

- Use `@Past Chats` to reference previous work in new conversations rather than copy-pasting entire discussions.
- Files: `@auth.ts` to include a specific file
- Folders: `@src/components/` to include an entire folder (type `/` after selecting to navigate deeper)
- Use slash `/` for running some custom agents
- `@Browser` to work with browser tab

# Subagents

Create subagents manually by adding markdown files to .cursor/agents/ (project) or ~/.cursor/agents/ (user).

```md
Create a subagent file at `.cursor/agents/verifier.md` with YAML frontmatter (name, description) followed by the prompt. The verifier subagent should validate completed work, check that implementations are functional, run tests, and report what passed vs what's incomplete.
```

```md
Create a subagent file at `.cursor/agents/security-reviewer.md` with YAML frontmatter containing name and description. The security-reviewer subagent should check code for common vulnerabilities like injection, XSS, and hardcoded secrets.
```

## File format

Each subagent is a markdown file with YAML frontmatter:

```md
---
name: security-auditor
description: Security specialist. Use when implementing auth, payments, or handling sensitive data.
model: inherit
---

You are a security expert auditing code for vulnerabilities.

When invoked:

1. Identify security-sensitive code paths
2. Check for common vulnerabilities (injection, XSS, auth bypass)
3. Verify secrets are not hardcoded
4. Review input validation and sanitization

Report findings by severity:

- Critical (must fix before deploy)
- High (fix soon)
- Medium (address when possible)
```

## Configuration fields

- name: Unique identifier. Use lowercase letters and hyphens. Defaults to **filename without extension**.
- description: When to use this subagent. Agent reads this to decide delegation.
- model: Model to use: `fast`, `inherit`, or a specific model ID. Defaults to `inherit`.

## Using subagents

### Automatic delegation

Include phrases like "use proactively" or "always use for" in your description field to encourage automatic delegation.

### Explicit invocation

Request a specific subagent by using the `/name` syntax in your prompt:

```md
> /verifier confirm the auth flow is complete
> /debugger investigate this error
> /security-auditor review the payment module
```

## Example subagents

### Debugger

```md
---
name: debugger
description: Debugging specialist for errors and test failures. Use when encountering issues.
---

You are an expert debugger specializing in root cause analysis.

When invoked:

1. Capture error message and stack trace
2. Identify reproduction steps
3. Isolate the failure location
4. Implement minimal fix
5. Verify solution works

For each issue, provide:

- Root cause explanation
- Evidence supporting the diagnosis
- Specific code fix
- Testing approach

Focus on fixing the underlying issue, not symptoms.
```

### Test runner

```md
---
name: test-runner
description: Test automation expert. Use proactively to run tests and fix failures.
---

You are a test automation expert.
When you see code changes, proactively run appropriate tests.

If tests fail:

1. Analyze the failure output
2. Identify the root cause
3. Fix the issue while preserving test intent
4. Re-run to verify

Report test results with:

- Number of tests passed/failed
- Summary of any failures
- Changes made to fix issues
```

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

show: `jq -r '.[] | "\(.identifier.id)\t\(.version)"' ~/.cursor/extensions/extensions.json | sort | column -t`

```
anysphere.cursorpyright              1.0.10
bmewburn.vscode-intelephense-client  1.16.4
dbaeumer.vscode-eslint               3.0.20
deerawan.vscode-faker                2.0.0
dotjoshjohnson.xml                   2.5.1
dracula-theme.theme-dracula          2.25.1
eamodio.gitlens                      17.9.0
esbenp.prettier-vscode               11.0.2
getpsalm.psalm-vscode-plugin         2.7.0
hashicorp.terraform                  2.37.6
mechatroner.rainbow-csv              3.3.0
ms-python.debugpy                    2025.18.0
ms-python.python                     2025.6.1
oderwat.indent-rainbow               8.3.1
pkief.material-icon-theme            5.30.0
```
