# Autoinstall Configuration

This repository contains an autoinstall configuration for setting up an Ubuntu system with specific packages, snaps, and late commands.

## Configuration Details

### Identity

- **Hostname:** ubuntu-lgabor
- **Username:** lgabor
- **Password:** P@sswr0rd

### Storage

- **Layout:** lvm

### Snaps

The following snaps will be installed:

- spotify
- telegram-desktop
- obsidian
- code
- notepad-plus-plus
- discord
- powershell
- kubectl
- node
- docker
- azcli

### Packages

The following packages will be installed:

- vim
- dotnet-host-8.0
- git

### Late Commands

The following commands will be executed late in the installation process:

1. Download and install ProtonVPN:
    ```sh
    curtin in-target -- wget https://repo2.protonvpn.com/debian/dists/stable/main/binary-all/protonvpn-stable-release_1.0.3-3_all.deb
    curtin in-target -- dpkg -i ./protonvpn-stable-release_1.0.3-3_all.deb
    curtin in-target -- sudo apt update
    curtin in-target -- sudo apt install -y proton-vpn-gnome-desktop
    ```

2. Add Microsoft package repository and install Azure Functions Core Tools:
    ```sh
    curtin in-target -- curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
    curtin in-target -- sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
    curtin in-target -- sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list'
    curtin in-target -- sudo apt update
    curtin in-target -- sudo apt install azure-functions-core-tools-4
    ```

## Usage

To use this autoinstall configuration, include the `autoinstall.yaml` file in your Ubuntu installation media or use it with a compatible autoinstall tool.

## Reference

For more details on autoinstall configurations, refer to the [Canonical Subiquity Autoinstall Reference](https://canonical-subiquity.readthedocs-hosted.com/en/latest/reference/autoinstall-reference.html).