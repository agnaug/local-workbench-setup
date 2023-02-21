# Setting up local working environment
Contains a list of steps to complete in defined sequence.

## Get fonts required by oh-my-zsh theme
Refer to [installation guide](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k)

## Install brew and others
> Note: Assumes xcode-select already installed!

[Homebrew](https://brew.sh/) for package management.

```sh
# Install Homebrew:
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

```sh
# Add brew to PATH:
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
```

[Visual Studio Code](https://code.visualstudio.com/docs) as a dedicated IDE
```sh
# Install Visual Studio Code:
brew install --cask visual-studio-code
```
> Open VS Code and (on mac) use <kbd>⇧</kbd> + <kbd>⌃</kbd> + <kbd>P</kbd> to open shell command wizard and search for `Shell Command: Install 'code' command in PATH. It will allow you to open VS code from terminal at any folder with use of `code .` command.

----

Install [oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh/wiki) to `upgrade` your build-in mac zsh shell experience with something that supports command autocompletion, syntax highlighting (so you know if your command is a valid one even before you finish typing it!).

```sh
# Install oh-my-zsh:
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
> Now kill terminal and open a new terminal session!

```sh
# Install plugins:
# This assume use of oh-my-zsh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

Get some theme for your shell, [powerlevel10k](https://github.com/romkatv/powerlevel10k) is my favorite, but there are heaps of other choices.

```sh
# This assume use of oh-my-zsh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# Update your ~/.zshrc configuration:
sed -i '' 's/ZSH_THEME=".*"/ZSH_THEME="powerlevel10k\/powerlevel10k"/g' ~/.zshrc
sed -i '' 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/g' ~/.zshrc
```

> Now, kill your terminal again and upon new session p10k configuration will be auto enabled, follow the prompt to customize your shiny terminal. You can reconfigure this later by running `p10k configure`.

## Install pyenv and poetry
Get [pyenv](https://github.com/pyenv/pyenv) to manage version of python and virtual environments (match made in heaven!).

If mac M1/M2 might need to get a missing dependency for successful python installation:

```sh
brew install xz

# Get pyenv:
brew install pyenv

# Add pyenv to PATH:
echo '' >> ~/.zshrc
echo '# Add pyenv to PATH'  >> ~/.zshrc
echo 'eval "$(pyenv init -)"'  >> ~/.zshrc

# Try to get a specific python version:
pyenv install 3.9
pyenv global 3.9
```

Once you successfully get pyenv, get [poetry](https://python-poetry.org/docs/) for dependency management and your code packaging (if you ever what to package your code in a wheel).

```sh
# Make POETRY_HOME:
mkdir -p ~/etc/poetry
echo '' >> ~/.zshrc
echo 'Add poetry HOME' >> ~/.zshrc
echo 'export POETRY_HOME=~/etc/poetry' >> ~/.zshrc
echo 'export PATH="$POETRY_HOME/bin:$PATH"' >> ~/.zshrc

# Setup poetry autocompletion:
mkdir $ZSH_CUSTOM/plugins/poetry
poetry completions zsh > $ZSH_CUSTOM/plugins/poetry/_poetry

# Modify plugins:
sed -i '' 's/plugins=(.*)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting poetry)/g' ~/.zshrc

# List your current settings
poetry config --list 

# Update poetry settings to always create .venv inside each of your projects
poetry config virtualenvs.in-project true
```

### Add vs code extensions
* streetsidesoftware.code-spell-checker