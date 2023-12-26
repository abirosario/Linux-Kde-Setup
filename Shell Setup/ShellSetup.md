# Shell Setup with ZSH

This guide will walk you through setting up ZSH as your default shell on your system.

## ZSH

### Updating System Repositories

Before installing Zsh, update the system package repository to ensure you get the latest program versions available:

```bash
sudo apt update
```

###  Installing Zsh

Install Zsh using the following command:

```bash
sudo apt install zsh -y
```

### Setting ZSH as Default Shell

Once installed, set Zsh as your default shell:

```bash
chsh -s $(which zsh)
```

### Fixing Snap Desktop Entry

To include Snap in the variable “XDG_DATA_DIRS,” follow these steps:

1. Open the file using a text editor:
   ```bash
   sudo nano /etc/X11/Xsession.d/60x11-common_xdg_path
   ```
2. Locate the section in the file that manages the XDG_DATA_DIRS variable.
3. Add the following line:
   ```bash
   XDG_DATA_DIRS=/var/lib/snapd/desktop:"$XDG_DATA_DIRS"
   ```
4. Example (inserting the line into the file):
   ```bash
   ...
      if [ -d /usr/share/gdm/greeter ] && [ -n "$IS_GDM" ]; then
          XDG_DATA_DIRS=/var/lib/snapd/desktop:"$XDG_DATA_DIRS"
          export XDG_DATA_DIRS
      fi
   ...
   ```

   Make sure to save the changes after editing the file.

This sequence of commands and edits will properly set up ZSH as your default shell and ensure Snap is included in the necessary directories for desktop entries.

### Customize ZSH

To customize your ZSH shell with themes, plugins, and configurations, follow these steps:

1. Create a `.zprofile` file or copy an existing one to your repository:

    ```bash
    mkdir -p ~/.config/zsh
    touch ~/.zprofile
    ```

2. Create a folder to house the themes and plugins for your ZSH configurations:

    ```bash
    mkdir -p ~/.config/zsh/ZshThemesPlugins
    ```

3. Clone the repositories for ZSH autocomplete, highlighting, and autosuggestions:

    ```bash
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.config/zsh/ZshThemesPlugins
    git clone https://github.com/zsh-users/zsh-autosuggestions.git ~/.config/zsh/ZshThemesPlugins
    git clone https://github.com/zsh-users/zsh-completions.git ~/.config/zsh/ZshThemesPlugins
    ```

    **Note:** It appears that the repository URL for autosuggestions is duplicated. Ensure the correct URL is used for the third plugin.

4. Copy the `zshrc` file from the repository to `~/.config/zsh/`.

5. Reboot your system to apply the changes effectively.

These steps will create the necessary structure and retrieve the plugins and configurations to enhance your ZSH shell with autocomplete, highlighting, and autosuggestions. Modify the `.zprofile` and `zshrc` files as needed to further customize your ZSH experience.

## Oh My Posh

Enhance your terminal experience with Oh My Posh, a customizable prompt engine for your shell.

### Setting ANSI Color

Ensure proper color rendering by setting the terminal environment variable:

```bash
export TERM=xterm-256color
```
### Installation Steps

#### 1. Install Oh My Posh

Download and install Oh My Posh:

```bash
sudo wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh
sudo chmod +x /usr/local/bin/oh-my-posh
```

#### 2. Obtain Themes

- Prepare a directory for themes:
  ```bash
  mkdir -p ~/.config/zsh/ZshThemesPlugins/poshthemes
  ```
- Download themes and extract them:
  ```bash
  wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip -O ~/.config/zsh/ZshThemesPlugins/poshthemes/themes.zip
  unzip ~/.config/zsh/ZshThemesPlugins/poshthemes/themes.zip -d ~/.config/zsh/ZshThemesPlugins/poshthemes
  chmod u+rw ~/.config/zsh/ZshThemesPlugins/poshthemes/*.json
  rm ~/.config/zsh/ZshThemesPlugins/poshthemes/themes.zip
  ```

### 3. Install Required Fonts

Install fonts for optimal display:

```bash
oh-my-posh font install
```

### 4. Configure Oh My Posh

Initialize Oh My Posh with a desired theme:

```bash
eval "$(oh-my-posh init zsh --config ~/.config/zsh/ZshThemesPlugins/poshthemes/atomic.omp.json)"
```

### 5. Auto-Start Oh My Posh with Terminal

For automatic initialization, append the following line to your zshrc file:

```bash
echo 'eval "$(oh-my-posh init zsh --config ~/.config/zsh/ZshThemesPlugins/poshthemes/atomic.omp.json)"' >> ~/.config/zsh/.zshrc
```

### Customization
Explore more themes and customization options in the ~/.config/zsh/ZshThemesPlugins/poshthemes directory.

## NeoFetch
Neofetch provides a simple way to display system information in the terminal with customizability options for an enhanced user experience.

### Installation

To install Neofetch, use the following command:

```bash
sudo apt install neofetch
```

### Running Neofetch at Shell Startup

To display system information every time you start your shell, add neofetch at the beginning of your zshrc or bashrc file.

```bash
echo 'neofetch' >> ~/.zshrc
```

### Customization

Neofetch's configuration file can be found at ~/.config/neofetch/config.conf. Customize it by:

1. Exploring Themes and Settings: Search for various themes and settings online.
2. Applying Customizations: Edit the config.conf file with your desired settings, colors, and information display configurations.

Remember, the configurations in config.conf can be adjusted to tailor Neofetch's appearance to your preferences.
