# KDE Setup Guide

## Initial Setup After Installation

Ensure your system is up-to-date:

```bash
sudo apt update
sudo apt upgrade -y
```

#### Install TimeShift

TimeShift allows for system snapshots and backups:

```bash
sudo apt install timeshift
```

#### Installing Complete Multimedia Support

Enhance multimedia capabilities with essential packages:

```bash
sudo apt install kubuntu-restricted-extras ubuntu-restricted-extras
```

#### Install Curl

Curl aids in transferring data:

```bash
sudo apt install curl
```

#### Improve Battery Life (Optional)

Enhance battery performance with TLP for Linux:

```bash
sudo apt-get install tlp tlp-rdw
```

Start TLP after installation:

```bash
sudo tlp start
```

<a id="cleaning"></a>

#### Cleaning

Remove incomplete packages, clean apt-cache, and eliminate unnecessary dependencies:

```bash
sudo apt-get autoclean
sudo apt-get clean
sudo apt-get autoremove
```

#### Use Flatpak for More Applications

Access a wider range of applications using Flatpak:

```bash
sudo apt install plasma-discover-backend-flatpak
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
sudo apt install flatpak
```

#### Install Additional Fonts

Enhance your font library with popular choices:

    sudo apt install fonts-open-sans fonts-roboto fonts-oxygen fonts-lato

#### Install Net Tools

Enhance your font library with popular choices:

```bash
sudo apt install net-tools
```

## Shell Setup

Enhance your Linux command line experience with ZSH and Oh My Posh! This setup guide walks you through installing ZSH, a powerful shell, and configuring Oh My Posh to personalize your command line prompt.
[Full Configuration](Shell%20Setup/ShellSetup.md)

## Git

### Installing Git

Ensure Git is installed on your Linux system. Use these commands based on your distribution:

- **Debian/Ubuntu:**

  ```bash
  sudo apt-get update
  sudo apt-get install git
  ```

- **Red Hat/Fedora:**
  ```bash
  sudo yum install git
  ```

### Configuring Git Settings

Open a terminal and follow these steps to set up your Git configuration:

```bash
# Set your Git username
git config --global user.name "Your Name"

# Set your Git email
git config --global user.email "your.email@example.com"

# Specify your preferred text editor for Git (e.g., VS Code)
git config --global core.editor "code --wait"

# Handle line endings when collaborating across platforms
git config --global core.autocrlf input

# Configure VS Code as the default difftool for visualizing version differences
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
```

Explanation of commands:

- `user.name` and `user.email`: Associates your identity with Git commits.
- `core.editor`: Sets your preferred text editor for Git operations.
- `core.autocrlf`: Helps manage line endings when collaborating across platforms.
- `diff.tool` and `difftool.vscode.cmd`: Establishes VS Code as the default tool for visualizing differences.

### Additional Recommendations

1. **SSH Setup:** Enhance security by generating SSH keys for communication with remote repositories. Use `ssh-keygen` and follow your Git provider's instructions to add these keys.

2. **Alias Configuration:** Simplify Git commands using aliases:

   ```bash
   git config --global alias.co checkout
   git config --global alias.br branch
   git config --global alias.ci commit
   git config --global alias.st status
   ```

### Verifying Configuration

To review your Git configuration, enter:

```bash
git config --global --list
```

This command displays all your global Git settings.

## Setting Up For Development

### Packages

#### Build-Essentials

If you didn't knew, build-essentials is literally what it says, the essentials to build a lot of software, mostly I use it to install g++ and gcc, c++ and c compiles and make, software used to make a compilation more human.

```bash
sudo apt install build-essential
```

#### Python3 and Pip3

When i finnished my programming course on college, the first thing I tried to learn was python (I did good i think), and looking that python2 is getting deprecated this year, why not python3? Mostly I use it when I'm trying to learn ML and Django (never quite understood Django)

```bash
sudo apt install python3 python3-pip
```

#### Node.js And NVM

To **install** or **update** nvm, you should run the [install script][2]. To do that, you may either download and run the script manually, or use the following cURL or Wget command:

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

```sh
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

Running either of the above commands downloads a script and runs it. The script clones the nvm repository to `~/.nvm`, and attempts to add the source lines from the snippet below to the correct profile file (`~/.bash_profile`, `~/.zshrc`, `~/.profile`, or `~/.bashrc`).

<a id="profile_snippet"></a>

```sh
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

**Install The Latest Version**

```bash
nvm install -g --lts
```

#### CRA (create-react-app) And Vite

- Install Create React App
  ```bash
  sudo npm install -g create-react-app
  ```
- Update NPM
  ```bash
  npm update -g
  ```
- Install Vite
  ```bash
  npm install -g create-vite@latest
  ```

### Docker

#### Instal Docker Engine

Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository.

1.  Set up Docker's apt repository.

    ```bash
    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg

    # Add the repository to Apt sources:
    echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    ```

2.  Install the Docker packages.
    ```bash
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```
3.  Verify that the Docker Engine installation is successful by running the hello-world image.
    ```bash
    sudo docker run hello-world
    ```
    This command downloads a test image and runs it in a container. When the container runs, it prints a confirmation message and exits.

You have now successfully installed and started Docker Engine.

#### Instal Docker Desktop

**Prerequisites**

For non-Gnome Desktop environments, gnome-terminal must be installed:

```bash
sudo apt install gnome-terminal
```

**Install Docker Desktop**

