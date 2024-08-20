# Çıt's Arch Linux Post-Installation Guide (XFCE) - Thinkpad T490
Hello. I wrote this guide for **Thinkpad T490 and XFCE specifically**, however you can still follow **almost** all the steps if you don't have the same computer as I have. So, let's begin!

## Install AUR Helper
Normally, everyone prefers **yay** but I prefer **paru** since it is written in **rust**.
### Install Paru AUR Helper
sudo pacman -S --needed base-devel git && git clone https://aur.archlinux.org/paru.git && cd paru && makepkg -si
## Install CachyOS Repositories and BORE Kernel (Optional)
CachyOS is a **performance focused Arch-based** Linux distribution. If you would like an **out of the box experience** (it can be considered out of the box compared to Arch), I would simply install CachyOS. However, I just want to use their greatly optimized repositories and kernel while configuring every other things about my system on my own. **Be careful, do not use CachyOS kernel if you need good battery life!**
### Install
wget https://mirror.cachyos.org/cachyos-repo.tar.xz && tar xvf cachyos-repo.tar.xz && cd cachyos-repo && sudo ./cachyos-repo.sh && sudo pacman -S linux-cachyos-bore
## GRUB Configuration
- GRUB_CMDLINE_LINUX_DEFAULT="mitigations=off" (do not remove the already existing parameters, just add mitigations=off next to them)
- GRUB_DEFAULT=saved
- GRUB_SAVEDEFAULT=true
- GRUB_DISABLE_SUBMENU=y
### Information About GRUB Configuration
- **You have to execute this command in terminal to apply changes**: sudo grub-mkconfig -o /boot/grub/grub.cfg
- CPU mitigations reduce performance by 30% on these CPUs:
  - **AMD**: Zen 1, Zen 1+, Zen 2
  - **Intel**: 6th, 7th and 8th Generation
  - This is why you might want to disable mitigations via **mitigations=off** kernel parameter especially if you're gaming. However, disabled mitigations might **introduce security risks**. If you care about security more than performance, do not disable mitigations.
- If you will be using **only one kernel** that you installed while installing Arch, you don't have to change the stats of **GRUB_DEFAULT**, **GRUB_SAVEDEFAULT** and **GRUB_DISABLE_SUBMENU** 
## Intel iGPU Configuration For X11
- Some projects such as **Debian, Fedora, KDE and Mozilla** suggest **modesetting** driver instead of using **xf86-video-intel** with **intel** driver as it is known to have problems with lower performance. However, using **modesetting** driver can cause issues such as **screen tearing** but we'll be using **Picom** with vsync on, so screen tearing won't be an issue as long as Picom is running.
- **Location of Intel Configuration File**: sudo nano /etc/X11/xorg.conf.d/20-intel.conf
  - Section "Device"
  - Identifier "Intel Graphics"
  - Driver "modesetting"
  - Option "Backlight" "intel_backlight"
  - Option "AccelMethod" "glamor"
  - Option "TearFree" "false"
  - Option "RenderAccel" "true"
  - Option "SwapbuffersWait" "false"
  - Option "DRI" "2"
  - Option "Throttle" "false"
  - Option "FramebufferCompression" "false"
  - Option "TripleBuffer" "false"
  - Option "Shadow" "false"
  - Option "LinearFramebuffer" "true"
  - Option "RelaxedFencing" "false"
  - Option "BufferCache" "true"
  - EndSection
## Install Necessary Packages For XFCE
sudo pacman -S unrar unzip intel-ucode ufw tlp throttled fwupd fastfetch alsa-tools easyeffects vlc noto-fonts-cjk noto-fonts-emoji pavucontrol capitaine-cursors picom xarchiver mousepad && paru -S xfce4-panel-profiles xfce4-docklike-plugin flat-remix-gtk && sudo systemctl enable --now tlp.service && sudo systemctl enable --now throttled.service && sudo systemctl enable --now ufw.service
- You don't have to install these packages:
  - **intel-ucode**: if you don't have an Intel CPU
  - **ufw**: if you don't want to enable firewall
  - **tlp**: if you don't want to have better battery life. Use **power-profiles-daemon** if you only want to have high performance
  - **throttled**: if you either don't have an Intel CPU or if you don't want to undervolt your CPU + iGPU
  - **fwupd**: if your computer is not supported by fwupd for firmware updates
