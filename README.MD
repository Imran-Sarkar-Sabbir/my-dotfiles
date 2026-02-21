# Dotfiles

Manage configuration files across macOS and Linux using [GNU Stow](https://www.gnu.org/software/stow/).

Stow creates symlinks from this repo into your home directory, so your configs stay version-controlled and portable.

## Prerequisites

**macOS**

```sh
brew install stow
```

**Linux (Debian/Ubuntu)**

```sh
sudo apt install stow
```

**Linux (Fedora)**

```sh
sudo dnf install stow
```

**Linux (Arch)**

```sh
sudo pacman -S stow
```

## Setup

Clone this repo into your home directory:

```sh
git clone <your-repo-url> ~/dotfiles
```

Run the setup script:

```sh
cd ~/dotfiles
./setup.sh
```

This runs `stow .` which symlinks everything in the repo to the corresponding path under `~/`.

## How Stow Works

Stow mirrors the directory structure of a package into a target directory (default: parent directory).

For example, if your repo looks like this:

```
~/dotfiles/
  .config/
    nvim/
      init.lua
  .zshrc
  .gitconfig
```

Running `stow .` from `~/dotfiles` creates:

```
~/.config/nvim/init.lua  ->  ~/dotfiles/.config/nvim/init.lua
~/.zshrc                 ->  ~/dotfiles/.zshrc
~/.gitconfig             ->  ~/dotfiles/.gitconfig
```

Your actual files live in the repo. The home directory just has symlinks pointing back to them.

## Adding New Configs

1. Move the config file into this repo, preserving the path relative to `~`:

   ```sh
   # example: track your zsh config
   mv ~/.zshrc ~/dotfiles/.zshrc
   ```

2. Re-run stow to create the symlink:

   ```sh
   cd ~/dotfiles
   stow .
   ```

3. Commit and push:

   ```sh
   git add .zshrc
   git commit -m "Add zshrc"
   git push
   ```

## Removing Symlinks

To unlink everything stow created:

```sh
cd ~/dotfiles
stow -D .
```

## Tips

- Add a `.stow-local-ignore` file to exclude files from being symlinked (e.g., `README.MD`, `setup.sh`).
- Use `stow -n .` for a dry run to preview what symlinks would be created.
- If stow reports conflicts, the target file already exists and isn't a symlink. Back it up or remove it first.
