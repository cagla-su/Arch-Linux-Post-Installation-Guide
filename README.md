# Arch Linux Post-Installation Guide
Hello. In this guide, you will be informed about **how I prepare my Arch system**. If you are ready, let's begin!
## Install AUR Helper
Normally, everyone prefers [yay](https://github.com/Jguer/yay) but I prefer [paru](https://github.com/Morganamilo/paru) since it is written in [rust](https://www.rust-lang.org/).
```
sudo pacman -S --needed base-devel git && git clone https://aur.archlinux.org/paru.git && cd paru && makepkg -si
```
## Install CachyOS Kernel and Repositories
CachyOS repositories contain **both Arch Linux and CachyOS packages**, which have been **re-built** with flags optimized for **performance, stability, and security**. That's why, I prefer CachyOS kernel and repositories on my Arch system.
```
curl -O https://mirror.cachyos.org/cachyos-repo.tar.xz && tar xvf cachyos-repo.tar.xz && cd cachyos-repo && sudo ./cachyos-repo.sh && sudo pacman -S linux-cachyos
```
## GRUB Configuration
```
sudo nano /etc/default/grub
```
```
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
GRUB_DISABLE_SUBMENU=y
```
```
sudo grub-mkconfig -o /boot/grub/grub.cfg
```
## Install Necessary Packages
```
sudo pacman -S unrar unzip ufw tlp flatpak fwupd fastfetch mpv noto-fonts-cjk noto-fonts-emoji 
```
```
sudo systemctl enable --now ufw.service && sudo systemctl enable --now tlp.service
```
## Install Personals Packages
```
sudo pacman -S vivaldi easyeffects && paru -S spotify
```
## Install Gaming Packages
```
sudo pacman -S cachyos-gaming-applications gamemode lib32-gamemode protonplus discord
```
## TLP Configuration
- TLP is simply an **advanced power manager** for laptops using Linux.
- Make sure to **uncheck each option** that are mentioned below while editing the configuration file.
```
sudo nano /etc/tlp.conf
```
```
TLP_ENABLE=1
DISK_IDLE_SECS_ON_AC=0
DISK_IDLE_SECS_ON_BAT=2

MAX_LOST_WORK_SECS_ON_AC=15
MAX_LOST_WORK_SECS_ON_BAT=60

CPU_DRIVER_OPMODE_ON_AC=active
CPU_DRIVER_OPMODE_ON_BAT=active

CPU_SCALING_GOVERNOR_ON_AC=powersave
CPU_SCALING_GOVERNOR_ON_BAT=powersave

CPU_ENERGY_PERF_POLICY_ON_AC=performance
CPU_ENERGY_PERF_POLICY_ON_BAT=power

CPU_MIN_PERF_ON_AC=0
CPU_MAX_PERF_ON_AC=100
CPU_MIN_PERF_ON_BAT=0
CPU_MAX_PERF_ON_BAT=30

CPU_BOOST_ON_AC=1
CPU_BOOST_ON_BAT=0

CPU_HWP_DYN_BOOST_ON_AC=1
CPU_HWP_DYN_BOOST_ON_BAT=0

NMI_WATCHDOG=0

PLATFORM_PROFILE_ON_AC=low-power
PLATFORM_PROFILE_ON_BAT=low-power

AHCI_RUNTIME_PM_ON_AC=on
AHCI_RUNTIME_PM_ON_BAT=auto

WIFI_PWR_ON_AC=off
WIFI_PWR_ON_BAT=on

WOL_DISABLE=Y

PCIE_ASPM_ON_AC=powersupersave
PCIE_ASPM_ON_BAT=powersupersave

RUNTIME_PM_ON_AC=on
RUNTIME_PM_ON_BAT=auto
```
## Configure Fish - Optional
- If you would like your terminal to predict what you are going to type, you might want to use [Fish](https://fishshell.com/) for your terminal.
```
sudo pacman -S fish
```
```
chsh -s /usr/bin/fish # you should log out/reboot after running the command
```
- If you would like to see **fastfetch** every time you launch terminal, you should execute the command below:
```
  function fish_greeting
  fastfetch
  end
```
```
funcsave fish_greeting
```
## Configure fastfetch - Optional
```
sudo nano ~/.config/fastfetch/config.jsonc
```
```
{
  "$schema": "https://github.com/fastfetch-cli/fastfetch/raw/dev/doc/json_schema.json",
"logo": {
"type": "small",
"padding": {
        "top": 6,
        "left": 3
    },
"color": {
"1": "magenta",
"2": "magenta"
}
},
"modules": [
    // Title
    {
      "type": "title",
      "format": "{#1}╭───────────────────"
    },
    // System Information
    {
      "type": "custom",
      "format": "{#1}│ {#}>^^< System Information >^^<"
    },
{
      "type": "host",
      "key": "│ Computer Model",
      "keyColor": "magenta"
    },
    {
      "type": "os",
      "key": "│ Operating System",
      "keyColor": "magenta"
    },
    {
      "type": "kernel",
      "key": "│ Kernel",
      "keyColor": "magenta"
    },
{
      "type": "packages",
      "key": "│ Packages",
      "keyColor": "magenta"
    },
    {
      "type": "custom",
      "format": "{#1}│"
    },
    // Desktop
    {
      "type": "custom",
      "format": "{#1}│ {#}>^^< Desktop >^^<",
    },
    {
      "type": "de",
      "key": "│ Desktop Environment",
      "keyColor": "magenta"
    },
    {
      "type": "wm",
      "key": "│ Window Manager",
      "keyColor": "magenta"
    },
    {
      "type": "shell",
      "key": "│ Shell",
      "keyColor": "magenta"
    },
    {
      "type": "custom",
      "format": "{#1}│"
    },
    // Hardware Information
    {
      "type": "custom",
      "format": "{#1}│ {#}>^^< Hardware Information >^^<",
    },
    {
      "type": "cpu",
      "key": "│ Processor",
      "keyColor": "magenta"
    },
    {
      "type": "gpu",
      "key": "│ Graphics Card",
      "keyColor": "magenta"
    },
    {
      "type": "memory",
      "key": "│ Memory",
      "keyColor": "magenta"
    },
    {
      "type": "disk",
      "key": "│ Disk",
      "keyColor": "magenta"
    },
    {
      "type": "custom",
      "format": "{#1}│"
    },
    // Colors
    {
      "type": "colors",
      "key": "{#separator}│",
      "symbol": "circle"
    },
    // Footer
    {
      "type": "custom",
      "format": "{#1}╰───────────────────"
    }
  ]
}
```
## Dolby Atmos Setup (EasyEffects)
- Download and extract [these impulses](https://github.com/shuhaowu/linux-thinkpad-speaker-improvements/tree/main/ThinkPadT495) for Dolby Atmos profiles.
- `EasyEffects` **-** `3 horizontal lines on the top right` **-** `Preferences` **-** `Launch Service at System Startup`
- **Next** : `Effects` **-** `Add Effect` **-** `Convolver` **-** `Impulses` **-** `Import Impulse` **-** `add the impulses` **-** `Impulses` **-** `load one of the impulses`
- Some impulses like **Movie** can deliver poor quality sounds while listening to music. You should load a different impulse such as **Voice** in such cases.
# Conclusion
This guide was about Arch Linux post-installation! I hope the guide has been useful. Thank you for reading, have a nice day! 🐧
