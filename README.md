# Level up your Mac Terminal

Wanna have the best looking Mac Terminal? I got you ;)

This guide goes straight into the commands for tool installation. For those seeking more in-depth insights, I've included direct links to the original websites.

Since macOS Catalina (10.15.2) the default shell is now Zsh instead of Bash; therefore, this guide assumes you are using Zsh already.

### 1. [Homebrew](https://brew.sh/)

Homebrew it's a command line tool used for installing apps. It will be needed later for installation of other tools. To install run the following command:

```bash
/bin/bash -c '$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)'
```

Add Homebrew to the system path to be able to run the command on the terminal.

```bash
echo 'export PATH=$PATH:/opt/homebrew/bin' >> ~/.zshrc
```

Apply changes on your system.

```bash
source ~/.zshrc
```

### 2. [iTerm2](https://iterm2.com/)

iTerm2 is a replacement for Terminal, the default terminal that comes installed on Macs. To install run the following command:

```bash
brew install --cask iterm2
```

### 3. [Dracula](https://draculatheme.com/iterm)

One of my favourite themes for iTerm2. No sponsorship, I swear!

Clone the repository or download it manually using the [GitHub .zip download](https://github.com/dracula/iterm/archive/master.zip) option.

```bash
git clone https://github.com/dracula/iterm.git
```

Then follow the steps below:

- *iTerm2 > Preferences > Profiles > Colors Tab*
- Open the *Color Presets...* drop-down in the bottom right corner
- Select *Import...* from the list
- Select the `Dracula.itermcolors` file
- Select the *Dracula* from *Color Presets...*

> **Note**: Colors may not be correctly displayed by the `ls` command. This will be fixed on the next step.

### 4. [gdircolors](https://man7.org/linux/man-pages/man1/dircolors.1.html)

Homebrew installs GNU [`coreutils`](https://www.gnu.org/software/coreutils/) with a `'g'` prefix. The `dircolors`, or in this case, `gdircolors` is used to setup the colors applied to the `ls` command.

```bash
brew install coreutils
```

Clone the repository or download it manually using the [GitHub .zip download](https://github.com/seebi/dircolors-solarized/archive/refs/heads/master.zip) option.

```bash
git clone git@github.com:seebi/dircolors-solarized.git
```

Create a config directory for `dircolors` and move the [`dircolors.ansi-dark`](https://github.com/seebi/dircolors-solarized/blob/master/dircolors.ansi-dark).

```
mkdir -p ~/.config/dircolors
mv dircolors-solarized/dircolors.ansi-dark ~/.config/dircolors
```

Use the [`dircolors.ansi-dark`](https://github.com/seebi/dircolors-solarized/blob/master/dircolors.ansi-dark) color format on `gdircolors` and override `ls` command to use `gls` instead.

```bash
echo 'eval $(gdircolors ~/.config/dircolors/dircolors.ansi-dark)' >> ~/.zshrc
echo 'alias ls="gls --color=auto --group-directories-first"' >> ~/.zshrc 
```

Apply changes on your system.

```bash
source ~/.zshrc
```

### 5. [Oh My Zsh](https://ohmyz.sh/)

Oh My Zsh is a framework for managing your Zsh configuration. It will boost your productivity with nice plugins and make your terminal look pretty. To install run the following command:

```bash
sh -c '$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)'
```

Oh My Zsh seems to change the directory colors for auto completion, to fix add the following lines to the `~/.zshrc` file.

```bash
echo 'zstyle ":completion:*" list-colors "${(@s.:.)LS_COLORS}"' >> ~/.zshrc 
echo 'autoload -Uz compinit' >> ~/.zshrc
echo 'compinit' >> ~/.zshrc
```

Apply changes on your system.

```bash
source ~/.zshrc
```

### 6. [Powerlevel10k](https://github.com/romkatv/powerlevel10k)

Powerlevel10k is a theme for Zsh. It emphasizes speed, flexibility and out-of-the-box experience. To install run the following command:

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Then set `ZSH_THEME="powerlevel10k/powerlevel10k"` in `~/.zshrc`, and start a new terminal session.

### 7. [Zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

It suggests commands as you type based on history and completions. To install run the following command:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Then add the plugin to the list of plugins inside `~/.zshrc`, and start a new terminal session.

```bash
plugins=( 
    # other plugins...
    zsh-autosuggestions
)
```

### 8. [Zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

It provides syntax highlighting, red for invalid and green for valid commands. To install run the following command:

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

Then add the plugin to the list of plugins inside `~/.zshrc`, and start a new terminal session.

```bash
plugins=( 
    # other plugins...
    zsh-syntax-highlighting
)
```

### 9. [Tree](https://mama.indstate.edu/users/ice/tree/) 

It lists content of directories in tree-like format. To install run the following command:

```bash
brew install tree
```

### 10. [Colorls](https://github.com/athityakumar/colorls)

A Ruby script that colorizes the `ls` output with color and icons. First install a version manager tool for Ruby with:

```bash
brew install rbenv ruby-build
```

Then to load rbenv automatically, append the following to `~/.zshrc`, and start a new terminal session.

```bash
echo 'eval "$(rbenv init - zsh)"' >> ~/.zshrc
```

Install Ruby `3.0.6`, but feel free to install any other as long as version >= 2.6. 

```bash
rbenv install 3.0.6
```

Set Ruby `3.0.6` as global to be used in all shells with:

```bash
rbenv global 3.0.6
```

Install the colorls ruby gem with:

```bash
gem install colorls
```

> **Note**: `colorls` doesn't obey the `ls` output color format, instead it uses a fixed theme. Next step will fix it.

### 11. [Dracula Colorls](https://draculatheme.com/colorls)

Clone the repository or download it manually using the [GitHub .zip download](https://github.com/dracula/colorls/archive/master.zip) option.

```bash
git clone git@github.com:dracula/colorls.git
```

Copy the [`dark_colors.yaml`](https://github.com/dracula/colorls/blob/master/dark_colors.yaml) file to the dark color scheme location for `colorls`.

```bash
cp dark_colors.yaml ~/.config/colorls/dark_colors.yaml
```

Finally add some alias in `~/.zshrc`.

- `lc` shows the file view with directories first, followed by files.
- `tc` shows tree view with directories first, followed by files.

```bash
echo 'alias lc="colorls --sd --dark"' >> ~/.zshrc
echo 'alias tc="colorls --tree --sd --dark"' >> ~/.zshrc
```

