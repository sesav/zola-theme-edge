+++
title = "Essential Command-Line Tools for Developer Productivity"
date = 2024-09-18
[taxonomies]
tags=["development", "tools"]
categories=["tools"]
+++

The command line is a developer's secret weapon for productivity. While GUI tools have their place, mastering these CLI tools can dramatically speed up your workflow and make you a more efficient developer.

## File and Directory Navigation

### exa - A Modern ls Replacement
```bash
# Install
brew install exa  # macOS
sudo apt install exa  # Ubuntu

# Usage
exa -la --git --icons  # Detailed view with git status
exa -T  # Tree view
alias ls='exa --icons'  # Replace ls
```

### fd - A Fast find Alternative
```bash
# Install
brew install fd  # macOS
sudo apt install fd-find  # Ubuntu

# Usage
fd config  # Find files containing "config"
fd -e js  # Find all JavaScript files
fd -t d node_modules  # Find directories named node_modules
```

### bat - Enhanced cat with Syntax Highlighting
```bash
# Install
brew install bat  # macOS
sudo apt install bat  # Ubuntu

# Usage
bat script.js  # View file with syntax highlighting
bat -A file.txt  # Show all characters including whitespace
alias cat='bat'  # Replace cat
```

## Text Processing and Search

### ripgrep (rg) - Blazingly Fast grep
```bash
# Install
brew install ripgrep  # macOS
sudo apt install ripgrep  # Ubuntu

# Usage
rg "TODO" --type js  # Search for TODO in JavaScript files
rg -i "error" logs/  # Case-insensitive search in logs directory
rg -n "function.*async"  # Show line numbers for async functions
```

### fzf - Fuzzy Finder
```bash
# Install
brew install fzf  # macOS
sudo apt install fzf  # Ubuntu

# Setup key bindings
$(brew --prefix)/opt/fzf/install  # macOS

# Usage
vim $(fzf)  # Open file in vim using fuzzy search
kill -9 $(ps aux | fzf | awk '{print $2}')  # Kill process interactively
git checkout $(git branch | fzf)  # Checkout branch interactively
```

### jq - JSON Processor
```bash
# Install
brew install jq  # macOS
sudo apt install jq  # Ubuntu

# Usage
curl api.github.com/users/octocat | jq '.name'
cat package.json | jq '.dependencies | keys[]'
echo '{"name": "John", "age": 30}' | jq -r '.name'
```

## System Monitoring and Process Management

### htop - Interactive Process Viewer
```bash
# Install
brew install htop  # macOS
sudo apt install htop  # Ubuntu

# Usage
htop  # Interactive process monitor
htop -u username  # Show processes for specific user
```

### ncdu - Disk Usage Analyzer
```bash
# Install
brew install ncdu  # macOS
sudo apt install ncdu  # Ubuntu

# Usage
ncdu /  # Analyze disk usage from root
ncdu ~/Downloads  # Analyze specific directory
```

### glances - System Monitor
```bash
# Install
pip install glances

# Usage
glances  # Comprehensive system monitoring
glances -w  # Web interface mode
```

## Git and Version Control

### tig - Text-mode Interface for Git
```bash
# Install
brew install tig  # macOS
sudo apt install tig  # Ubuntu

# Usage
tig  # Browse repository history
tig status  # Interactive git status
tig blame filename  # Interactive git blame
```

### gh - GitHub CLI
```bash
# Install
brew install gh  # macOS
sudo apt install gh  # Ubuntu

# Usage
gh repo create my-project --private
gh pr create --title "Fix bug" --body "Description"
gh issue list --assignee @me
```

### lazygit - Simple Terminal UI for Git
```bash
# Install
brew install lazygit  # macOS

# Usage
lazygit  # Interactive git interface
```

## Network and Web Tools

### httpie - User-friendly HTTP Client
```bash
# Install
brew install httpie  # macOS
sudo apt install httpie  # Ubuntu

# Usage
http GET api.github.com/users/octocat
http POST httpbin.org/post name=John age:=30
http --auth user:pass GET api.example.com/data
```

### curl with Modern Alternatives

### xh - Fast and Friendly HTTP Client
```bash
# Install
brew install xh  # macOS

# Usage (similar to httpie but faster)
xh GET httpbin.org/json
xh POST httpbin.org/post name=John
```

## Development Tools

