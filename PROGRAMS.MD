# Programs & Dependencies

All the programs and tools used by this dotfiles setup.

---

## 01. Oh My Zsh

Framework for managing Zsh configuration.

**Install:**

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

**Plugins:**

```bash
# zsh-autosuggestions — suggests commands as you type based on history
git clone https://github.com/zsh-users/zsh-autosuggestions.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-syntax-highlighting — highlights valid/invalid commands in the terminal
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# fast-syntax-highlighting — faster, feature-rich syntax highlighting
git clone https://github.com/zdharma-continuum/fast-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
```

**Theme (pixegami-agnoster):**

```bash
git clone https://github.com/pixegami/terminal-profile.git /tmp/pixegami-terminal-profile
cp /tmp/pixegami-terminal-profile/configs/pixegami-agnoster.zsh-theme ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/
rm -rf /tmp/pixegami-terminal-profile
```

**Usage:** Configuration is loaded automatically on shell startup via `source ~/.profile` and `source $ZSH/oh-my-zsh.sh` in `.zshrc`.

**Config:** [`.zshrc`](.zshrc)

---

## 02. Tmux

Terminal multiplexer — run multiple terminal sessions in one window.

**Install:**

```bash
brew install tmux
```

**Plugin Manager (TPM):**

```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

After installing, open tmux and press `prefix + I` to fetch and install plugins.

**Plugins included:**
- `tmux-resurrect` — save and restore tmux sessions
- `tmux-continuum` — automatic session saving and restore on tmux start

**Key bindings (custom):**

| Keys | Action |
|---|---|
| `Ctrl-a` | Prefix (remapped from `Ctrl-b`) |
| `prefix + \|` | Split pane horizontally |
| `prefix + -` | Split pane vertically |
| `prefix + r` | Reload config |
| `prefix + K` | Kill a session (choose from list) |
| `Ctrl-h/j/k/l` | Navigate panes (vim-style, works with nvim splits) |
| `Ctrl-Alt-l` | Clear screen and scrollback history |

**Usage:**

```bash
tmux          # start new session (alias: t)
tmux a        # attach to last session (alias: ta)
```

**Config:** [`.tmux.conf`](.tmux.conf)

---

## 03. Neovim

Hyperextensible Vim-based text editor. Uses [LazyVim](https://www.lazyvim.org/) as the configuration framework.

**Install:**

```bash
brew install neovim
```

**Usage:**

```bash
nvim          # open neovim (alias: nv)
```

LazyVim plugins are auto-installed on first launch.

**Config:** [`.config/nvim/`](.config/nvim/)

---

## 04. Alacritty

GPU-accelerated terminal emulator.

**Install:**

```bash
brew install --cask alacritty
```

**Alacritty themes (includes pixegami theme):**

Themes are bundled in this repo at `.config/alacritty/themes/`. They are symlinked into place by GNU Stow along with the rest of the dotfiles.

**Usage:** Launch Alacritty from Spotlight or your application launcher. It starts maximized with no title bar decorations.

**Config:** [`.config/alacritty/`](.config/alacritty/)

---

## 05. Fonts

Programming fonts used by the terminal and editor.

**Install:**

```bash
brew install --cask font-anonymous-pro
brew install --cask font-jetbrains-mono
brew install font-hack-nerd-font
brew install --cask font-meslo-lg-nerd-font
```

**Usage:** Configured automatically in `alacritty.toml`. Anonymous Pro is the default regular font, JetBrains Mono is used for bold.

---

## 06. Lazygit

Simple terminal UI for git.

**Install:**

```bash
brew install lazygit
```

**Usage:**

```bash
lazygit       # open lazygit (alias: lg)
```

---

## 07. bat

A `cat` clone with syntax highlighting and line numbers.

**Install:**

```bash
brew install bat
```

**Usage:**

```bash
bat file.txt  # view file with syntax highlighting (alias adds --color=always --style=numbers)
```

Also used automatically by the `fzf` alias for file previews.

---

## 08. fzf

Command-line fuzzy finder.

**Install:**

```bash
brew install fzf
```

**Usage:**

```bash
fzf           # fuzzy find files (alias adds bat preview)
Ctrl+e        # fuzzy find a file and open it in Neovim (keybinding in .zshrc)
```

---

## 09. fd

A fast alternative to `find`.

**Install:**

```bash
brew install fd
```

**Usage:**

```bash
fd pattern    # find files matching pattern (alias: fd maps to fdfind)
```

---

## 10. GNU Stow

Symlink farm manager — used to deploy these dotfiles.

**Install:**

```bash
brew install stow
```

**Usage:**

```bash
cd ~/dotfiles
stow .        # create symlinks into $HOME (or run ./setup.sh)
stow -D .     # remove symlinks
stow -n .     # dry run — preview what would be linked
```

Files listed in `.stow-local-ignore` (like `README.MD`, `setup.sh`) are excluded from symlinking.

---

## 11. NVM

Node Version Manager — manage multiple Node.js versions.

**Install:**

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

**Usage:**

```bash
nvm install --lts    # install latest LTS
nvm use --lts        # use latest LTS
nvm ls               # list installed versions
```
