# Linux Post-Installation Guide
# Table of Contents
- [Using Custom DNS](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#using-custom-dns)
- [Disabling NetworkManager-wait-online.service](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#disabling-networkmanager-wait-onlineservice)
- [Terminal Configuration](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#terminal-configuration-) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/ae34a1ca-71fe-4bf4-b1df-ddee947edaf5" />
  - [Fish Configuration](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#-fish-configuration) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/a4a4ce43-0e32-406f-951a-8761be2f9c5e" />
  - [fastfetch Configuration](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#fastfetch-configuration)
- [Conclusion](https://github.com/cagla-su/Linux-Post-Installation-Guide?tab=readme-ov-file#conclusion)
## Türkçe Çeviri 🇹🇷
> [!NOTE]
> Rehberin [Türkçe çevirisi buradadır](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri.md). Birebir çeviri değildir ama içerik aynıdır.
## Distribution-Specific Guides
- <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/17e40f3d-086e-4979-bd7a-786ce5864c66" /> **Arch Linux -** [Arch Linux Post-Installation Guide](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/Distro-Specific/Arch-Linux.md)
    - <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/17e40f3d-086e-4979-bd7a-786ce5864c66" /> 🇹🇷 **Türkçe Hali -** [Arch Linux Kurulum Sonrası Rehberi](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/Da%C4%9F%C4%B1t%C4%B1ma%20%C3%96zel/Arch-Linux-TR.md)
# Using Custom DNS
```
sudo systemctl enable --now systemd-resolved
```
- After enabling `systemd-resolved`, follow the instructions of custom DNS you want to use. My suggestions are listed below:
-  <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/c80c1141-f1a6-43ce-a153-2566c6a28295" /> [Cloudflare DNS](https://developers.cloudflare.com/1.1.1.1/setup/linux/)
    - **The fastest** but **weak** when it comes to **privacy**.
-  <img width="16" height="25" alt="image-removebg-preview" src="https://github.com/user-attachments/assets/ee74ad8d-6a6f-4359-ab5a-3b009f6bb527" /> [NextDNS](https://nextdns.io/)
    - **The second fastest** after <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/c80c1141-f1a6-43ce-a153-2566c6a28295" /> Cloudflare but **really good** when it comes to **privacy**.
-  <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/b3b22da0-bb93-4ad8-897d-60023db6aa5c" /> [Mullvad DNS](https://mullvad.net/en/help/dns-over-https-and-dns-over-tls)
    - **Not bad** in terms of **speed** but **the best** when it comes to **privacy**. 
# Gaming
I have a separate guide about **gaming on Linux**. You can check the guide [from here](https://github.com/cagla-su/Linux-Gaming-Guide).
# Laptops
I have a separate optimization guide for **laptops** but **mainly for Thinkpads**. You can check the guide [from here](https://github.com/cagla-su/Thinkpad-Linux-Optimization-Guide).
# Use Android on Linux <img width="16" height="25" alt="image-removebg-preview(1)" src="https://github.com/user-attachments/assets/cec27060-1d67-48e1-8f29-a3a5b639fde8" />
I have a separate guide about **using <img width="16" height="25" alt="image-removebg-preview(1)" src="https://github.com/user-attachments/assets/cec27060-1d67-48e1-8f29-a3a5b639fde8" /> Android on Linux**. You can check the guide [from here](https://github.com/cagla-su/Waydroid-Guide).
# Disabling NetworkManager-wait-online.service
For a **faster boot time**, disable `NetworkManager-wait-online.service`:
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
<img width="722" height="343" alt="image" src="https://github.com/user-attachments/assets/51ac5587-8963-4017-83b2-d78b2aa588b0" />

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
"1": "blue",
"2": "blue"
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
      "keyColor": "white"
    },
    {
      "type": "os",
      "key": "│ Operating System",
      "keyColor": "white"
    },
    {
      "type": "kernel",
      "key": "│ Kernel",
      "keyColor": "white"
    },
{
      "type": "packages",
      "key": "│ Packages",
      "keyColor": "white"
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
      "keyColor": "cyan"
    },
    {
      "type": "gpu",
      "key": "│ Graphics Card",
      "keyColor": "cyan"
    },
    {
      "type": "memory",
      "key": "│ Memory",
      "keyColor": "cyan"
    },
    {
      "type": "disk",
      "key": "│ Disk",
      "keyColor": "cyan"
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
