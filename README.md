# SteamOS Ubuntu

![SteamOS Ubuntu](image.png)

SteamOS Ubuntu is a set of scripts to create an Ubuntu-based Steam machine.

It will do the following:

* Create the `steam` user account if it does not exist.
* Install steam, if it is not installed.
* Install the Steam Compositor, Steam Mode Switch, and boot splash themes.
* Configure autologin for the `steam` user account.
* Configure the default session to the Steam Compositor.
* Create `reboot-to-[steamos,desktop]-mode` scripts to switch between sessions.
* Create `steamos-fg` script for games that won't run in the foreground on the SteamOS Compositor.
* Optionally install the latest graphics drivers for AMD, Nvidia, and Intel GPUs.
* Optionally install proton fixes.

For best results, this should be run on a fresh installation of
Ubuntu 18.04 desktop.

## Requirements
In order to install SteamOS Ubuntu, you should have a fresh installation of
Ubuntu 18.04 Desktop installed. Other versions may work, but have not been 
tested.

## Installation
Installation is very simple. Follow these steps to install SteamOS Ubuntu:

1. Install git:    
`sudo apt install git -y`

2. Clone or download this repository:    
`git clone https://github.com/ShadowApex/steamos-ubuntu.git`

3. Run the installation script:    
`cd steamos-ubuntu`    
`sudo ./install.sh`

4. If the "STEAM needs to be online to update" error appears on startup, Press CTRL+ALT+F3 to enter a virtual terminal, and login with the account used before installation.

5. Run the `sudo passwd steam` command and follow the instructions to change the password to the Steam user account (as this will be required to run any sudo commands), run `sudo usermod -aG sudo steam` to give the account elevated privileges, then run the `reboot-to-desktop-mode` command to reboot to the GNOME desktop environment.

6. When back in the GNOME desktop environment, press "CTRL+ALT+T" or open the Terminal, and run these commands in order:    
`sudo mkdir -p ~/.steam/ubuntu12_32/steam-runtime`    
`steam`

7. After Steam is finished updating (When the Steam login window appears), close Steam, and run this command to reboot into SteamOS mode:    
`reboot-to-steamos-mode`

## Advanced Options
The installation script has several options that you can specify upon installation
in the form of environment variables. You can specify these options by prefixing
running the install script with the options you want.

For example, if you want to disable installing OpenSSH and run the script non-
interactively, you can run this command:

`INCLUDE_OPENSSH=false NON_INTERACTIVE=true sudo ./install.sh`

Here is the list of all the available installation options:

| Option Name          | Default | Description                                              |
| -------------------- | ------- | -------------------------------------------------------- |
| `INCLUDE_OPENSSH`    | true    | Whether or not OpenSSH server should be installed        |
| `INCLUDE_SAKURA`     | true    | Whether or not to install a terminal emulator            |
| `INCLUDE_PROTONFIX`  | true    | Whether or not to install Protonfix                      |
| `INCLUDE_GPU_DRIVERS`| true    | Whether or not to install the latest GPU drivers         |
| `GPU_TYPE`           | auto    | GPU drivers to install. Can be: auto, nvidia, amd, intel |
| `NON_INTERACTIVE`    | false   | Whether or not to prompt the user during install         |
| `STEAM_USER`         | steam   | The username of the account to autologin as              |

## FAQ

### How can I switch between desktop mode and SteamOS mode?

After installation, there will not be an easy way to switch between a regular
Gnome desktop session and Steam. In order to make it easier to switch between
the two, there are two commands that are installed that will let you switch 
between the two:

* `reboot-to-desktop-mode` - sets gnome as the default session and reboots
* `reboot-to-steamos-mode` - sets steam as the default session and reboots

You can access the terminal from Steam by adding a local shortcut for `Sakura`.

### Some games aren't launching correctly in SteamOS mode
When using the SteamOS compositor, some games start behind the big picture UI and
no graphics are displayed. The `steamos-fg` script forces such games to be shown 
in the foreground.

Affected games this script fixes include:

    Dead Cells
    Dirt Rally
    Civilization VI
    The Count Lucanor
    Mad Max

To fix this, add `steamos-fg %command%` to the launch options for each game you 
wish to use this script with.

### How can I change the resolution and refresh rate used in SteamOS mode?

After installation, follow [this guide](https://github.com/ValveSoftware/SteamOS/wiki/Custom-Resolutions-And-Refresh-Rates) for instructions on how to change the screen resolution and refresh rate. This can be done after "Step 6" of the Installation guide.

## Attributions
* Alkazar for [steamos-fg](https://github.com/alkazar/steamos-fg)
* nickcj931 for the [Steam offline error fix](https://github.com/ShadowApex/steamos-ubuntu/issues/6#issuecomment-498036893)
* gamer-os for [Steam-Compositor-Plus](https://github.com/gamer-os/steamos-compositor-plus)

## Legal
The Steam logo and Ubuntu logo are registered trademarks of Valve Corporation
and Canonical respectively. This project is in no way officially affiliated with
Valve or Canonical.
