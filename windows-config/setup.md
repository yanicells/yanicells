## Windows and WSL
- Install Python
- Install NVM
- Install Node.js LTS via NVM
- Install Git for Windows
- Set up SSH keys and add to GitHub
- Install bun (optional)
- Install tree (for project structure visualization)

## VS Code Setup Guide
- Install all my extensions
- Import settings from `vscode-settings.json`
- Set up keybindings from `vscode-keybindings.json`
- Download JetBrains Mono font and set it as the default font in settings, and terminal settings.
- Download it from JetBrains website, extract the zip, and install all TTF files.
- Have default terminal as git bash or WSL depending on the project.
- Configure WSL: Ubuntu as remote window (found in bottom left corner of VS Code).

## Code Setup Guide
- For cursor, import settings from VS Code settings.
- Edit the font family to "JetBrains Mono", font size and font family
- Set WSL as remove window.
- When using WSL as remote window, make sure to install the extensions in the WSL window as well.
- Setup AI tools. Claude Code, and Warp
- Install bun on WSL and windows. 

## Additional Reminders

- Add two directories in my explorer quick access, one for where I use git bash and one for where I use WSL.
- To ensure that the title tab title does not change for any terminal, go to settings, select the terminal profile (Git Bash, Ubuntu), click on Terminal Emulation, and turn on "Supress title changes."
- In the profile, go to appearance, set Scrollbar visibility to Hidden
- In Launch Parameters, launch mode to default, launch position at 0, 0, and center on launch to off. On startup, set to maximized.

## Windows Settings Tweaks
- Set dark mode for system and apps.
- Hide taskbar in settings.
- Download flow launcher and set it up.
- Add alt walker plugin to flow launcher. (research on everything search)
- Flow launcher: disable animation and sound in settings, launch on startup, double check the Pinyin searching.

# Terminal Setup Guide

## Prerequisites
- Windows terminal installed
- Git for Windows installed
- WSL2 with Ubuntu installed

## 1. Clone Settings Repo
```bash
git clone https://github.com/yanicells/yanicells.git
cd yanicells
```

## 2. PowerShell Setup

**Copy profile:**
```powershell
# Create profile directory if needed
New-Item -Path "$HOME\Documents\WindowsPowerShell" -ItemType Directory -Force

# Copy profile
Copy-Item "powershell-profile.ps1" "$HOME\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1"
```

## 3. Git Bash Setup

**Install fastfetch:**
```bash
# Download from https://github.com/fastfetch-cli/fastfetch/releases
# Extract and add to PATH or place in Git installation folder
```

**Copy fastfetch config:**
```bash
mkdir -p ~/.config/fastfetch
cp fastfetch-config.jsonc ~/.config/fastfetch/config.jsonc
cp fastfetch-ascii.txt ~/.config/fastfetch/ascii.txt
```

**Set tab title:**
```bash
touch ~/.bashrc
echo 'PROMPT_COMMAND='"'"'echo -ne "\033]0;Git Bash\007"'"'"'' >> ~/.bashrc
```

## 4. Ubuntu (WSL) Setup

**Install essentials:**
```bash
sudo apt update
sudo apt install git zsh -y

# Install fastfetch
sudo add-apt-repository ppa:zhangsongcui3371/fastfetch -y
sudo apt update
sudo apt install fastfetch -y
```

**Install Oh My Zsh:**
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

**Install Powerlevel10k:**
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

sed -i 's/ZSH_THEME=".*"/ZSH_THEME="powerlevel10k\/powerlevel10k"/' ~/.zshrc
```

**Copy fastfetch config:**
```bash
mkdir -p ~/.config/fastfetch
cp /mnt/c/path/to/yanicells/fastfetch-config.jsonc ~/.config/fastfetch/config.jsonc
cp /mnt/c/path/to/yanicells/fastfetch-ascii.txt ~/.config/fastfetch/ascii.txt
```

**Configure .zshrc:**
```bash
echo 'typeset -g POWERLEVEL9K_INSTANT_PROMPT=quiet' | cat - ~/.zshrc > temp && mv temp ~/.zshrc
echo 'fastfetch' >> ~/.zshrc
echo 'DISABLE_AUTO_TITLE="true"' >> ~/.zshrc
echo 'precmd() { echo -ne "\033]0;Ubuntu\007" }' >> ~/.zshrc
```

**Set Zsh as default:**
```bash
chsh -s $(which zsh)
```

**Setup SSH (reuse existing key):**
```bash
mkdir -p ~/.ssh
# Copy your existing id_ed25519 and id_ed25519.pub to ~/.ssh/
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

# Test
ssh -T git@github.com
```

## 5. Windows Terminal Config

**Copy settings:**
```bash
# Open Windows Terminal settings (Ctrl+,)
# Copy JSON from terminal-settings.json into your settings
# Or manually configure profiles for PowerShell, Git Bash, and Ubuntu
```

**Key profile settings:**

**Git Bash:**
```jsonc
{
    "commandline": "C:\\Program Files\\Git\\bin\\bash.exe -c \"fastfetch; exec bash\"",
    "name": "Git Bash",
    "startingDirectory": "C:\\Users\\YourUsername\\Documents",
    "tabTitle": "Git Bash"
}
```

**Ubuntu:**
```jsonc
{
    "commandline": "wsl.exe -d Ubuntu --cd \"~/dev\" -- zsh -c \"fastfetch; exec zsh\"",
    "name": "Ubuntu",
    "tabTitle": "Ubuntu"
}
```

## Done!
Restart all terminals to apply changes.