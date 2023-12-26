```json
{
  // Theme and icons
  "workbench.colorTheme": "GitHub Dark Default",
  "workbench.iconTheme": "material-icon-theme",

  // Workbench
  "workbench.tree.indent": 15,

  // Editor: appearance and behavior
  "editor.fontSize": 14,
  "editor.fontFamily": "JetBrains Mono",
  "editor.fontLigatures": true,
  "editor.tabSize": 4,
  "editor.formatOnSave": true,
  "editor.formatOnPaste": true,
  "editor.minimap.enabled": true,
  "editor.inlineSuggest.enabled": true,
  "editor.guides.bracketPairs": true,
  "editor.tokenColorCustomizations": {
    "textMateRules": [
      {
        "scope": "variable",
        "settings": {
          "fontStyle": "italic"
        }
      },
      {
        "scope": "entity.name.type.class",
        "settings": {
          "fontStyle": "underline"
        }
      }
    ]
  },

  // Language specific settings
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "typescript.updateImportsOnFileMove.enabled": "always",
  "javascript.preferences.importModuleSpecifier": "relative",
  "javascript.updateImportsOnFileMove.enabled": "always",

  // File handling
  "files.trimTrailingWhitespace": true,

  // Terminal settings
  "terminal.integrated.defaultProfile.osx": "zsh",
  "terminal.external.osxExec": "Warp.app",
  "terminal.external.linuxExec": "warp",

  // Diff Editor
  "diffEditor.ignoreTrimWhitespace": false,

  // Miscellaneous
  "symbols.hidesExplorerArrows": false,
  "security.workspace.trust.untrustedFiles": "open",
  "explorer.confirmDragAndDrop": false
}
```