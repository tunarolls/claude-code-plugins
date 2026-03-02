# OmniSharp LSP Plugin

C# language server (OmniSharp) for Claude Code, providing code intelligence and diagnostics.

## Supported Extensions
`.cs`

## Installation

### 1. Install OmniSharp

**Windows (recommended):**
```powershell
# Download from GitHub releases
$version = "v1.39.15"
$url = "https://github.com/OmniSharp/omnisharp-roslyn/releases/download/$version/omnisharp-win-x64-net6.0.zip"
$dest = "$env:USERPROFILE\.local\bin\omnisharp"
New-Item -ItemType Directory -Force -Path $dest
Invoke-WebRequest -Uri $url -OutFile "$dest\omnisharp.zip"
Expand-Archive -Path "$dest\omnisharp.zip" -DestinationPath $dest -Force
Remove-Item "$dest\omnisharp.zip"

# Add to PATH (or add this to your profile)
$env:PATH += ";$dest"
```

**Or via bash (Git Bash/WSL):**
```bash
mkdir -p ~/.local/bin/omnisharp
curl -L -o ~/.local/bin/omnisharp/omnisharp.zip \
  "https://github.com/OmniSharp/omnisharp-roslyn/releases/download/v1.39.15/omnisharp-win-x64-net6.0.zip"
cd ~/.local/bin/omnisharp && unzip -o omnisharp.zip && rm omnisharp.zip
```

**macOS:**
```bash
brew install omnisharp/omnisharp-roslyn/omnisharp-mono
```

**Linux:**
```bash
# Download appropriate release from GitHub
# https://github.com/OmniSharp/omnisharp-roslyn/releases
```

### 2. Ensure OmniSharp is in PATH

Either add OmniSharp to your system PATH, or create an alias/symlink:

```bash
# Option A: Add to PATH in your shell profile
export PATH="$HOME/.local/bin/omnisharp:$PATH"

# Option B: Create symlink (if OmniSharp.exe exists)
ln -s ~/.local/bin/omnisharp/OmniSharp.exe ~/.local/bin/omnisharp
```

### 3. Install the Plugin

From the repo root:
```bash
/plugin install .claude/plugins/omnisharp-lsp
```

Or add the repo's `.claude/plugins` as a marketplace:
```bash
/plugin marketplace add .claude/plugins
```

### 4. Enable in settings

Add to `~/.claude/settings.json`:
```json
{
  "enabledPlugins": {
    "omnisharp-lsp@local": true
  },
  "env": {
    "ENABLE_LSP_TOOL": "1"
  }
}
```

## Requirements
- .NET SDK 6.0 or later
- OmniSharp in PATH (or absolute path configured)
- Claude Code 2.1.50+

## Quick Setup (TL;DR)

```bash
# 1. Install OmniSharp (Windows/Git Bash)
mkdir -p ~/.local/bin/omnisharp && cd ~/.local/bin/omnisharp
curl -LO "https://github.com/OmniSharp/omnisharp-roslyn/releases/download/v1.39.15/omnisharp-win-x64-net6.0.zip"
unzip -o omnisharp-win-x64-net6.0.zip && rm omnisharp-win-x64-net6.0.zip

# 2. Add to PATH (add to ~/.bashrc or ~/.bash_profile)
export PATH="$HOME/.local/bin/omnisharp:$PATH"

# 3. Install plugin (from repo root in Claude Code)
/plugin marketplace add .claude/plugins
/plugin install omnisharp-lsp@acctsys-plugins

# 4. Add to ~/.claude/settings.json
# {
#   "enabledPlugins": { "omnisharp-lsp@acctsys-plugins": true },
#   "env": { "ENABLE_LSP_TOOL": "1" }
# }

# 5. Restart Claude Code
```

## LSP Operations

Once enabled, the LSP tool provides these operations:

| Operation | Description |
|-----------|-------------|
| `documentSymbol` | List all symbols (classes, methods, properties) in a file |
| `goToDefinition` | Jump to where a symbol is defined |
| `findReferences` | Find all usages of a symbol |
| `hover` | Get type info and documentation |
| `goToImplementation` | Find implementations of an interface |
| `workspaceSymbol` | Search symbols across the workspace |
| `prepareCallHierarchy` | Get call hierarchy for a function |
| `incomingCalls` | Find callers of a function |
| `outgoingCalls` | Find functions called by a function |

## More Information
- [OmniSharp GitHub](https://github.com/OmniSharp/omnisharp-roslyn)
- [.NET SDK Download](https://dotnet.microsoft.com/download)
