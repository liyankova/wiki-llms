---
url: https://opencode.ai/config.json
title: Page
source_domain: opencode.ai
---

# Page

{
"$schema": "https://json-schema.org/draft/2020-12/schema",
"ref": "Config",
"type": "object",
"properties": {
"$schema": {
"description": "JSON schema reference for configuration validation",
"type": "string"
},
"theme": {
"description": "Theme name to use for the interface",
"type": "string"
},
"keybinds": {
"description": "Custom keybind configurations",
"ref": "KeybindsConfig",
"type": "object",
"properties": {
"leader": {
"description": "Leader key for keybind combinations\n\ndefault: `ctrl+x`",
"default": "ctrl+x",
"type": "string",
"examples": [
"ctrl+x"
]
},
"app\_exit": {
"description": "Exit the application\n\ndefault: `ctrl+c,ctrl+d,q`",
"default": "ctrl+c,ctrl+d,q",
"type": "string",
"examples": [
"ctrl+c,ctrl+d,q"
]
},
"editor\_open": {
"description": "Open external editor\n\ndefault: `e`",
"default": "e",
"type": "string",
"examples": [
"e"
]
},
"theme\_list": {
"description": "List available themes\n\ndefault: `t`",
"default": "t",
"type": "string",
"examples": [
"t"
]
},
"sidebar\_toggle": {
"description": "Toggle sidebar\n\ndefault: `b`",
"default": "b",
"type": "string",
"examples": [
"b"
]
},
"scrollbar\_toggle": {
"description": "Toggle session scrollbar\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"username\_toggle": {
"description": "Toggle username visibility\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"status\_view": {
"description": "View status\n\ndefault: `s`",
"default": "s",
"type": "string",
"examples": [
"s"
]
},
"session\_export": {
"description": "Export session to editor\n\ndefault: `x`",
"default": "x",
"type": "string",
"examples": [
"x"
]
},
"session\_new": {
"description": "Create a new session\n\ndefault: `n`",
"default": "n",
"type": "string",
"examples": [
"n"
]
},
"session\_list": {
"description": "List all sessions\n\ndefault: `l`",
"default": "l",
"type": "string",
"examples": [
"l"
]
},
"session\_timeline": {
"description": "Show session timeline\n\ndefault: `g`",
"default": "g",
"type": "string",
"examples": [
"g"
]
},
"session\_fork": {
"description": "Fork session from message\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"session\_rename": {
"description": "Rename session\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"session\_share": {
"description": "Share current session\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"session\_unshare": {
"description": "Unshare current session\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"session\_interrupt": {
"description": "Interrupt current session\n\ndefault: `escape`",
"default": "escape",
"type": "string",
"examples": [
"escape"
]
},
"session\_compact": {
"description": "Compact the session\n\ndefault: `c`",
"default": "c",
"type": "string",
"examples": [
"c"
]
},
"messages\_page\_up": {
"description": "Scroll messages up by one page\n\ndefault: `pageup`",
"default": "pageup",
"type": "string",
"examples": [
"pageup"
]
},
"messages\_page\_down": {
"description": "Scroll messages down by one page\n\ndefault: `pagedown`",
"default": "pagedown",
"type": "string",
"examples": [
"pagedown"
]
},
"messages\_half\_page\_up": {
"description": "Scroll messages up by half page\n\ndefault: `ctrl+alt+u`",
"default": "ctrl+alt+u",
"type": "string",
"examples": [
"ctrl+alt+u"
]
},
"messages\_half\_page\_down": {
"description": "Scroll messages down by half page\n\ndefault: `ctrl+alt+d`",
"default": "ctrl+alt+d",
"type": "string",
"examples": [
"ctrl+alt+d"
]
},
"messages\_first": {
"description": "Navigate to first message\n\ndefault: `ctrl+g,home`",
"default": "ctrl+g,home",
"type": "string",
"examples": [
"ctrl+g,home"
]
},
"messages\_last": {
"description": "Navigate to last message\n\ndefault: `ctrl+alt+g,end`",
"default": "ctrl+alt+g,end",
"type": "string",
"examples": [
"ctrl+alt+g,end"
]
},
"messages\_next": {
"description": "Navigate to next message\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"messages\_previous": {
"description": "Navigate to previous message\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"messages\_last\_user": {
"description": "Navigate to last user message\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"messages\_copy": {
"description": "Copy message\n\ndefault: `y`",
"default": "y",
"type": "string",
"examples": [
"y"
]
},
"messages\_undo": {
"description": "Undo message\n\ndefault: `u`",
"default": "u",
"type": "string",
"examples": [
"u"
]
},
"messages\_redo": {
"description": "Redo message\n\ndefault: `r`",
"default": "r",
"type": "string",
"examples": [
"r"
]
},
"messages\_toggle\_conceal": {
"description": "Toggle code block concealment in messages\n\ndefault: `h`",
"default": "h",
"type": "string",
"examples": [
"h"
]
},
"tool\_details": {
"description": "Toggle tool details visibility\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"model\_list": {
"description": "List available models\n\ndefault: `m`",
"default": "m",
"type": "string",
"examples": [
"m"
]
},
"model\_cycle\_recent": {
"description": "Next recently used model\n\ndefault: `f2`",
"default": "f2",
"type": "string",
"examples": [
"f2"
]
},
"model\_cycle\_recent\_reverse": {
"description": "Previous recently used model\n\ndefault: `shift+f2`",
"default": "shift+f2",
"type": "string",
"examples": [
"shift+f2"
]
},
"model\_cycle\_favorite": {
"description": "Next favorite model\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"model\_cycle\_favorite\_reverse": {
"description": "Previous favorite model\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"command\_list": {
"description": "List available commands\n\ndefault: `ctrl+p`",
"default": "ctrl+p",
"type": "string",
"examples": [
"ctrl+p"
]
},
"agent\_list": {
"description": "List agents\n\ndefault: `a`",
"default": "a",
"type": "string",
"examples": [
"a"
]
},
"agent\_cycle": {
"description": "Next agent\n\ndefault: `tab`",
"default": "tab",
"type": "string",
"examples": [
"tab"
]
},
"agent\_cycle\_reverse": {
"description": "Previous agent\n\ndefault: `shift+tab`",
"default": "shift+tab",
"type": "string",
"examples": [
"shift+tab"
]
},
"variant\_cycle": {
"description": "Cycle model variants\n\ndefault: `ctrl+t`",
"default": "ctrl+t",
"type": "string",
"examples": [
"ctrl+t"
]
},
"input\_clear": {
"description": "Clear input field\n\ndefault: `ctrl+c`",
"default": "ctrl+c",
"type": "string",
"examples": [
"ctrl+c"
]
},
"input\_paste": {
"description": "Paste from clipboard\n\ndefault: `ctrl+v`",
"default": "ctrl+v",
"type": "string",
"examples": [
"ctrl+v"
]
},
"input\_submit": {
"description": "Submit input\n\ndefault: `return`",
"default": "return",
"type": "string",
"examples": [
"return"
]
},
"input\_newline": {
"description": "Insert newline in input\n\ndefault: `shift+return,ctrl+return,alt+return,ctrl+j`",
"default": "shift+return,ctrl+return,alt+return,ctrl+j",
"type": "string",
"examples": [
"shift+return,ctrl+return,alt+return,ctrl+j"
]
},
"input\_move\_left": {
"description": "Move cursor left in input\n\ndefault: `left,ctrl+b`",
"default": "left,ctrl+b",
"type": "string",
"examples": [
"left,ctrl+b"
]
},
"input\_move\_right": {
"description": "Move cursor right in input\n\ndefault: `right,ctrl+f`",
"default": "right,ctrl+f",
"type": "string",
"examples": [
"right,ctrl+f"
]
},
"input\_move\_up": {
"description": "Move cursor up in input\n\ndefault: `up`",
"default": "up",
"type": "string",
"examples": [
"up"
]
},
"input\_move\_down": {
"description": "Move cursor down in input\n\ndefault: `down`",
"default": "down",
"type": "string",
"examples": [
"down"
]
},
"input\_select\_left": {
"description": "Select left in input\n\ndefault: `shift+left`",
"default": "shift+left",
"type": "string",
"examples": [
"shift+left"
]
},
"input\_select\_right": {
"description": "Select right in input\n\ndefault: `shift+right`",
"default": "shift+right",
"type": "string",
"examples": [
"shift+right"
]
},
"input\_select\_up": {
"description": "Select up in input\n\ndefault: `shift+up`",
"default": "shift+up",
"type": "string",
"examples": [
"shift+up"
]
},
"input\_select\_down": {
"description": "Select down in input\n\ndefault: `shift+down`",
"default": "shift+down",
"type": "string",
"examples": [
"shift+down"
]
},
"input\_line\_home": {
"description": "Move to start of line in input\n\ndefault: `ctrl+a`",
"default": "ctrl+a",
"type": "string",
"examples": [
"ctrl+a"
]
},
"input\_line\_end": {
"description": "Move to end of line in input\n\ndefault: `ctrl+e`",
"default": "ctrl+e",
"type": "string",
"examples": [
"ctrl+e"
]
},
"input\_select\_line\_home": {
"description": "Select to start of line in input\n\ndefault: `ctrl+shift+a`",
"default": "ctrl+shift+a",
"type": "string",
"examples": [
"ctrl+shift+a"
]
},
"input\_select\_line\_end": {
"description": "Select to end of line in input\n\ndefault: `ctrl+shift+e`",
"default": "ctrl+shift+e",
"type": "string",
"examples": [
"ctrl+shift+e"
]
},
"input\_visual\_line\_home": {
"description": "Move to start of visual line in input\n\ndefault: `alt+a`",
"default": "alt+a",
"type": "string",
"examples": [
"alt+a"
]
},
"input\_visual\_line\_end": {
"description": "Move to end of visual line in input\n\ndefault: `alt+e`",
"default": "alt+e",
"type": "string",
"examples": [
"alt+e"
]
},
"input\_select\_visual\_line\_home": {
"description": "Select to start of visual line in input\n\ndefault: `alt+shift+a`",
"default": "alt+shift+a",
"type": "string",
"examples": [
"alt+shift+a"
]
},
"input\_select\_visual\_line\_end": {
"description": "Select to end of visual line in input\n\ndefault: `alt+shift+e`",
"default": "alt+shift+e",
"type": "string",
"examples": [
"alt+shift+e"
]
},
"input\_buffer\_home": {
"description": "Move to start of buffer in input\n\ndefault: `home`",
"default": "home",
"type": "string",
"examples": [
"home"
]
},
"input\_buffer\_end": {
"description": "Move to end of buffer in input\n\ndefault: `end`",
"default": "end",
"type": "string",
"examples": [
"end"
]
},
"input\_select\_buffer\_home": {
"description": "Select to start of buffer in input\n\ndefault: `shift+home`",
"default": "shift+home",
"type": "string",
"examples": [
"shift+home"
]
},
"input\_select\_buffer\_end": {
"description": "Select to end of buffer in input\n\ndefault: `shift+end`",
"default": "shift+end",
"type": "string",
"examples": [
"shift+end"
]
},
"input\_delete\_line": {
"description": "Delete line in input\n\ndefault: `ctrl+shift+d`",
"default": "ctrl+shift+d",
"type": "string",
"examples": [
"ctrl+shift+d"
]
},
"input\_delete\_to\_line\_end": {
"description": "Delete to end of line in input\n\ndefault: `ctrl+k`",
"default": "ctrl+k",
"type": "string",
"examples": [
"ctrl+k"
]
},
"input\_delete\_to\_line\_start": {
"description": "Delete to start of line in input\n\ndefault: `ctrl+u`",
"default": "ctrl+u",
"type": "string",
"examples": [
"ctrl+u"
]
},
"input\_backspace": {
"description": "Backspace in input\n\ndefault: `backspace,shift+backspace`",
"default": "backspace,shift+backspace",
"type": "string",
"examples": [
"backspace,shift+backspace"
]
},
"input\_delete": {
"description": "Delete character in input\n\ndefault: `ctrl+d,delete,shift+delete`",
"default": "ctrl+d,delete,shift+delete",
"type": "string",
"examples": [
"ctrl+d,delete,shift+delete"
]
},
"input\_undo": {
"description": "Undo in input\n\ndefault: `ctrl+-,super+z`",
"default": "ctrl+-,super+z",
"type": "string",
"examples": [
"ctrl+-,super+z"
]
},
"input\_redo": {
"description": "Redo in input\n\ndefault: `ctrl+.,super+shift+z`",
"default": "ctrl+.,super+shift+z",
"type": "string",
"examples": [
"ctrl+.,super+shift+z"
]
},
"input\_word\_forward": {
"description": "Move word forward in input\n\ndefault: `alt+f,alt+right,ctrl+right`",
"default": "alt+f,alt+right,ctrl+right",
"type": "string",
"examples": [
"alt+f,alt+right,ctrl+right"
]
},
"input\_word\_backward": {
"description": "Move word backward in input\n\ndefault: `alt+b,alt+left,ctrl+left`",
"default": "alt+b,alt+left,ctrl+left",
"type": "string",
"examples": [
"alt+b,alt+left,ctrl+left"
]
},
"input\_select\_word\_forward": {
"description": "Select word forward in input\n\ndefault: `alt+shift+f,alt+shift+right`",
"default": "alt+shift+f,alt+shift+right",
"type": "string",
"examples": [
"alt+shift+f,alt+shift+right"
]
},
"input\_select\_word\_backward": {
"description": "Select word backward in input\n\ndefault: `alt+shift+b,alt+shift+left`",
"default": "alt+shift+b,alt+shift+left",
"type": "string",
"examples": [
"alt+shift+b,alt+shift+left"
]
},
"input\_delete\_word\_forward": {
"description": "Delete word forward in input\n\ndefault: `alt+d,alt+delete,ctrl+delete`",
"default": "alt+d,alt+delete,ctrl+delete",
"type": "string",
"examples": [
"alt+d,alt+delete,ctrl+delete"
]
},
"input\_delete\_word\_backward": {
"description": "Delete word backward in input\n\ndefault: `ctrl+w,ctrl+backspace,alt+backspace`",
"default": "ctrl+w,ctrl+backspace,alt+backspace",
"type": "string",
"examples": [
"ctrl+w,ctrl+backspace,alt+backspace"
]
},
"history\_previous": {
"description": "Previous history item\n\ndefault: `up`",
"default": "up",
"type": "string",
"examples": [
"up"
]
},
"history\_next": {
"description": "Next history item\n\ndefault: `down`",
"default": "down",
"type": "string",
"examples": [
"down"
]
},
"session\_child\_cycle": {
"description": "Next child session\n\ndefault: `right`",
"default": "right",
"type": "string",
"examples": [
"right"
]
},
"session\_child\_cycle\_reverse": {
"description": "Previous child session\n\ndefault: `left`",
"default": "left",
"type": "string",
"examples": [
"left"
]
},
"session\_parent": {
"description": "Go to parent session\n\ndefault: `up`",
"default": "up",
"type": "string",
"examples": [
"up"
]
},
"terminal\_suspend": {
"description": "Suspend terminal\n\ndefault: `ctrl+z`",
"default": "ctrl+z",
"type": "string",
"examples": [
"ctrl+z"
]
},
"terminal\_title\_toggle": {
"description": "Toggle terminal title\n\ndefault: `none`",
"default": "none",
"type": "string",
"examples": [
"none"
]
},
"tips\_toggle": {
"description": "Toggle tips on home screen\n\ndefault: `h`",
"default": "h",
"type": "string",
"examples": [
"h"
]
}
},
"additionalProperties": false
},
"logLevel": {
"description": "Log level",
"ref": "LogLevel",
"type": "string",
"enum": [
"DEBUG",
"INFO",
"WARN",
"ERROR"
]
},
"tui": {
"description": "TUI specific settings",
"type": "object",
"properties": {
"scroll\_speed": {
"description": "TUI scroll speed",
"type": "number",
"minimum": 0.001
},
"scroll\_acceleration": {
"description": "Scroll acceleration settings",
"type": "object",
"properties": {
"enabled": {
"description": "Enable scroll acceleration",
"type": "boolean"
}
},
"required": [
"enabled"
],
"additionalProperties": false
},
"diff\_style": {
"description": "Control diff rendering style: 'auto' adapts to terminal width, 'stacked' always shows single column",
"type": "string",
"enum": [
"auto",
"stacked"
]
}
},
"additionalProperties": false
},
"server": {
"description": "Server configuration for opencode serve and web commands",
"ref": "ServerConfig",
"type": "object",
"properties": {
"port": {
"description": "Port to listen on",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"hostname": {
"description": "Hostname to listen on",
"type": "string"
},
"mdns": {
"description": "Enable mDNS service discovery",
"type": "boolean"
},
"cors": {
"description": "Additional domains to allow for CORS",
"type": "array",
"items": {
"type": "string"
}
}
},
"additionalProperties": false
},
"command": {
"description": "Command configuration, see https://opencode.ai/docs/commands",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "object",
"properties": {
"template": {
"type": "string"
},
"description": {
"type": "string"
},
"agent": {
"type": "string"
},
"model": {
"type": "string"
},
"subtask": {
"type": "boolean"
}
},
"required": [
"template"
],
"additionalProperties": false
}
},
"watcher": {
"type": "object",
"properties": {
"ignore": {
"type": "array",
"items": {
"type": "string"
}
}
},
"additionalProperties": false
},
"plugin": {
"type": "array",
"items": {
"type": "string"
}
},
"snapshot": {
"type": "boolean"
},
"share": {
"description": "Control sharing behavior:'manual' allows manual sharing via commands, 'auto' enables automatic sharing, 'disabled' disables all sharing",
"type": "string",
"enum": [
"manual",
"auto",
"disabled"
]
},
"autoshare": {
"description": "@deprecated Use 'share' field instead. Share newly created sessions automatically",
"type": "boolean"
},
"autoupdate": {
"description": "Automatically update to the latest version. Set to true to auto-update, false to disable, or 'notify' to show update notifications",
"anyOf": [
{
"type": "boolean"
},
{
"type": "string",
"const": "notify"
}
]
},
"disabled\_providers": {
"description": "Disable providers that are loaded automatically",
"type": "array",
"items": {
"type": "string"
}
},
"enabled\_providers": {
"description": "When set, ONLY these providers will be enabled. All other providers will be ignored",
"type": "array",
"items": {
"type": "string"
}
},
"model": {
"description": "Model to use in the format of provider/model, eg anthropic/claude-2",
"type": "string"
},
"small\_model": {
"description": "Small model to use for tasks like title generation in the format of provider/model",
"type": "string"
},
"default\_agent": {
"description": "Default agent to use when none is specified. Must be a primary agent. Falls back to 'build' if not set or if the specified agent is invalid.",
"type": "string"
},
"username": {
"description": "Custom username to display in conversations instead of system username",
"type": "string"
},
"mode": {
"description": "@deprecated Use `agent` field instead.",
"type": "object",
"properties": {
"build": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
},
"plan": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
}
},
"additionalProperties": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
}
},
"agent": {
"description": "Agent configuration, see https://opencode.ai/docs/agent",
"type": "object",
"properties": {
"plan": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
},
"build": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
},
"general": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
},
"explore": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
},
"title": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
},
"summary": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
},
"compaction": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
}
},
"additionalProperties": {
"ref": "AgentConfig",
"type": "object",
"properties": {
"model": {
"type": "string"
},
"temperature": {
"type": "number"
},
"top\_p": {
"type": "number"
},
"prompt": {
"type": "string"
},
"tools": {
"description": "@deprecated Use 'permission' field instead",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"disable": {
"type": "boolean"
},
"description": {
"description": "Description of when to use the agent",
"type": "string"
},
"mode": {
"type": "string",
"enum": [
"subagent",
"primary",
"all"
]
},
"hidden": {
"description": "Hide this subagent from the @ autocomplete menu (default: false, only applies to mode: subagent)",
"type": "boolean"
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"color": {
"description": "Hex color code for the agent (e.g., #FF5733)",
"type": "string",
"pattern": "^#[0-9a-fA-F]{6}$"
},
"steps": {
"description": "Maximum number of agentic iterations before forcing text-only response",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"maxSteps": {
"description": "@deprecated Use 'steps' field instead.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
}
},
"additionalProperties": {}
}
},
"provider": {
"description": "Custom provider configurations and model overrides",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "ProviderConfig",
"type": "object",
"properties": {
"api": {
"type": "string"
},
"name": {
"type": "string"
},
"env": {
"type": "array",
"items": {
"type": "string"
}
},
"id": {
"type": "string"
},
"npm": {
"type": "string"
},
"models": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "object",
"properties": {
"id": {
"type": "string"
},
"name": {
"type": "string"
},
"family": {
"type": "string"
},
"release\_date": {
"type": "string"
},
"attachment": {
"type": "boolean"
},
"reasoning": {
"type": "boolean"
},
"temperature": {
"type": "boolean"
},
"tool\_call": {
"type": "boolean"
},
"interleaved": {
"anyOf": [
{
"type": "boolean",
"const": true
},
{
"type": "object",
"properties": {
"field": {
"type": "string",
"enum": [
"reasoning\_content",
"reasoning\_details"
]
}
},
"required": [
"field"
],
"additionalProperties": false
}
]
},
"cost": {
"type": "object",
"properties": {
"input": {
"type": "number"
},
"output": {
"type": "number"
},
"cache\_read": {
"type": "number"
},
"cache\_write": {
"type": "number"
},
"context\_over\_200k": {
"type": "object",
"properties": {
"input": {
"type": "number"
},
"output": {
"type": "number"
},
"cache\_read": {
"type": "number"
},
"cache\_write": {
"type": "number"
}
},
"required": [
"input",
"output"
],
"additionalProperties": false
}
},
"required": [
"input",
"output"
],
"additionalProperties": false
},
"limit": {
"type": "object",
"properties": {
"context": {
"type": "number"
},
"output": {
"type": "number"
}
},
"required": [
"context",
"output"
],
"additionalProperties": false
},
"modalities": {
"type": "object",
"properties": {
"input": {
"type": "array",
"items": {
"type": "string",
"enum": [
"text",
"audio",
"image",
"video",
"pdf"
]
}
},
"output": {
"type": "array",
"items": {
"type": "string",
"enum": [
"text",
"audio",
"image",
"video",
"pdf"
]
}
}
},
"required": [
"input",
"output"
],
"additionalProperties": false
},
"experimental": {
"type": "boolean"
},
"status": {
"type": "string",
"enum": [
"alpha",
"beta",
"deprecated"
]
},
"options": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
},
"headers": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "string"
}
},
"provider": {
"type": "object",
"properties": {
"npm": {
"type": "string"
}
},
"required": [
"npm"
],
"additionalProperties": false
},
"variants": {
"description": "Variant-specific configuration",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "object",
"properties": {
"disabled": {
"description": "Disable this variant for the model",
"type": "boolean"
}
},
"additionalProperties": {}
}
}
},
"additionalProperties": false
}
},
"whitelist": {
"type": "array",
"items": {
"type": "string"
}
},
"blacklist": {
"type": "array",
"items": {
"type": "string"
}
},
"options": {
"type": "object",
"properties": {
"apiKey": {
"type": "string"
},
"baseURL": {
"type": "string"
},
"enterpriseUrl": {
"description": "GitHub Enterprise URL for copilot authentication",
"type": "string"
},
"setCacheKey": {
"description": "Enable promptCacheKey for this provider (default false)",
"type": "boolean"
},
"timeout": {
"description": "Timeout in milliseconds for requests to this provider. Default is 300000 (5 minutes). Set to false to disable timeout.",
"anyOf": [
{
"description": "Timeout in milliseconds for requests to this provider. Default is 300000 (5 minutes). Set to false to disable timeout.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
},
{
"description": "Disable timeout for this provider entirely.",
"type": "boolean",
"const": false
}
]
}
},
"additionalProperties": {}
}
},
"additionalProperties": false
}
},
"mcp": {
"description": "MCP (Model Context Protocol) server configurations",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"anyOf": [
{
"anyOf": [
{
"ref": "McpLocalConfig",
"type": "object",
"properties": {
"type": {
"description": "Type of MCP server connection",
"type": "string",
"const": "local"
},
"command": {
"description": "Command and arguments to run the MCP server",
"type": "array",
"items": {
"type": "string"
}
},
"environment": {
"description": "Environment variables to set when running the MCP server",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "string"
}
},
"enabled": {
"description": "Enable or disable the MCP server on startup",
"type": "boolean"
},
"timeout": {
"description": "Timeout in ms for fetching tools from the MCP server. Defaults to 5000 (5 seconds) if not specified.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
}
},
"required": [
"type",
"command"
],
"additionalProperties": false
},
{
"ref": "McpRemoteConfig",
"type": "object",
"properties": {
"type": {
"description": "Type of MCP server connection",
"type": "string",
"const": "remote"
},
"url": {
"description": "URL of the remote MCP server",
"type": "string"
},
"enabled": {
"description": "Enable or disable the MCP server on startup",
"type": "boolean"
},
"headers": {
"description": "Headers to send with the request",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "string"
}
},
"oauth": {
"description": "OAuth authentication configuration for the MCP server. Set to false to disable OAuth auto-detection.",
"anyOf": [
{
"ref": "McpOAuthConfig",
"type": "object",
"properties": {
"clientId": {
"description": "OAuth client ID. If not provided, dynamic client registration (RFC 7591) will be attempted.",
"type": "string"
},
"clientSecret": {
"description": "OAuth client secret (if required by the authorization server)",
"type": "string"
},
"scope": {
"description": "OAuth scopes to request during authorization",
"type": "string"
}
},
"additionalProperties": false
},
{
"type": "boolean",
"const": false
}
]
},
"timeout": {
"description": "Timeout in ms for fetching tools from the MCP server. Defaults to 5000 (5 seconds) if not specified.",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
}
},
"required": [
"type",
"url"
],
"additionalProperties": false
}
]
},
{
"type": "object",
"properties": {
"enabled": {
"type": "boolean"
}
},
"required": [
"enabled"
],
"additionalProperties": false
}
]
}
},
"formatter": {
"anyOf": [
{
"type": "boolean",
"const": false
},
{
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "object",
"properties": {
"disabled": {
"type": "boolean"
},
"command": {
"type": "array",
"items": {
"type": "string"
}
},
"environment": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "string"
}
},
"extensions": {
"type": "array",
"items": {
"type": "string"
}
}
},
"additionalProperties": false
}
}
]
},
"lsp": {
"anyOf": [
{
"type": "boolean",
"const": false
},
{
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"anyOf": [
{
"type": "object",
"properties": {
"disabled": {
"type": "boolean",
"const": true
}
},
"required": [
"disabled"
],
"additionalProperties": false
},
{
"type": "object",
"properties": {
"command": {
"type": "array",
"items": {
"type": "string"
}
},
"extensions": {
"type": "array",
"items": {
"type": "string"
}
},
"disabled": {
"type": "boolean"
},
"env": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "string"
}
},
"initialization": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {}
}
},
"required": [
"command"
],
"additionalProperties": false
}
]
}
}
]
},
"instructions": {
"description": "Additional instruction files or patterns to include",
"type": "array",
"items": {
"type": "string"
}
},
"layout": {
"description": "@deprecated Always uses stretch layout.",
"ref": "LayoutConfig",
"type": "string",
"enum": [
"auto",
"stretch"
]
},
"permission": {
"ref": "PermissionConfig",
"anyOf": [
{
"type": "object",
"properties": {
"\_\_originalKeys": {
"type": "array",
"items": {
"type": "string"
}
},
"read": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"edit": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"glob": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"grep": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"list": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"bash": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"task": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"external\_directory": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"todowrite": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"todoread": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"question": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"webfetch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"websearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"codesearch": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
"lsp": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
},
"doom\_loop": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
},
"additionalProperties": {
"ref": "PermissionRuleConfig",
"anyOf": [
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
},
{
"ref": "PermissionObjectConfig",
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
}
]
}
},
{
"ref": "PermissionActionConfig",
"type": "string",
"enum": [
"ask",
"allow",
"deny"
]
}
]
},
"tools": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "boolean"
}
},
"enterprise": {
"type": "object",
"properties": {
"url": {
"description": "Enterprise URL",
"type": "string"
}
},
"additionalProperties": false
},
"compaction": {
"type": "object",
"properties": {
"auto": {
"description": "Enable automatic compaction when context is full (default: true)",
"type": "boolean"
},
"prune": {
"description": "Enable pruning of old tool outputs (default: true)",
"type": "boolean"
}
},
"additionalProperties": false
},
"experimental": {
"type": "object",
"properties": {
"hook": {
"type": "object",
"properties": {
"file\_edited": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "array",
"items": {
"type": "object",
"properties": {
"command": {
"type": "array",
"items": {
"type": "string"
}
},
"environment": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "string"
}
}
},
"required": [
"command"
],
"additionalProperties": false
}
}
},
"session\_completed": {
"type": "array",
"items": {
"type": "object",
"properties": {
"command": {
"type": "array",
"items": {
"type": "string"
}
},
"environment": {
"type": "object",
"propertyNames": {
"type": "string"
},
"additionalProperties": {
"type": "string"
}
}
},
"required": [
"command"
],
"additionalProperties": false
}
}
},
"additionalProperties": false
},
"chatMaxRetries": {
"description": "Number of retries for chat completions on failure",
"type": "number"
},
"disable\_paste\_summary": {
"type": "boolean"
},
"batch\_tool": {
"description": "Enable the batch tool",
"type": "boolean"
},
"openTelemetry": {
"description": "Enable OpenTelemetry spans for AI SDK calls (using the 'experimental\_telemetry' flag)",
"type": "boolean"
},
"primary\_tools": {
"description": "Tools that should only be available to primary agents.",
"type": "array",
"items": {
"type": "string"
}
},
"continue\_loop\_on\_deny": {
"description": "Continue the agent loop when a tool call is denied",
"type": "boolean"
},
"mcp\_timeout": {
"description": "Timeout in milliseconds for model context protocol (MCP) requests",
"type": "integer",
"exclusiveMinimum": 0,
"maximum": 9007199254740991
}
},
"additionalProperties": false
}
},
"additionalProperties": false,
"allowComments": true,
"allowTrailingCommas": true
}