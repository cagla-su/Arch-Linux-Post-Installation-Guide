# Arch Linux Post-Installation Guide
Hello. In this guide, you will be informed about **how to prepare <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/17e40f3d-086e-4979-bd7a-786ce5864c66" /> Arch Linux post-installation**. If you are ready, let's begin!
## Install AUR Helper
Generally, users prefer [yay](https://github.com/Jguer/yay) but I prefer [paru](https://github.com/Morganamilo/paru) because I think it is better.
```
sudo pacman -S --needed base-devel git && git clone https://aur.archlinux.org/paru.git && cd paru && makepkg -si
```
## Rank Mirrors
```
sudo pacman -S reflector
```
```
sudo reflector --country Türkiye --latest 5 --sort rate --save /etc/pacman.d/mirrorlist
```
- Make sure to change the country name according to the country you are living.
## Use Custom DNS
```
sudo systemctl enable --now systemd-resolved
```
- After enabling `systemd-resolved`, follow the instructions of custom DNS you want to use. My suggestion is either <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/52a59002-d12c-403b-ae21-6d63aa8d4a2f" /> [Cloudflare DNS](https://developers.cloudflare.com/1.1.1.1/setup/linux/#systemd-resolved) or <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/ff72bf0c-8b37-4309-8520-ffd8892dbeeb" /> [NextDNS](https://nextdns.io/)
## Install <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" /> CachyOS Repositories and Kernel
<img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" /> CachyOS is a **performance-focused** Linux distribution, that's why I use their **repositories** and **kernel** for **higher performance**.
```
curl -O https://mirror.cachyos.org/cachyos-repo.tar.xz
tar xvf cachyos-repo.tar.xz && cd cachyos-repo
sudo ./cachyos-repo.sh
sudo pacman -S linux-cachyos-bore
```
## Install Necessary Packages
```
sudo pacman -S unrar unzip ufw tlp flatpak fwupd fastfetch mpv noto-fonts-cjk noto-fonts-emoji 
```
```
sudo systemctl enable --now ufw.service && sudo systemctl enable --now tlp.service
```
## Install Gaming Packages
```
sudo pacman -S gamemode lib32-gamemode steam lutris prismlauncher discord && flatpak install flathub org.vinegarhq.Sober com.heroicgameslauncher.hgl com.vysp3r.ProtonPlus
```
Additionally, I follow [this guide](https://github.com/lutris/docs/blob/master/InstallingDrivers.md#arch--manjaro--other-arch-linux-derivatives) for Vulkan drivers. If you would like to learn more about Linux gaming, I suggest that you check [my Linux gaming guide](https://github.com/cagla-su/Linux-Gaming-Guide).
## systemd-boot Configuration
- Skip this part if you are using a different bootloader such as GRUB.
```
sudo nano /boot/loader/loader.conf
```
```                      
default @saved
timeout 5
```
- Additionally, systemd-boot **may not detect <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" /> CachyOS kernel**, in this case, follow these steps:
```
ls /boot/loader/entries/*
```
- If you can see the custom kernel here, everything is fine.
- If you **cannot**, looking at the output you get, go to the location of Linux kernel you are using and copy the .conf file with a different name (linux-cachyos-bore) and edit the file:
```
sudo nano /boot/loader/entries/linux-cachyos-bore.conf
```
```
title   Arch Linux (linux-cachyos-bore)
linux   /vmlinuz-linux-cachyos-bore
initrd  /initramfs-linux-cachyos-bore.img
options # DO NOT TOUCH THIS LINE
```
- When you reboot, you will be able to switch to the custom kernel.
## TLP Configuration
- TLP is simply an **advanced power manager** for laptops using Linux.
  - If you are using a PC, install `power-profiles-daemon` instead.
- Make sure to **uncheck each option** that are mentioned below while editing the configuration file.
```
sudo nano /etc/tlp.conf
```
```
TLP_ENABLE=1
DISK_IDLE_SECS_ON_AC=0
DISK_IDLE_SECS_ON_BAT=2

CPU_DRIVER_OPMODE_ON_AC=active
CPU_DRIVER_OPMODE_ON_BAT=active

CPU_SCALING_GOVERNOR_ON_AC=performance
CPU_SCALING_GOVERNOR_ON_BAT=powersave

CPU_ENERGY_PERF_POLICY_ON_AC=performance
CPU_ENERGY_PERF_POLICY_ON_BAT=power

CPU_MIN_PERF_ON_AC=0
CPU_MAX_PERF_ON_AC=100
CPU_MIN_PERF_ON_BAT=0
CPU_MAX_PERF_ON_BAT=20

CPU_BOOST_ON_AC=1
CPU_BOOST_ON_BAT=0

CPU_HWP_DYN_BOOST_ON_AC=1
CPU_HWP_DYN_BOOST_ON_BAT=0

NMI_WATCHDOG=0

PLATFORM_PROFILE_ON_AC=performance
PLATFORM_PROFILE_ON_BAT=low-power

AHCI_RUNTIME_PM_ON_AC=on
AHCI_RUNTIME_PM_ON_BAT=auto

WIFI_PWR_ON_AC=off
WIFI_PWR_ON_BAT=on

WOL_DISABLE=Y

RUNTIME_PM_ON_AC=on
RUNTIME_PM_ON_BAT=auto
```
## Little Performance Tweaks
### vm.swappiness
- If you have **16 GB or more RAM**, reducing `vm.swappiness` value can benefit you for **higher performance**.
  - However if you have **less than 16 GB RAM, skip this part**.
```
sudo nano /etc/sysctl.conf
```
```                            
vm.swappiness=10
```
```
sudo sysctl -p
```
### Disable NetworkManager-wait-online.service
- For a **faster boot time**, disable `NetworkManager-wait-online.service`:
```
sudo systemctl disable NetworkManager-wait-online.service
```
## Configure Fish - Optional
If you would like your terminal to **predict what you are going to type**, I suggest that you use [Fish](https://fishshell.com/) for your terminal.
```
sudo pacman -S fish
```
```
chsh -s /usr/bin/fish # you should reboot after running the command
```
- If terminal tells you that the **process has failed**, try `chsh -s /bin/fish` instead.
Additionally, if you would like to see **fastfetch** every time you launch terminal, you should execute the commands below:
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
sudo mkdir ~/.config/fastfetch/ && sudo nano ~/.config/fastfetch/config.jsonc
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
## <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/076989c3-9b17-4ff4-822e-91d60e209632" /> Dolby Atmos Setup (<img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/318f8066-239b-45b1-ba4c-d5de14fe597f" /> EasyEffects)
- Download and extract [these impulses](https://github.com/shuhaowu/linux-thinkpad-speaker-improvements/tree/main/ThinkPadT495) for <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/076989c3-9b17-4ff4-822e-91d60e209632" /> Dolby Atmos profiles.
- **Launch <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/318f8066-239b-45b1-ba4c-d5de14fe597f" /> EasyEffects** : `3 horizontal lines on the top right` **-** `Preferences` **-** `Launch Service at System Startup`
- **Next** : `Effects` **-** `Add Effect` **-** `Convolver` **-** `Impulses` **-** `Import Impulse` **-** `add the impulses` **-** `Impulses` **-** `load one of the impulses`
- Some impulses like **Movie** can deliver poor quality while listening to music. You should load a different impulse such as **Voice** in such cases.
# Conclusion
This guide was about Arch Linux post-installation! I hope the guide has been useful. Thank you for reading! 🐧