### docker and docker-compose Shortcuts
```bash
# Useful aliases
alias dps='docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"'
alias dcu='docker-compose up -d'
alias dcd='docker-compose down'
alias dcl='docker-compose logs -f'
```

### nvm - Node Version Manager
```bash
# Install
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# Usage
nvm install 18  # Install Node.js v18
nvm use 16  # Switch to Node.js v16
nvm ls  # List installed versions
```

### pyenv - Python Version Manager
```bash
# Install
curl https://pyenv.run | bash

# Usage
pyenv install 3.11.0  # Install Python 3.11.0
pyenv global 3.11.0  # Set global Python version
pyenv versions  # List installed versions
```

## Terminal Enhancements

### zsh with Oh My Zsh
```bash
# Install Oh My Zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Useful plugins in ~/.zshrc
plugins=(git docker kubectl z fzf)
```

### Starship - Cross-shell Prompt
```bash
# Install
curl -sS https://starship.rs/install.sh | sh

# Add to shell config
echo 'eval "$(starship init zsh)"' >> ~/.zshrc
```

### tmux - Terminal Multiplexer
```bash
# Install
brew install tmux  # macOS
sudo apt install tmux  # Ubuntu

# Basic usage
tmux new -s mysession  # Create new session
tmux attach -t mysession  # Attach to session
Ctrl-b d  # Detach from session
Ctrl-b c  # Create new window
```

## Productivity Aliases and Functions

Add these to your `.zshrc` or `.bashrc`:

```bash
# Navigation
alias ..='cd ..'
alias ...='cd ../..'
alias l='exa -la --git --icons'
alias ll='exa -la --git --icons'

# Git shortcuts
alias gs='git status'
alias ga='git add'
alias gc='git commit -m'
alias gp='git push'
alias gl='git pull'

# Docker shortcuts
alias d='docker'
alias dc='docker-compose'

# Quick edit configs
alias zshrc='vim ~/.zshrc'
alias vimrc='vim ~/.vimrc'

# Network
alias myip='curl ipinfo.io/ip'
alias ports='netstat -tuln'

# Utilities
mkcd() { mkdir -p "$1" && cd "$1"; }
extract() {
  if [ -f $1 ] ; then
    case $1 in
      *.tar.bz2)   tar xjf $1     ;;
      *.tar.gz)    tar xzf $1     ;;
      *.bz2)       bunzip2 $1     ;;
      *.rar)       unrar e $1     ;;
      *.gz)        gunzip $1      ;;
      *.tar)       tar xf $1      ;;
      *.tbz2)      tar xjf $1     ;;
      *.tgz)       tar xzf $1     ;;
      *.zip)       unzip $1       ;;
      *.Z)         uncompress $1  ;;
      *.7z)        7z x $1        ;;
      *)     echo "'$1' cannot be extracted via extract()" ;;
    esac
  else
    echo "'$1' is not a valid file"
  fi
}
```

## Installation Script

Save this as `setup-cli-tools.sh`:

```bash
#!/bin/bash
# CLI Tools Installation Script

# Detect OS
if [[ "$OSTYPE" == "darwin"* ]]; then
    # macOS
    brew install exa fd bat ripgrep fzf jq htop ncdu tig gh httpie
elif [[ "$OSTYPE" == "linux-gnu"* ]]; then
    # Ubuntu/Debian
    sudo apt update
    sudo apt install -y exa fd-find bat ripgrep fzf jq htop ncdu tig httpie
    
    # Install gh CLI
    curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo gpg --dearmor -o /usr/share/keyrings/githubcli-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
    sudo apt update
    sudo apt install gh
fi

# Install language version managers
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
curl https://pyenv.run | bash

# Install Starship prompt
curl -sS https://starship.rs/install.sh | sh

echo "CLI tools installation complete! Restart your terminal to use the new tools."
```

## Tips for Mastery

1. **Start with one tool at a time** - Don't overwhelm yourself
2. **Create aliases** for frequently used commands
3. **Learn keyboard shortcuts** for your terminal
4. **Practice regularly** - consistency is key
5. **Customize your setup** - make it yours

The command line becomes incredibly powerful when you combine these tools. Start with the basics and gradually incorporate more tools into your workflow as you become comfortable.

Remember: the goal isn't to use every tool, but to find the ones that make **you** more productive!