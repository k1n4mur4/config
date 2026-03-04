# WezTerm Configuration for Windows

A feature-rich WezTerm terminal emulator configuration for Windows with Vim-inspired keybindings, workspace management, and multi-shell support.

## Features

- **Cross-platform keybindings**: Adaptive modifier keys (ALT for Windows, SUPER/Cmd for macOS)
- **Workspace management**: Organize tabs by project or context with dedicated workspaces
- **Multi-shell launcher**: Quick access to PowerShell, Command Prompt, Git Bash, and WSL distributions
- **Vim-inspired navigation**: Familiar H/J/K/L navigation for panes and copy mode
- **Custom visual theme**: 70% opacity with gold (#ae8b2d) and blue-gray (#5c6d74) tab colors
- **Modal editing**: Key tables for pane resizing, activation, and text selection
- **Comprehensive copy mode**: Full Vim-style text navigation and selection

## Prerequisites

**Required:**
- Windows 10 or Windows 11
- WezTerm version 20230712 or later (for workspace support and key tables)

**Optional:**
- PowerShell 7+ for enhanced shell experience
- Git Bash (Git for Windows) for Unix-like shell access
- WSL2 with distributions (Ubuntu, Kali Linux, etc.) for Linux integration
- Nerd Font (e.g., JetBrains Mono Nerd Font, FiraCode Nerd Font) for tab bar icons

## Installation

### Step 1: Install WezTerm

```powershell
# Using winget (recommended)
winget install wez.wezterm

# Or download installer from:
# https://wezfurlong.org/wezterm/install/windows.html
```

Verify installation:
```powershell
wezterm --version
# Should output: wezterm 20230712-xxxxxx or later
```

### Step 2: Clone This Repository

```powershell
# Clone to your preferred location
git clone https://github.com/kinamura/config.git
cd config
```

### Step 3: Create Configuration Directory

```powershell
# Create WezTerm config directory if it doesn't exist
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.config\wezterm"
```

### Step 4: Create Symbolic Links

**Important:** Run PowerShell as Administrator for symlink creation.

```powershell
# From the config repository root directory
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\.config\wezterm\wezterm.lua" -Target "$PWD\windows\.config\wezterm\wezterm.lua"
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\.config\wezterm\keybinds.lua" -Target "$PWD\windows\.config\wezterm\keybinds.lua"
```

**Alternative (without Administrator):** Copy files instead of symlinking:
```powershell
Copy-Item -Path "windows\.config\wezterm\*.lua" -Destination "$env:USERPROFILE\.config\wezterm\" -Force
```
*Note: Copying requires manual updates when pulling new changes.*

### Step 5: Verify Installation

1. Launch WezTerm (search "WezTerm" in Start menu)
2. Press `Ctrl+Shift+R` to reload configuration
3. Check for errors in the debug overlay (`Ctrl+Shift+L` → "Show Debug Overlay")
4. Test a keybinding: Press `Ctrl+Q` (leader key), then `W` to show workspaces

If no errors appear, installation is successful!

## Configuration Files Overview

| File | Purpose | Key Settings |
|------|---------|--------------|
| [wezterm.lua](./wezterm.lua) | Main configuration | Font size (12pt), opacity (70%), shell launcher, tab bar styling, OS detection |
| [keybinds.lua](./keybinds.lua) | Keybinding definitions | Leader key (Ctrl+Q), adaptive modifiers, key tables for resize/activate/copy modes |

### wezterm.lua Details

The main configuration file includes:
- **OS Detection**: Automatically detects Windows/macOS/Linux and adapts settings
- **Font Settings**: 12.0pt font size with IME (Input Method Editor) enabled for international input
- **Visual Settings**: 70% window background opacity for transparency
- **Shell Launcher**: Configurable menu with 6 shell options (PowerShell, CMD, Git Bash, WSL variants)
- **Custom Tab Bar**:
  - Triangular tab design using Nerd Font symbols
  - Active tab: Gold color (#ae8b2d)
  - Inactive tab: Blue-gray color (#5c6d74)
  - Hides tab bar when only one tab is open
- **Keybindings**: Disables default keybindings and imports from `keybinds.lua`

### keybinds.lua Details

The keybindings file provides:
- **Leader Key**: `Ctrl+Q` with 2-second timeout for prefix commands
- **Adaptive Modifiers**: Uses `ALT` on Windows, `SUPER` (Cmd) on macOS
- **Key Tables**: Three modal modes for specialized operations
  - `resize_pane`: Vim keys (H/J/K/L) to resize panes
  - `activate_pane`: Quick pane navigation with 1-second timeout
  - `copy_mode`: Comprehensive Vim-style text navigation and selection
- **Status Indicator**: Shows active key table name in right status bar

## Keybindings Reference

### Leader Key

The leader key enables prefix-based commands (similar to tmux):

| Key | Description |
|-----|-------------|
| `Ctrl+Q` | Leader key (2-second timeout) |

**Usage:** Press `Ctrl+Q`, then press another key within 2 seconds to execute leader commands (e.g., `Ctrl+Q` → `W` shows workspaces).

---

### Workspace Management

Workspaces allow you to organize tabs by project or context (e.g., "frontend", "backend", "devops").

| Keybinding | Action | Description |
|------------|--------|-------------|
| `Leader+W` | Show workspaces | Display workspace switcher launcher menu |
| `Leader+Shift+W` | Create workspace | Prompt to name and switch to new workspace |
| `Leader+$` | Rename workspace | Rename the current workspace |

**Tip:** Use workspaces to maintain separate tab groups for different projects without cluttering your tab bar.

---

### Tab Operations

| Keybinding | Action | Description |
|------------|--------|-------------|
| `Ctrl+T` | New tab | Create new tab in current workspace (Windows) |
| `Alt+T` | New tab | Create new tab (alternative on Windows) |
| `Cmd+T` | New tab | Create new tab (macOS) |
| `Ctrl+Tab` | Next tab | Cycle to the next tab |
| `Ctrl+Shift+Tab` | Previous tab | Cycle to the previous tab |
| `Alt+1` to `Alt+8` | Select tab 1-8 | Jump directly to tab by number |
| `Alt+9` | Select last tab | Jump to the last tab |
| `Alt+W` | Close tab | Close current tab without confirmation |
| `Leader+{` | Move tab left | Swap current tab position leftward |
| `Leader+}` | Move tab right | Swap current tab position rightward |
| `Ctrl+Shift+L` | Shell launcher | Open launcher menu to select shell type |

**Shell Launcher:** The launcher menu (`Ctrl+Shift+L`) provides quick access to:
- PowerShell
- Command Prompt
- Git Bash
- WSL (Ubuntu, Kali, Default distribution)

---

### Pane (Split Window) Operations

Panes allow you to split your terminal window into multiple sections.

| Keybinding | Action | Description |
|------------|--------|-------------|
| `Ctrl+D` | Split horizontal | Split current pane horizontally (tmux-style) |
| `Ctrl+Shift+D` | Split vertical | Split current pane vertically (tmux-style) |
| `Leader+D` | Split vertical | Alternative vertical split |
| `Leader+R` | Split horizontal | Alternative horizontal split |
| `Ctrl+L` | Close pane | Close current pane without confirmation |
| `Leader+X` | Close pane | Close pane with confirmation prompt |
| `Leader+H` | Move left | Focus the pane to the left (Vim-style) |
| `Leader+J` | Move down | Focus the pane below (Vim-style) |
| `Leader+K` | Move up | Focus the pane above (Vim-style) |
| `Leader+L` | Move right | Focus the pane to the right (Vim-style) |
| `Leader+S` | Resize mode | Enter pane resize mode (see below) |
| `Leader+A` | Quick activate | Enter quick pane activation mode (1s timeout) |
| `Ctrl+Shift+[` | Pane selector | Visual interface for pane selection |
| `Leader+Z` | Zoom pane | Toggle maximize/zoom current pane |

#### Resize Mode (`Leader+S`)

After pressing `Leader+S`, you enter resize mode. Use Vim keys to adjust pane sizes:

| Key | Action | Description |
|-----|--------|-------------|
| `H` | Shrink left | Move right border leftward (shrink horizontally) |
| `L` | Expand right | Move right border rightward (expand horizontally) |
| `K` | Shrink up | Move bottom border upward (shrink vertically) |
| `J` | Expand down | Move bottom border downward (expand vertically) |
| `Enter` | Exit | Exit resize mode |
| `Escape` | Exit | Exit resize mode |

**Status indicator:** While in resize mode, the status bar displays "TABLE: resize_pane".

#### Quick Activate Mode (`Leader+A`)

After pressing `Leader+A`, quickly press a direction key within 1 second:

| Key | Action |
|-----|--------|
| `H` | Jump to left pane |
| `J` | Jump to pane below |
| `K` | Jump to pane above |
| `L` | Jump to right pane |

**Tip:** This mode is faster than repeated `Leader+H/J/K/L` commands when you know your target direction.

---

### Copy & Paste

| Keybinding | Action | Description |
|------------|--------|-------------|
| `Ctrl+Shift+C` | Copy | Copy selected text to clipboard |
| `Ctrl+Shift+V` | Paste | Paste from clipboard |
| `Leader+[` | Copy mode | Enter copy/scrollback mode (Vim-style navigation) |

---

### Copy Mode Navigation

Copy mode provides Vim-style text navigation and selection. Enter with `Leader+[`.

**Status indicator:** While in copy mode, the status bar displays "TABLE: copy_mode".

#### Movement

| Keybinding | Action | Description |
|------------|--------|-------------|
| `H` | Move left | Move cursor one character left |
| `J` | Move down | Move cursor one line down |
| `K` | Move up | Move cursor one line up |
| `L` | Move right | Move cursor one character right |
| `W` | Forward word | Jump to start of next word |
| `B` | Backward word | Jump to start of previous word |
| `E` | End of word | Jump to end of current/next word |
| `^` | Line start (non-whitespace) | Jump to first non-whitespace character |
| `$` | Line end | Jump to end of line |
| `0` | Line start (column 0) | Jump to beginning of line (column 0) |

#### Scrolling

| Keybinding | Action | Description |
|------------|--------|-------------|
| `G` | Go to bottom | Jump to bottom of scrollback buffer |
| `gg` | Go to top | Jump to top of scrollback buffer |
| `Ctrl+F` | Page down | Scroll one full page down |
| `Ctrl+B` | Page up | Scroll one full page up |
| `Ctrl+D` | Half page down | Scroll half page down |
| `Ctrl+U` | Half page up | Scroll half page up |
| `H` (uppercase) | Top of viewport | Move to top line of visible area |
| `M` (uppercase) | Middle of viewport | Move to middle line of visible area |
| `L` (uppercase) | Bottom of viewport | Move to bottom line of visible area |

#### Selection

| Keybinding | Action | Description |
|------------|--------|-------------|
| `V` | Character selection | Start selecting by character (visual mode) |
| `Shift+V` | Line selection | Start selecting whole lines (visual line mode) |
| `Ctrl+V` | Block selection | Start selecting rectangular block (visual block mode) |
| `Y` | Yank (copy) | Copy selected text to clipboard |
| `Enter` | Yank and exit | Copy selected text and exit copy mode |

**Selection workflow:**
1. Navigate to start position
2. Press `V` (character), `Shift+V` (line), or `Ctrl+V` (block)
3. Move to end position
4. Press `Y` to copy or `Enter` to copy and exit

#### Jumping

| Keybinding | Action | Description |
|------------|--------|-------------|
| `F <char>` | Find forward | Jump forward to next occurrence of character |
| `T <char>` | Till forward | Jump forward to just before character |
| `Shift+F <char>` | Find backward | Jump backward to previous occurrence of character |
| `Shift+T <char>` | Till backward | Jump backward to just after character |
| `;` | Repeat jump | Repeat last F/T/f/t jump |

**Example:** Press `F`, then `x` to jump to the next "x" character.

#### Exit Copy Mode

| Keybinding | Action |
|------------|--------|
| `Escape` | Exit copy mode |
| `Ctrl+C` | Exit copy mode |
| `Q` | Exit copy mode |

---

### Visual & Interface

| Keybinding | Action | Description |
|------------|--------|-------------|
| `Alt+Enter` | Fullscreen toggle | Toggle fullscreen mode |
| `Alt+P` | Command palette | Open WezTerm command palette (Windows) |
| `Cmd+P` | Command palette | Open WezTerm command palette (macOS) |
| `Ctrl+Shift+P` | Command palette | Alternative command palette shortcut |
| `Ctrl+0` | Reset font size | Reset font size to default (12pt) |
| `Ctrl++` | Increase font size | Zoom in (increase font size) |
| `Ctrl+-` | Decrease font size | Zoom out (decrease font size) |
| `Ctrl+Shift+R` | Reload config | Reload WezTerm configuration files |

**Command Palette:** The command palette provides searchable access to all WezTerm commands, keybindings, and launcher menu items.

---

## Shell Launcher Menu

Press `Ctrl+Shift+L` to open the shell launcher menu with the following options:

| Menu Item | Command | Notes |
|-----------|---------|-------|
| PowerShell | `powershell.exe` | Default shell (Windows PowerShell 5.1) |
| Command Prompt | `cmd.exe` | Legacy Windows command interpreter |
| Git Bash | `C:\Program Files\Git\bin\bash.exe` | Requires Git for Windows installation |
| WSL (Ubuntu) | `wsl.exe -d Ubuntu-22.04` | Requires WSL2 and Ubuntu distribution |
| WSL (Kali) | `wsl.exe -d kali-linux` | Requires WSL2 and Kali Linux distribution |
| WSL (Default) | `wsl.exe` | Launches default WSL distribution |

### Customizing WSL Distributions

Update the distribution names in [wezterm.lua](./wezterm.lua) to match your installed WSL distributions:

1. **Check installed distributions:**
   ```powershell
   wsl -l -v
   ```

2. **Edit wezterm.lua:**
   ```lua
   {
     label = "WSL (YourDistro)",
     args = { "wsl.exe", "-d", "YourDistroName" },
   },
   ```

3. **Reload configuration:**
   Press `Ctrl+Shift+R` in WezTerm

---

## Customization Guide

### Changing Font

Edit [wezterm.lua](./wezterm.lua):

```lua
-- Change font family
config.font = wezterm.font("JetBrains Mono Nerd Font")
-- or
config.font = wezterm.font("FiraCode Nerd Font")

-- Change font size
config.font_size = 14.0  -- Default: 12.0
```

### Adjusting Opacity

Edit [wezterm.lua](./wezterm.lua):

```lua
-- Change window opacity (0.0 = fully transparent, 1.0 = fully opaque)
config.window_background_opacity = 0.9  -- Default: 0.7
```

### Modifying Tab Colors

Edit [wezterm.lua](./wezterm.lua) in the `format-tab-title` event handler:

```lua
local background = "#5c6d74"  -- Inactive tab color (blue-gray)
if tab.is_active then
  background = "#ae8b2d"      -- Active tab color (gold)
  -- Try other colors:
  -- background = "#ff6b6b"   -- Red
  -- background = "#4ecdc4"   -- Teal
  -- background = "#95e1d3"   -- Mint green
end
```

### Adding Custom Keybindings

Edit [keybinds.lua](./keybinds.lua) in the `keys` table:

```lua
-- Add new keybinding
{ key = "n", mods = "CTRL|SHIFT", action = act.SpawnWindow },

-- Add leader-based command
{ key = "c", mods = "LEADER", action = act.SpawnTab("CurrentPaneDomain") },
```

**Available actions:** See [WezTerm keybinding actions](https://wezfurlong.org/wezterm/config/lua/keyassignment/index.html).

### Changing Default Shell

Edit [wezterm.lua](./wezterm.lua):

```lua
-- Use PowerShell 7
config.default_prog = { "pwsh.exe" }

-- Use WSL Ubuntu
config.default_prog = { "wsl.exe", "-d", "Ubuntu-22.04" }

-- Use Git Bash
config.default_prog = { "C:\\Program Files\\Git\\bin\\bash.exe", "-i", "-l" }
```

### Modifying Leader Key

Edit [wezterm.lua](./wezterm.lua):

```lua
-- Change leader key to Ctrl+A (tmux-style)
config.leader = { key = "a", mods = "CTRL", timeout_milliseconds = 2000 }

-- Change leader key to Ctrl+Space
config.leader = { key = " ", mods = "CTRL", timeout_milliseconds = 2000 }

-- Reduce timeout to 1 second
config.leader = { key = "q", mods = "CTRL", timeout_milliseconds = 1000 }
```

**Important:** After changing the leader key, update all `mods = "LEADER"` keybindings to use your new leader.

---

## Troubleshooting

### Configuration Not Loading

**Symptom:** WezTerm doesn't apply custom settings or keybindings.

**Solutions:**
1. **Verify file paths:**
   ```powershell
   # Check if symlinks exist
   Get-Item "$env:USERPROFILE\.config\wezterm\*.lua" | Select-Object Target

   # Output should show paths to your repository files
   ```

2. **Check for syntax errors:**
   - Open WezTerm
   - Press `Ctrl+Shift+L` → Select "Show Debug Overlay"
   - Look for Lua errors in red text

3. **Manually reload configuration:**
   - Press `Ctrl+Shift+R`
   - Check debug overlay again

### WSL Shells Not Appearing

**Symptom:** WSL distributions missing from launcher menu.

**Solutions:**
1. **Verify WSL is installed:**
   ```powershell
   wsl --status
   ```

2. **Check distribution names:**
   ```powershell
   wsl -l -v
   # Compare names with those in wezterm.lua
   ```

3. **Update distribution names:**
   - Edit [wezterm.lua](./wezterm.lua)
   - Match `args = { "wsl.exe", "-d", "YourDistroName" }` to actual names
   - Press `Ctrl+Shift+R` to reload

4. **Ensure distributions are running:**
   ```powershell
   wsl -d Ubuntu-22.04
   # If it starts, distribution is working
   ```

### Keybindings Not Working

**Symptom:** Keybindings don't execute expected actions.

**Solutions:**
1. **Verify default keybindings are disabled:**
   - Check [wezterm.lua](./wezterm.lua) contains:
     ```lua
     config.disable_default_key_bindings = true
     ```

2. **Check for conflicts with Windows shortcuts:**
   - Some `Alt+Key` combinations may be captured by Windows
   - Try using alternative keybindings

3. **Test leader key:**
   - Press `Ctrl+Q`, then `W` (should show workspaces)
   - If nothing happens, check leader key configuration

4. **Verify keybinds.lua is loaded:**
   - Check debug overlay for errors mentioning `keybinds.lua`

### Tab Bar Icons Missing

**Symptom:** Tab bar shows squares or question marks instead of triangular icons.

**Solutions:**
1. **Install a Nerd Font:**
   - Download from: https://www.nerdfonts.com/
   - Recommended: JetBrains Mono Nerd Font, FiraCode Nerd Font

2. **Update font in configuration:**
   ```lua
   config.font = wezterm.font("JetBrainsMono Nerd Font")
   ```

3. **Reload configuration:**
   - Press `Ctrl+Shift+R`

### Copy Mode Not Entering

**Symptom:** Pressing `Leader+[` doesn't enter copy mode.

**Solutions:**
1. **Check leader key sequence:**
   - Press `Ctrl+Q` (you should see "LEADER" in status bar briefly)
   - Within 2 seconds, press `[`

2. **Verify copy mode keybinding:**
   - Check [keybinds.lua](./keybinds.lua) contains:
     ```lua
     { key = "[", mods = "LEADER", action = act.ActivateCopyMode },
     ```

3. **Check right status bar:**
   - Should display "TABLE: copy_mode" when active
   - If not visible, status bar might be hidden

---

## Tips & Best Practices

### Workspace Workflow

- **Project isolation:** Create separate workspaces for each project
  - `Leader+Shift+W` → Name: "frontend"
  - `Leader+Shift+W` → Name: "backend"
  - `Leader+W` → Switch between workspaces

- **Context switching:** Use workspaces to maintain mental context
  - "dev" workspace: code editor, test runner, file system
  - "ops" workspace: logs, monitoring, SSH sessions
  - "research" workspace: documentation, API testing

### Pane Layout Strategies

- **Development layout:**
  ```
  ┌─────────────┬─────┐
  │             │     │
  │   Editor    │ Git │
  │             │     │
  ├─────────────┤     │
  │   Server    │     │
  └─────────────┴─────┘
  ```
  - Split horizontally (`Ctrl+D`) for editor/server
  - Split vertically (`Ctrl+Shift+D`) for git sidebar

- **Debugging layout:**
  ```
  ┌─────────────┬─────┐
  │   Logs      │     │
  ├─────────────┤ App │
  │   Console   │     │
  └─────────────┴─────┘
  ```

### Copy Mode Efficiency

- **Quick copy:**
  1. `Leader+[` (enter copy mode)
  2. Navigate to start of text
  3. `V` (start selection)
  4. Navigate to end of text
  5. `Enter` (copy and exit)

- **Copy entire line:**
  1. `Leader+[` (enter copy mode)
  2. Navigate to line
  3. `Shift+V` (select line)
  4. `Enter` (copy and exit)

- **Copy command output:**
  1. `Leader+[` (enter copy mode)
  2. `gg` (go to top)
  3. `Shift+V` (line selection)
  4. `G` (extend to bottom)
  5. `Y` (copy all)

### Shell Switching

- **PowerShell ↔ WSL:**
  - `Ctrl+Shift+L` → Select "WSL (Ubuntu)"
  - Quickly switch between Windows and Linux environments

- **Multiple shells side-by-side:**
  - Split pane (`Ctrl+D`)
  - `Ctrl+Shift+L` in each pane to select different shells

### Font Size Adjustment

- **Presentations:**
  - `Ctrl++` multiple times to enlarge font for visibility
  - `Ctrl+0` to reset after presentation

- **Reading logs:**
  - `Ctrl+-` to fit more content on screen

---

## Additional Resources

- **WezTerm Official Documentation:** https://wezfurlong.org/wezterm/
- **WezTerm Keybinding Reference:** https://wezfurlong.org/wezterm/config/keys.html
- **WezTerm Color Schemes:** https://wezfurlong.org/wezterm/colorschemes/index.html
- **Lua Language Guide:** https://www.lua.org/manual/5.4/
- **Nerd Fonts:** https://www.nerdfonts.com/
- **WSL Documentation:** https://learn.microsoft.com/en-us/windows/wsl/

---

## License

This configuration is licensed under the MIT License - see the [LICENSE](../../../LICENSE) file for details.

**Copyright © 2026 kinamura**

---

**Happy terminal emulation!** 🚀
