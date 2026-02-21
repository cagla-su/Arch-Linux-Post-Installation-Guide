# Linux Post-Installation Guide
# Table of Contents
- [Using Custom DNS](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#using-custom-dns)
- [System Configuration](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#system-configuration)
  - [systemd-boot Configuration](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#systemd-boot-configuration)
  - [Disabling NetworkManager-wait-online.service](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#disabling-networkmanager-wait-onlineservice)
- [Terminal Configuration](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#terminal-configuration-) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/ae34a1ca-71fe-4bf4-b1df-ddee947edaf5" />
  - [Fish Configuration](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#-fish-configuration) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/a4a4ce43-0e32-406f-951a-8761be2f9c5e" />
  - [Fastfetch Configuration](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#fastfetch-configuration)
- [Conclusion](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#conclusion)
## Türkçe Çeviri 🇹🇷
> [!NOTE]
> Rehberin [Türkçe çevirisi buradadır](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri.md). Birebir çeviri değildir ama içerik aynıdır.
## Using Custom DNS
```
sudo systemctl enable --now systemd-resolved
```
- After enabling `systemd-resolved`, follow the instructions of custom DNS you want to use. My suggestion is either <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/b3b22da0-bb93-4ad8-897d-60023db6aa5c" /> [Mullvad DNS](https://mullvad.net/en/help/dns-over-https-and-dns-over-tls) or <img width="16" height="25" alt="image-removebg-preview" src="https://github.com/user-attachments/assets/17f508fa-4c9c-4d74-9f27-f7afaed205c6" /> [NextDNS](https://nextdns.io/)
# System Configuration
## systemd-boot Configuration
> [!IMPORTANT]
> Skip this step if you are using a **different bootloader** such as **GRUB**.
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
- If you **can see the custom kernel** here, everything is fine.
- If you **cannot**, looking at the output you get, go to the location of Linux kernel you are using and **copy the .conf file with a different name** (linux-cachyos-bore) and edit the file:
```
sudo nano /boot/loader/entries/linux-cachyos-bore.conf
```
```
title   Arch Linux (linux-cachyos-bore)
linux   /vmlinuz-linux-cachyos-bore
initrd  /initramfs-linux-cachyos-bore.img
options # DO NOT TOUCH THIS LINE
```
- When you reboot, you will **be able to switch** to the custom kernel.
## Disabling NetworkManager-wait-online.service
- For a **faster boot time**, disable `NetworkManager-wait-online.service`:
```
sudo systemctl disable NetworkManager-wait-online.service
```
# Terminal Configuration <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/ae34a1ca-71fe-4bf4-b1df-ddee947edaf5" />
## <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/a4a4ce43-0e32-406f-951a-8761be2f9c5e" /> Fish Configuration
If you would like your terminal to **predict what you are going to type**, I suggest that you use <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/a4a4ce43-0e32-406f-951a-8761be2f9c5e" /> [Fish](https://fishshell.com/) for your terminal.
```
sudo pacman -S fish
```
```
chsh -s /usr/bin/fish # you should reboot after running the command
```
> [!NOTE]
> - If terminal tells you that the **process has failed**, try `chsh -s /bin/fish` instead.
> - Additionally, if you would like to see **fastfetch every time you launch terminal**, you should **execute the commands below**:
```
  function fish_greeting
  fastfetch
  end
```
```
funcsave fish_greeting
```
## fastfetch Configuration
> [!WARNING]
> - Fastfetch's default theme is *usually useful* but if you would like to **try my** fastfetch **theme**, you should **execute the commands below**.
> - The picture below is an **example** of how **my** fastfetch theme looks like. If you did not like it, please **skip this step**.
<img width="712" height="375" alt="image" src="https://github.com/user-attachments/assets/4839909f-dc9a-43f0-afca-14f3ac4a2dd8" />

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
# Conclusion
This guide was about Linux post-installation! I hope the guide has been useful. Thank you for reading! <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/60e83c84-d8f8-4035-8052-08aabe1d83a1" />
