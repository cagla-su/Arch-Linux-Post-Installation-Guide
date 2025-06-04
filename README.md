# Arch Linux Post-Installation Guide
Hello 🤭. In this guide, you will be informed about how do I prepare my Arch system after installation. So, let's begin!
## Install AUR Helper
Normally, everyone prefers [yay](https://github.com/Jguer/yay) but I prefer [paru](https://github.com/Morganamilo/paru) since it is written in [rust](https://www.rust-lang.org/).
### Install Paru AUR Helper
```
sudo pacman -S --needed base-devel git && git clone https://aur.archlinux.org/paru.git && cd paru && makepkg -si
```
## Install CachyOS Repositories and CachyOS Kernel - Optional
- [CachyOS](https://cachyos.org/) is a **performance focused Arch-based** Linux distribution. If you would like an **out of the box experience** (it can be considered out of the box compared to Arch) and need the best performance possible, I suggest you simply install CachyOS.
- However, I just want to use its [greatly optimized repositories and kernel](https://github.com/CachyOS/linux-cachyos#cachyos-repositories) while configuring every other thing about my system on my own.
  - **Be careful, do not use CachyOS kernel if you need good battery life!** However, you can still install the kernel and use it while performing resource-intensive tasks (such as gaming) and switch to the default **Linux** or **Linux-LTS** kernel when you need more battery life.
### Install
```
wget https://mirror.cachyos.org/cachyos-repo.tar.xz && tar xvf cachyos-repo.tar.xz && cd cachyos-repo && sudo ./cachyos-repo.sh && sudo pacman -Sy && sudo pacman -S linux-cachyos
```
## systemd-boot Configuration
**The command to configure systemd-boot**
```
sudo nano /boot/loader/loader.conf
```
**How should your loader.conf file look like**
```
default @saved
timeout 5
#console-mode keep
auto-entries 0
```
## Install Necessary Packages
```
sudo pacman -S unrar unzip intel-ucode ufw auto-cpufreq flatpak fwupd fastfetch vlc noto-fonts-cjk noto-fonts-emoji && sudo systemctl enable --now ufw.service
```
You can install `amd-ucode` instead of `intel-ucode` if you have an AMD CPU.
## Install Optional Packages
```
sudo pacman -S zen-browser onlyoffice easyeffects && paru -S spotify zoom
```
## Install Gaming Packages
```
sudo pacman -S cachyos-gaming-applications gamemode lib32-gamemode protonup-qt vesktop
```
## Enable auto-cpufreq
- auto-cpufreq is an automatic CPU speed & power optimizer. It is generally good for laptops since it does everything for you.
- **Command to enable auto-cpufreq**
```
sudo auto-cpufreq --install
```
After the command, you don't have to do anything further but if you would like to configure it a bit more, continue reading the step.
### auto-cpufreq Configuration 
**Command to configure auto-cpufreq**:
```
sudo nano /etc/auto-cpufreq.conf
```
```
[charger]
governor = performance
energy_performance_preference = performance
energy_perf_bias = balance_performance
platform_profile = performance
scaling_min_freq = 1000000
scaling_max_freq = 3900000 # check your CPU's supported maximum processor frequency and change the value according to it
turbo = always

[battery] # You can change the values to be the same as charger section if you don't want to have good battery life but to have high performance on battery mode as well. You can just not include this section if you have a PC or a laptop with no battery.
governor = powersave
energy_performance_preference = power
energy_perf_bias = power
platform_profile = low-power
scaling_min_freq = 800000 # for laptops, any frequency lower than 800 MHz is unstable but if you want and if your CPU supports it, you can decrease the value
scaling_max_freq = 1000000 # for a balance of snappiness and power saving, maximum 1 GHz frequency is nice but of course you can increase the value if you want
turbo = never
enable_thresholds = true # do not include this option in your file if you don't have a battery or if you don't want to set a threshold
start_threshold = 75 # do not include this option in your file if you don't have a battery or if you don't want to set a threshold
stop_threshold = 80 # do not include this option in your file if you don't have a battery or if you don't want to set a threshold
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
**The command to configure fastfetch**
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
- After launching [EasyEffects](https://github.com/wwmm/easyeffects) and setting it to launch at boot from app settings, download [these impulses](https://github.com/shuhaowu/linux-thinkpad-speaker-improvements/tree/main/ThinkPadT495) for Dolby Atmos profiles.
- After downloading the files, move them to a location you will remember the path of.
- Next, in EasyEffects, open `Effects` page and click `Add Effect`. Then, add a `Convolver`.
- Click `Impulses` and `Import Impulse`, now add the .irs files you downloaded.
- Last, in `Impulses` section, it will be enough to load one of the presets. You can always switch among presets.
## Conclusion
This guide was about Arch Linux post-installation! I hope the guide has been useful. Thank you for reading, have a nice day! 🐧
