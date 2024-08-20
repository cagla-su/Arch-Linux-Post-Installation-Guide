# **Çıt's Arch Linux Post-Installation Guide - Thinkpad T490**
Hello. I wrote this guide for **Thinkpad T490 specifically**, however you can still follow all the steps if you don't have the same computer as I have. So, let's begin!

## Install AUR Helper
Normally, everyone installs yay but I prefer paru since it is written in rust.
### Install Paru AUR Helper
sudo pacman -S --needed base-devel git && git clone https://aur.archlinux.org/paru.git && cd paru && makepkg -si
