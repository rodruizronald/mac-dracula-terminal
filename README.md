Are you a [Dracula Theme](https://draculatheme.com/) lover? I got you! Have a look at the end result.

![alt](https://cdn.hashnode.com/res/hashnode/image/upload/v1693078815691/fo8K1vgtf.png?auto=format)

![alt](https://cdn.hashnode.com/res/hashnode/image/upload/v1693078887684/jAP4qtnZ9.png?auto=format)

![alt](https://cdn.hashnode.com/res/hashnode/image/upload/v1693078904005/mGCBVOqiD.png?auto=format)

![alt](https://cdn.hashnode.com/res/hashnode/image/upload/v1693078919206/EATbfqdJn.png?auto=format)

This guide goes straight into the commands for tool installation. For those seeking more in-depth insights, I've included direct links to the original websites.

Since macOS Catalina (10.15.2) the default shell is now Zsh instead of Bash; therefore, this guide assumes you are using Zsh already.

### 1\. [Homebrew](https://brew.sh/)

Homebrew it's a command line tool used for installing apps. It will be needed later for the installation of other tools.

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

To enable it, run the following command on the terminal.

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
```

Apply changes to your system.

```bash
source ~/.zprofile
```

### 2\. [iTerm2](https://iterm2.com/)

iTerm2 is a replacement for Terminal, the default terminal that comes installed on Macs.

```bash
brew install --cask iterm2
```

### 3\. [Dracula](https://draculatheme.com/iterm)

One of my favourite themes for iTerm2.

Clone the repository or download it manually using the [GitHub .zip download](https://github.com/dracula/iterm/archive/master.zip) option.

```bash
git clone https://github.com/dracula/iterm.git
```

Then follow the steps below:

* *iTerm2 &gt; Preferences &gt; Profiles &gt; Colors Tab*
    
* Open the *Color Presets...* drop-down in the bottom right corner
    
* Select *Import...* from the list
    
* Select the `Dracula.itermcolors` file
    
* Select the *Dracula* from *Color Presets...*
    

### 4\. [Oh My Zsh](https://ohmyz.sh/)

Oh-My-Zsh is a framework for managing your Zsh configuration. It will boost your productivity with nice plugins and make your terminal look pretty.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### 5\. [gdircolors](https://man7.org/linux/man-pages/man1/dircolors.1.html)

Homebrew installs GNU [`coreutils`](https://www.gnu.org/software/coreutils/) with a 'g' prefix. The `dircolors`, or in this case, `gdircolors` are used to set up the colours applied to the `ls` command.

```bash
brew install coreutils
```

Clone the repository or download it manually using the [GitHub .zip download](https://github.com/seebi/dircolors-solarized/archive/refs/heads/master.zip) option.

```bash
git clone https://github.com/seebi/dircolors-solarized.git
```

Create a config directory for `dircolors` and move the [`dircolors.ansi-dark`](https://github.com/seebi/dircolors-solarized/blob/master/dircolors.ansi-dark).

```plaintext
mkdir -p ~/.config/dircolors
cp dircolors-solarized/dircolors.ansi-dark ~/.config/dircolors
```

Use the [`dircolors.ansi-dark`](https://github.com/seebi/dircolors-solarized/blob/master/dircolors.ansi-dark) color format on `gdircolors` and override `ls` command to use `gls` instead.

```bash
echo 'eval "$(gdircolors ~/.config/dircolors/dircolors.ansi-dark)"' >> ~/.zshrc
echo 'alias ls="gls --color=auto --group-directories-first"' >> ~/.zshrc
```

Oh-My-Zsh seems to change the colours for auto-completion. Add the following lines to the `~/.zshrc` file.

```bash
echo 'zstyle ":completion:*" list-colors "${(@s.:.)LS_COLORS}"' >> ~/.zshrc 
echo 'autoload -Uz compinit' >> ~/.zshrc
echo 'compinit' >> ~/.zshrc
```

Apply changes to your system.

```bash
source ~/.zshrc
```

### 6\. [Powerlevel10k](https://github.com/romkatv/powerlevel10k)

Powerlevel10k is a theme for Zsh. It emphasizes speed, flexibility and out-of-the-box experience.

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Then set `ZSH_THEME="powerlevel10k/powerlevel10k"` in `~/.zshrc`, and start a new terminal session.

### 7\. [Zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)

It suggests commands as you type based on history and completions.

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

### 8\. [Zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)

It provides syntax highlighting, red for invalid and green for valid commands.

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

### 9\. [Tree](https://mama.indstate.edu/users/ice/tree/)

It lists the content of directories in a tree-like format.

```bash
brew install tree
```

### 10\. [Colorls](https://github.com/athityakumar/colorls)

A Ruby script that colourizes the `ls` output with colour and icons. First install a version manager tool for Ruby with:

```bash
brew install rbenv ruby-build
```

Then to load rbenv automatically, append the following to `~/.zprofile`, and start a new terminal session.

```bash
echo 'eval "$(rbenv init - zsh)"' >> ~/.zprofile
```

Apply changes to your system.

```bash
source ~/.zprofile
```

Install Ruby `3.0.6`, but feel free to install any other as long as version &gt;= 2.6.

```bash
rbenv install 3.0.6
```

Set Ruby `3.0.6` as global to be used in all shells with:

```bash
rbenv global 3.0.6
```

Install the `colorls` ruby gem with:

```bash
gem install colorls
```

> **Note**: `colorls` doesn't obey the `ls` output color format, instead, it uses a fixed theme. The next step will fix it.

### 11\. [Dracula Colorls](https://draculatheme.com/colorls)

Clone the repository or download it manually using the [GitHub .zip download](https://github.com/dracula/colorls/archive/master.zip) option.

```bash
git clone https://github.com/dracula/colorls.git
```

Copy the [`dark_colors.yaml`](https://github.com/dracula/colorls/blob/master/dark_colors.yaml) file to the dark colour scheme location for `colorls`.

```bash
mkdir -p ~/.config/dircolors
cp colorls/dark_colors.yaml ~/.config/colorls
```

Finally, add some aliases in `~/.zprofile`

* `lc` shows the file view with directories first, followed by files.
    
* `tc` shows a tree view with directories first, followed by files.
    

```bash
echo 'alias lc="colorls --sd --dark"' >> ~/.zprofile
echo 'alias tc="colorls --tree --sd --dark"' >> ~/.zprofile
```

Apply changes to your system.

```bash
source ~/.zprofile
```