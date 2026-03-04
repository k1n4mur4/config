# Dotfiles Configuration Repository

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![WezTerm](https://img.shields.io/badge/WezTerm-20230712+-green.svg)

A centralized dotfiles management repository for multiple operating systems, featuring terminal emulator configurations and development environment setups.

## Overview

This repository manages configuration files (dotfiles) across different operating systems using an OS-first directory structure. Each OS has its own dedicated directory containing application-specific configurations.

**Current Support:**
- Windows: WezTerm terminal emulator with Vim-inspired keybindings

**Planned Expansion:**
- macOS configurations
- Linux distributions (Ubuntu, Arch, Debian)

## Directory Structure

```
config/
├── windows/          # Windows-specific configurations
│   └── .config/
│       └── wezterm/  # WezTerm terminal emulator
│           ├── wezterm.lua      # Main configuration
│           ├── keybinds.lua     # Keybinding definitions
│           └── README.md        # Detailed Windows WezTerm guide
├── mac/              # macOS configurations (coming soon)
├── linux/            # Linux distribution-specific configs
│   ├── ubuntu/       # Ubuntu-specific configurations (coming soon)
│   ├── arch/         # Arch Linux configurations (coming soon)
│   └── debian/       # Debian configurations (coming soon)
├── LICENSE           # MIT License
└── README.md         # This file
```

**Organizational Philosophy:**
- **OS-first hierarchy**: Top-level directories organized by operating system
- **Home directory mirroring**: Each OS directory structure mirrors the target system's home directory layout
- **Application isolation**: Each application has its own subdirectory with comprehensive documentation

## Quick Navigation

| OS | Applications | Documentation |
|----|--------------|---------------|
| Windows | WezTerm | [Windows WezTerm Guide](./windows/.config/wezterm/README.md) |
| macOS | Coming soon | - |
| Linux (Ubuntu) | Coming soon | - |
| Linux (Arch) | Coming soon | - |
| Linux (Debian) | Coming soon | - |

## Prerequisites

### WezTerm Installation

This repository currently provides WezTerm terminal emulator configurations. Install WezTerm for your platform:

**Windows:**
```powershell
# Using winget (recommended)
winget install wez.wezterm

# Or download from: https://wezfurlong.org/wezterm/install/windows.html
```

**macOS:**
```bash
# Using Homebrew
brew install --cask wezterm
```

**Linux:**
```bash
# Ubuntu/Debian
curl -fsSL https://apt.fury.io/wez/gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/wezterm-fury.gpg
echo 'deb [signed-by=/usr/share/keyrings/wezterm-fury.gpg] https://apt.fury.io/wez/ * *' | sudo tee /etc/apt/sources.list.d/wezterm.list
sudo apt update
sudo apt install wezterm

# Arch Linux
sudo pacman -S wezterm

# Fedora
sudo dnf install wezterm

# Or download from: https://wezfurlong.org/wezterm/install/linux.html
```

**Version Requirements:**
- WezTerm 20230712 or later (required for workspace support, key tables, and modern features)

**Optional Dependencies:**
- **Nerd Fonts**: For enhanced tab bar icons and symbols
  - Recommended: JetBrains Mono Nerd Font, FiraCode Nerd Font
  - Install from: https://www.nerdfonts.com/
- **Git Bash** (Windows only): For Git Bash shell option in launcher menu
- **WSL2** (Windows only): For Linux distribution integration
  - Ubuntu, Kali Linux, or other distributions

## Installation

### General Guidelines

This repository uses **symbolic links** (symlinks) to connect configuration files to their expected locations. This approach offers several advantages:

- **Version control**: Changes are tracked in this repository
- **Easy updates**: Pull latest changes with `git pull`
- **No duplication**: Single source of truth for configurations
- **Cross-platform**: Works on Windows, macOS, and Linux

### OS-Specific Instructions

For detailed installation instructions specific to your operating system, refer to the corresponding OS-specific README:

- **Windows**: See [Windows WezTerm Guide](./windows/.config/wezterm/README.md) for detailed setup instructions
- **macOS**: Coming soon
- **Linux**: Coming soon

### Basic Installation Flow

1. **Clone this repository**
   ```bash
   git clone https://github.com/kinamura/config.git
   cd config
   ```

2. **Navigate to your OS directory**
   ```bash
   # Example for Windows
   cd windows
   ```

3. **Follow OS-specific README**
   - Each OS directory contains detailed instructions for creating symbolic links
   - Administrator/root privileges may be required for symlink creation

## Contributing

Contributions are welcome! Here's how you can help:

### Adding New OS Configurations

1. **Create OS directory** (if it doesn't exist)
   ```
   mkdir -p <os-name>/<application>
   ```

2. **Add configuration files**
   - Place your dotfiles in the appropriate subdirectory
   - Follow the home directory structure convention

3. **Create README**
   - Document installation instructions
   - List all features and keybindings
   - Include troubleshooting section
   - Provide customization examples

4. **Update main README**
   - Add entry to Quick Navigation table
   - Update Directory Structure section
   - Mention any new prerequisites

### Proposing Features or Reporting Issues

- **Issues**: Report bugs or request features on [GitHub Issues](https://github.com/kinamura/config/issues)
- **Pull Requests**: Submit improvements or new configurations via pull requests
- **Coding Style**:
  - Lua: Follow existing code formatting in `wezterm.lua` files
  - Markdown: Use GitHub-flavored Markdown
  - Comments: Add clear explanations for complex configurations

## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

**Copyright © 2026 kinamura**

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

---

**Happy configuring!** 🚀
