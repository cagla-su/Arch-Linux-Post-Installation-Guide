# Table of Contents
- [Get Started](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#get-started)  
  - [Installing AUR Helper](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#installing-aur-helper)
  - [Ranking Mirrors](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#ranking-mirrors)
  - [Installing CachyOS Repositories and Kernel](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#installing--cachyos-repositories-and-kernel) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" />
  - [Installing Necessary Packages](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#installing-necessary-packages)
  - [Installing Gaming Packages](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#installing-gaming-packages)
- [Conclusion](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#conclusion)
# Get Started
## Installing AUR Helper
Generally, users prefer [yay](https://github.com/Jguer/yay) but I prefer [paru](https://github.com/Morganamilo/paru) because I think it is better.
```
sudo pacman -S --needed base-devel git && git clone https://aur.archlinux.org/paru.git && cd paru && makepkg -si
```
## Ranking Mirrors
```
sudo pacman -S reflector
```
```
sudo reflector --country Türkiye --latest 5 --sort rate --save /etc/pacman.d/mirrorlist
```
- Make sure to change the country name according to the country you are living.
## Installing Necessary Packages
```
sudo pacman -S unrar unzip ufw flatpak fwupd fastfetch mpv noto-fonts-cjk noto-fonts-emoji && sudo systemctl enable --now ufw.service
```

## Installing Gaming Packages
```
sudo pacman -S gamemode lib32-gamemode steam lutris discord && flatpak install flathub com.heroicgameslauncher.hgl com.vysp3r.ProtonPlus
```
# Conclusion
This guide was about Arch Linux post-installation! I hope the guide has been useful. Thank you for reading! <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/60e83c84-d8f8-4035-8052-08aabe1d83a1" />