1.  Download latest [DEB package](https://desktop.docker.com/linux/main/amd64/docker-desktop-4.26.1-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64)
2.  Install the package with apt as follows:
    ```bash
    sudo apt-get update
    sudo apt-get install ./docker-desktop-<version>-<arch>.deb
    ```
    There are a few post-install configuration steps done through the post-install script contained in the deb package.

### Mongo DB

If you prefer to use Docker, MongoDB can be set up using a Docker image. Alternatively, for a workstation setup, follow this [Mongo Server Installation Guide](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu).

#### MongoDB Tools

- **MongoDB Shell**: [Download MongoDB Shell DEB](https://downloads.mongodb.com/compass/mongodb-mongosh_2.1.1_amd64.deb)
- **MongoDB Compass**: [Download MongoDB Compass DEB](https://downloads.mongodb.com/compass/mongodb-compass_1.41.0_amd64.deb)
- **MongoDB Atlas CLI**: [Download MongoDB Atlas CLI DEB](https://fastdl.mongodb.org/mongocli/mongodb-atlas-cli_1.14.0_linux_x86_64.deb)

For each tool, download the DEB package and install it using `sudo apt-get install ./package_name.deb`.

Please note: Ensure compatibility with your system architecture and update versions accordingly.

#### .NET

##### .NET SDK Versions

The .NET SDK allows you to develop apps with .NET. If you install the .NET SDK, you don't need to install the corresponding runtime. To install the .NET SDK, run the following commands:

- **.NET SDK 8**
  Install the .NET SDK version 8 which includes the latest features and improvements:
  ```bash
  sudo apt-get install -y dotnet-sdk-8.0
  ```
- **.NET SDK 7**
  For compatibility or specific project requirements using .NET SDK version 7:
  ```bash
  sudo apt-get install -y dotnet-sdk-7.0
  ```
- **_.NET SDK 6_**
  Use .NET SDK version 6 for legacy projects or specific framework dependencies:
  ```bash
  sudo apt-get install -y dotnet-sdk-6.0
  ```

##### Verification Steps

To confirm successful installations:

- For .NET SDK, run `dotnet --version` to display the installed SDK version.
- For Mono, execute `mono --version` to check the installed version.

##### .NET Framework (Mono)

- **Adding the Mono Repository**
  To install the Mono framework, add its repository and install:
  ```bash
  sudo apt install ca-certificates gnupg
  sudo gpg --homedir /tmp --no-default-keyring --keyring /usr/share/keyrings/mono-official-archive-keyring.gpg --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
  echo "deb [signed-by=/usr/share/keyrings/mono-official-archive-keyring.gpg] https://download.mono-project.com/repo/ubuntu stable-focal main" | sudo tee /etc/apt/sources.list.d/mono-official-stable.list
  sudo apt update
  ```
- **Installing Mono**
  Execute the following command to install Mono:
  ```bash
  sudo apt install mono-devel
  ```

##### Troubleshooting

**Common Issues and Resolutions**

- **Issue**: Installation fails due to repository issues.

  - **Resolution**: Ensure correct repository keys and URLs. Re-import keys and update repositories.

- **Issue**: SDK versions conflict or installation errors.
  - **Resolution**: Verify system dependencies and compatibility before installation.

## Additional Resources

- [.NET Official Documentation](https://docs.microsoft.com/en-us/dotnet/)
- [Mono Project Documentation](https://www.mono-project.com/docs/)

### Programs

#### Code Editors

- **Visual Studio Code (VS Code)**

  - Description: A highly customizable and feature-rich code editor with support for various programming languages, debugging, and extensions.
  - [Download Link](https://code.visualstudio.com/): Install VS Code from the official website.

- **Kate**

  - Description: A lightweight and versatile text editor included in the KDE software compilation, offering syntax highlighting and plugins for code editing.
  - Installed by default in KDE-based distributions or available through package managers.

- **Sublime Text**
  - Description: A sophisticated text editor known for its speed, ease of use, and extensive plugin ecosystem.
  - [Download Link](https://www.sublimetext.com/): Install Sublime Text from the official website.

#### Integrated Development Environments (IDEs)

- **DataGrip**

  - Description: A powerful database IDE for multiple SQL databases, providing intelligent query console, schema navigation, and data editing.
  - [Download Link](https://www.jetbrains.com/datagrip/download/): Install DataGrip from JetBrains' official website.

- **PyCharm**

  - Description: A robust Python IDE with intelligent code completion, debugging, and support for web development frameworks.
  - [Download Link](https://www.jetbrains.com/pycharm/download/): Install PyCharm from JetBrains' official website.

- **Rider**

  - Description: A cross-platform .NET IDE offering advanced coding assistance, refactoring, and debugging capabilities.
  - [Download Link](https://www.jetbrains.com/rider/download/): Install Rider from JetBrains' official website.

- **WebStorm**

  - Description: A professional JavaScript, TypeScript, and Node.js IDE with smart coding assistance and integrated tools for web development.
  - [Download Link](https://www.jetbrains.com/webstorm/download/): Install WebStorm from JetBrains' official website.

- **Postman**
  - Description: A comprehensive API testing tool facilitating the creation, sharing, and documentation of APIs.
  - [Download Link](https://www.postman.com/downloads/): Install Postman from the official website.

#### Tools

- **Postman**

  - Description: See above.

- **Draw.io**

  - Description: A versatile diagramming tool for creating flowcharts, diagrams, and visual representations of ideas or processes.
  - [Online Version](https://app.diagrams.net/): Use Draw.io online or check instructions for installation.

- **GitKraken**
  - Description: A Git GUI client offering an intuitive interface for managing Git repositories, pull requests, and code collaboration.
  - [Download Link](https://www.gitkraken.com/download): Install GitKraken from the official website.
