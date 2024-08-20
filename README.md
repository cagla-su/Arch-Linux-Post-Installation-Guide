# Çıt's Arch Linux Post-Installation Guide (XFCE) - Thinkpad T490
Hello. I wrote this guide for **Thinkpad T490 and XFCE specifically**, however you can still follow all the steps if you don't have the same computer as I have. So, let's begin!

## Install AUR Helper
Normally, everyone prefers **yay** but I prefer **paru** since it is written in **rust**.
### Install Paru AUR Helper
sudo pacman -S --needed base-devel git && git clone https://aur.archlinux.org/paru.git && cd paru && makepkg -si
## Install CachyOS Repositories and BORE Kernel (Optional)
CachyOS is a **performance focused Arch-based** Linux distribution. If you would like an **out of the box experience** (it can be considered out of the box compared to Arch), I would simply install CachyOS. However, I just want to use their greatly optimized repositories and kernel while configuring every other things about my system on my own. **Be careful, do not use CachyOS kernel if you need good battery life!**
### Install
wget https://mirror.cachyos.org/cachyos-repo.tar.xz && tar xvf cachyos-repo.tar.xz && cd cachyos-repo && sudo ./cachyos-repo.sh && sudo pacman -S linux-cachyos-bore
## GRUB Configuration
GRUB_CMDLINE_LINUX_DEFAULT="mitigations=off" (do not remove the already existing parameters, just add mitigations=off next to them)
GRUB_DEFAULT=saved
GRUB_SAVEDEFAULT=true
GRUB_DISABLE_SUBMENU=y
### Information About GRUB Configuration
- **You have to apply this command to apply changes**: sudo grub-mkconfig -o /boot/grub/grub.cfg
- CPU mitigations reduce performance by 30% on these CPUs:
  - **AMD**: Zen 1, Zen 1+, Zen 2
  - **Intel**: 6th, 7th and 8th Generation
  - This is why you might want to disable mitigations via **mitigations=off** kernel parameter especially if you're gaming. However, disabled mitigations might introduce security risks. If you care about security more than performance, do not disable mitigations.
## Intel iGPU Configuration For X11
- Some projects such as Debian, Fedora, KDE, Mozilla suggest **modesetting** driver instead of using **xf86-video-intel** with **intel** driver as it is known to have problems with lower performance. However, using **modesetting** driver can cause issues such as **screen tearing** but we'll be using **Picom** with vsync on, so screen tearing won't be an issue as long as Picom is running.
- **Terminal Command For Intel Configuration**: sudo nano /etc/X11/xorg.conf.d/20-intel.conf
  - Section "Device"
  Identifier "Intel Graphics"
  Driver "modesetting"
  Option "Backlight" "intel_backlight"
  Option "AccelMethod" "glamor"
  Option "TearFree" "false"
  Option "RenderAccel" "true"
  Option "SwapbuffersWait" "false"
  Option "DRI" "2"
  Option "Throttle" "false"
  Option "FramebufferCompression" "false"
  VideoRam 24576
  Option "TripleBuffer" "false"
  Option "Shadow" "false"
  Option "LinearFramebuffer" "true"
  Option "RelaxedFencing" "false"
  Option "BufferCache" "true"
EndSection