## Install Other Packages - Gaming and Utilities
sudo pacman -S cachyos-gaming-meta gamemode lib32-gamemode protonup-qt vesktop heroic-games-launcher prismlauncher joplin-desktop spectacle obs-studio onlyoffice shotcut okular && paru -S nomacs ptyxis spotify zoom
### For Gamemode
- Download the .ini file from [the link](https://github.com/FeralInteractive/gamemode/blob/master/example/gamemode.ini) and move it to the correct directory via this command:
  - cd Downloads && sudo mv gamemode.ini /etc/
## TLP Configuration
- You can use **TLP-UI** instead but I noticed it doesn't uncheck some options which prevents them from functioning, that's why it is healthier to apply them manually. Also, again, **do not use TLP if you don't need battery life, using power-profiles-daemon is easier and needs no configuration!!!**
- **Location**: sudo nano /etc/tlp.conf (make sure unchecking (removing # signs) of each option)
  - TLP_ENABLE=1
  - TLP_DEFAULT_MODE=BAT
  - CPU_DRIVER_OPMODE_ON_AC=active
  - CPU_DRIVER_OPMODE_ON_BAT=active
  - CPU_SCALING_GOVERNOR_ON_AC=performance
  - CPU_SCALING_GOVERNOR_ON_BAT=powersave
  - CPU_ENERGY_PERF_POLICY_ON_AC=performance
  - CPU_ENERGY_PERF_POLICY_ON_BAT=power
  - CPU_MIN_PERF_ON_AC=0
  - CPU_MAX_PERF_ON_AC=100
  - CPU_MIN_PERF_ON_BAT=0
  - CPU_MAX_PERF_ON_BAT=30
  - CPU_BOOST_ON_AC=1 (**DON'T USE THIS OPTION IF YOUR CPU DOES NOT SUPPORT BOOST**)
  - CPU_BOOST_ON_BAT=0 (**DON'T USE THIS OPTION IF YOUR CPU DOES NOT SUPPORT BOOST**)
  - CPU_HWP_DYN_BOOST_ON_AC=1 (**DON'T USE THIS OPTION IF YOUR CPU DOES NOT SUPPORT DYNAMIC BOOST**)
  - CPU_HWP_DYN_BOOST_ON_BAT=0 (**DON'T USE THIS OPTION IF YOUR CPU DOES NOT SUPPORT DYNAMIC BOOST**)
  - NMI_WATCHDOG=0
  - PLATFORM_PROFILE_ON_AC=performance
  - PLATFORM_PROFILE_ON_BAT=low-power
  - AHCI_RUNTIME_PM_ON_AC=on
  - AHCI_RUNTIME_PM_ON_BAT=auto
  - WIFI_PWR_ON_AC=off
  - WIFI_PWR_ON_BAT=on
  - WOL_DISABLE=Y
  - SOUND_POWER_SAVE_ON_AC=0
  - SOUND_POWER_SAVE_ON_BAT=1
  - PCIE_ASPM_ON_AC=performance
  - PCIE_ASPM_ON_BAT=powersupersave
  - RUNTIME_PM_ON_AC=on
  - RUNTIME_PM_ON_BAT=auto
  - START_CHARGE_THRESH_BAT0=85 (**USE THIS ONLY IF YOUR LAPTOP SUPPORTS BATTERY THRESHOLDS AND IF YOU WANT TO USE THIS FEATURE**)
  - STOP_CHARGE_THRESH_BAT0=90 (**USE THIS ONLY IF YOUR LAPTOP SUPPORTS BATTERY THRESHOLDS AND IF YOU WANT TO USE THIS FEATURE**)
  - NATACPI_ENABLE=1 (Battery care driver for **all supported laptops**)
  - TPACPI_ENABLE=1 (Battery care driver for **Thinkpads only**)
  - TPSMAPI_ENABLE=1 (Battery care driver for **Thinkpads only**)
## Throttled Configuration (DO NOT USE THROTTLED IF YOU DON'T HAVE AN INTEL CPU)
- Throttled was actually first started as a project to solve throttling issues due to a bug in Linux on Thinkpads, however now it seems to be fixing the same issue on other laptops as well. If you have an Intel CPU that supports **undervolting**, then you can use Throttled to prevent overheating. However, the values I'll be giving you are **WRITTEN FOR THINKPAD T490 (Intel Core i5-8265U) SPECIFICALLY, DO NOT APPLY THE SAME VALUES IF YOU HAVE DIFFERENT HARDWARE**"
- **Location**: sudo nano /etc/throttled.conf
  - [BATTERY]
    - Trip_Temp_C: 60
    - cTDP: 1
    - Disable_BDPROCHOT: False
  - [AC]
    - Trip_Temp_C: 80
    - HWP_Mode: True
    - cTDP: 2
    - Disable_BDPROCHOT: False
  - [UNDERVOLT.BATTERY]
    - CORE: -80
    - GPU: -80
    - CACHE: -80
    - UNCORE: -40
  - [UNDERVOLT.AC]
    - CORE: -60
    - GPU: -60
    - CACHE: -60
    - UNCORE: -40
## ZRAM Size Increase (Optional) 
- For 16 GB RAM, Arch Linux dedicates 4 GB ZRAM which is not enough for me. That's why I increase it to 8 GB. You can skip this step if you don't know what you're doing.
  - sudo nano /etc/systemd/zram-generator.conf
    - [zram0]
    - zram-size = 8192
  - sudo systemctl restart systemd-zram-setup@zram0.service
## Configure Fish (Optional)
- If you would like your terminal to predict what you are going to type with colorful letters, you might want to use Fish for your terminal.
  - sudo pacman -S fish
  - chsh -s /usr/bin/fish (you have to reboot after this command for next commands to work)
    - function fish_greeting
    - fastfetch
    - end
  - funcsave fish_greeting
## Picom Configuration
- After installing Picom, you have to **disable XFCE's default compositor** via following these steps:
  - Settings Manager - Window Manager Tweaks - Compositor - Enable Display Compositing (untick the box)
- After these steps, write these commands on terminal:
  - sudo nano ~/.config/picom.conf
    - backend = "glx";
    - glx-no-stencil = true;
    - fading = true;
    - vsync = true;
- And reboot your system to apply changes. You can set keybinds to disable and enable Picom since you might want to disable compositor while gaming to gain better performance. You can set keybinds using these steps:
  - **To Disable Picom**: Settings Manager - Keyboard - Application Shortcuts - Add - Command: killall picom - Command Shortcut: Your preferred key combination
  - **To Enable Picom**: Settings Manager - Keyboard - Application Shortcuts - Add - Command: picom - Command Shortcut: Your preferred key combination
## SDDM For XFCE
- SDDM looks better than LightDM, so why wouldn't we use it instead? :) I'm going to be using [Catppuccin SDDM](https://github.com/catppuccin/sddm/releases).
- **Needed Packages**: sudo pacman -S sddm qt6-svg qt6-declarative
- **Disable LightDM and enable SDDM**: sudo systemctl disable lightdm.service && sudo systemctl enable sddm.service
- **Add Catppuccin Theme**: Extract .zip file on your downloads directory and apply this command: **cd Downloads && sudo cp -r catppuccin-frappe /usr/share/sddm/themes/**
### Let's Edit SDDM
- **Location**: sudo nano /etc/sddm.conf.d/
  - [Theme]
  - Current=catppuccin-frappe (for example if you installed catppuccin-mocha, type catppuccin-mocha instead)
- And reboot your computer to apply changes.
## XFCE Ricing
- After applying your preferred (or the ones I installed) desktop and icon themes, you might want to make rices. However, if you would like an already made panel preset, here is [mine](https://drive.google.com/file/d/1ef-N87La8UkVuTtwFG6oRucCx9G8ujA3/view?usp=sharing)
- If you preferred using my panel preset, you can apply it following these steps:
  - Settings Manager - Panel Profiles - Import - Preset File - Çıt - Apply
## Dolby Atmos Setup (EasyEffects) - [Reference](https://www.reddit.com/r/thinkpad/comments/q5pt38/x1_extreme_gen_4_dolby_atmos_setup_for_linux/)
- After launching EasyEffects and setting it to launch at boot from app settings, download [this .zip file](https://www.mediafire.com/file/qt9znutry7fgzk7/dolby.zip/file) for Dolby Atmos presets.
- After downloading and extracting the .zip file, move the folder to a location you will remember the path of.
- Next, in EasyEffects, open **Effects** page and click on **Add Effect**. Then, add a **Convolver** and click on convolver.
- Click on **Impulses** and then **Import Impulse**, now add all of the .irs files you downloaded.
- Last, on **Impulses** page, it will be enough to load one of the presets (you can switch between presets).
