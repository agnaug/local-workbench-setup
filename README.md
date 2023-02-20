# Setting up local working environment
Contains a list of steps to complete in defined sequence.

## Get fonts required by oh-my-zsh theme
Refer to [installation guide](https://github.com/romkatv/powerlevel10k#meslo-nerd-font-patched-for-powerlevel10k)

## Install brew and others
> Note: Assumes xcode-select already installed!

```sh
# Install Homebrew:
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

```sh
# Add brew to PATH:
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
```

```sh
# Install Visual Studio Code:
brew install --cask visual-studio-code
```
> Open vs code and make sure to add `code` command to your PATH!

```sh
# Install oh-my-zsh:
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
> Now kill terminal and open a new terminal session!

```sh
# Install plugins:
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions


# Install theme:
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k


# Update your ~/.zshrc configuration:
sed -i '' 's/ZSH_THEME=".*"/ZSH_THEME="powerlevel10k\/powerlevel10k"/g' ~/.zshrc
sed -i '' 's/plugins=(git)/plugins=(git zsh-autosuggestions zsh-syntax-highlighting)/g' ~/.zshrc
```

> Now, kill your terminal again and upon new session p10k configuration will be auto enabled, select your choices.

## Install pyenv and poetry
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


Poetry depends on successful pyenv installation 
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
```

### Add vs code extensions
* streetsidesoftware.code-spell-checker