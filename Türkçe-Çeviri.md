# Table of Contents
- [Get Started](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#get-started)  
  - [Installing AUR Helper](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#installing-aur-helper)
  - [Ranking Mirrors](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#ranking-mirrors)
  - [Using Custom DNS](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#using-custom-dns)
  - [Installing CachyOS Repositories and Kernel](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#installing--cachyos-repositories-and-kernel) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" />
  - [Installing Necessary Packages](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#installing-necessary-packages)
  - [Installing Gaming Packages](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#installing-gaming-packages)
- [System Configuration](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#system-configuration)
  - [systemd-boot Configuration](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#systemd-boot-configuration)
  - [TLP Configuration](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#tlp-configuration)
  - [Little Performance Tweaks](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#little-performance-tweaks)
    - [Reducing the vm.swappiness Value](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#reducing-the-vmswappiness-value)
    - [Disabling NetworkManager-wait-online.service](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#disabling-networkmanager-wait-onlineservice)
- [Terminal Configuration](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#terminal-configuration-) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/ae34a1ca-71fe-4bf4-b1df-ddee947edaf5" />
  - [Fish Configuration](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#-fish-configuration) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/a4a4ce43-0e32-406f-951a-8761be2f9c5e" />
  - [Fastfetch Configuration](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#fastfetch-configuration)
- [Dolby Atmos Setup (EasyEffects)](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#-dolby-atmos-setup--easyeffects) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/076989c3-9b17-4ff4-822e-91d60e209632" /> <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/318f8066-239b-45b1-ba4c-d5de14fe597f" />
- [Conclusion](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide?tab=readme-ov-file#conclusion)
## Türkçe Çeviri 🇹🇷
Rehberin [Türkçe çevirisi buradadır](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e-%C3%87eviri.md). Birebir çeviri değildir ama içerik aynıdır.
# Arch Linux Kurulum Sonrası Rehberi
Esenlikler. Bu rehberde **<img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/17e40f3d-086e-4979-bd7a-786ce5864c66" /> Arch Linux kurulumu sonrasında sisteminizi nasıl kullanıma hazır hâle getireceğiniz** hakkında bilgilendirileceksiniz. Hazırsanız, başlayalım!
# Başlangıç
## AUR Yardımcısı Yükleme
Genelde kullanıcılar [yay](https://github.com/Jguer/yay) kullanmayı tercih eder fakat ben [paru](https://github.com/Morganamilo/paru) tercih ediyorum çünkü daha iyi olduğunu düşünüyorum.
```
sudo pacman -S --needed base-devel git && git clone https://aur.archlinux.org/paru.git && cd paru && makepkg -si
```
## En Uygun Mirror'ları Ayarlama
```
sudo pacman -S reflector
```
```
sudo reflector --country Türkiye --latest 5 --sort rate --save /etc/pacman.d/mirrorlist
```
- Türkiye'de yaşamıyorsanız `--country` değerini yaşadığınız ülkenin adıyla değiştirin.
## Özel DNS Kullanma
```
sudo systemctl enable --now systemd-resolved
```
- `systemd-resolved` hizmetini etkinleştirdikten sonra, kullanmak istediğiniz özel DNS'in adımlarını takip edin. Benim tavsiyem <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/52a59002-d12c-403b-ae21-6d63aa8d4a2f" /> [Cloudflare DNS](https://developers.cloudflare.com/1.1.1.1/setup/linux/#systemd-resolved) veya <img width="16" height="25" alt="image-removebg-preview" src="https://github.com/user-attachments/assets/17f508fa-4c9c-4d74-9f27-f7afaed205c6" /> [NextDNS](https://nextdns.io/)'dir.
## <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" /> CachyOS Depolarını ve Çekirdeğini Yükleme
<img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" /> CachyOS **performans odaklı** bir Linux dağıtımıdır, bu yüzden **daha yüksek performans için** onların **depoları** ve **çekirdeğini** kullanıyorum.
```
curl -O https://mirror.cachyos.org/cachyos-repo.tar.xz
tar xvf cachyos-repo.tar.xz && cd cachyos-repo
sudo ./cachyos-repo.sh
sudo pacman -S linux-cachyos-bore
```
## Gerekli Paketleri Yükleme
```
sudo pacman -S unrar unzip ufw tlp flatpak fwupd fastfetch mpv noto-fonts-cjk noto-fonts-emoji 
```
```
sudo systemctl enable --now ufw.service && sudo systemctl enable --now tlp.service
```
## Oyun Oynama Paketlerini Yükleme
```
sudo pacman -S gamemode lib32-gamemode steam lutris prismlauncher discord && flatpak install flathub org.vinegarhq.Sober com.heroicgameslauncher.hgl com.vysp3r.ProtonPlus
```
Ek olarak, **Vulkan sürücüleri** için [bu rehberi](https://github.com/lutris/docs/blob/master/InstallingDrivers.md#arch--manjaro--other-arch-linux-derivatives) takip ediyorum. **Linux'ta oyun oynama hakkında daha fazla bilgi edinmek** isterseniz, [Linux'ta oyun oynama rehberime](https://github.com/cagla-su/Linux-Gaming-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri/linuxta-oyun-oynama-rehberi.md) göz atmanızı tavsiye ederim.
# Sistem Yapılandırması
## systemd-boot Yapılandırması
- Eğer **GRUB** gibi **başka bir önyükleyici** kullanıyorsanız bu adımı atlayın.
```
sudo nano /boot/loader/loader.conf
```
```                      
default @saved
timeout 5
```
- Ek olarak, systemd-boot **<img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" /> CachyOS çekirdeğini algılamayabilir**, bu durumda şu adımları takip edin:
```
ls /boot/loader/entries/*
```
- Eğer **özel çekirdeğinizi görebiliyorsanız**, her şey yolunda demektir.
- Eğer **göremiyorsanız**, elde ettiğiniz çıktıya bakarak, kullandığınız Linux çekirdeğinin konumuna gidin ve **.conf dosyasını başka bir isim kullanarak kopyalayın** (linux-cachyos-bore) ve dosyayı düzenleyin:
```
sudo nano /boot/loader/entries/linux-cachyos-bore.conf
```
```
title   Arch Linux (linux-cachyos-bore)
linux   /vmlinuz-linux-cachyos-bore
initrd  /initramfs-linux-cachyos-bore.img
options # BU SATIRA DOKUNMAYIN
```
- Cihazınızı yeniden başlattığınızda özel çekirdeğe **geçiş yapabileceksiniz**.
## TLP Yapılandırması
- TLP Linux kullanan dizüstü bilgisayarlar için **gelişmiş bir güç yöneticisidir**.
  - Eğer **masaüstü bilgisayar** kullanıyorsanız, bunun yerine [Tuned](https://medium.com/@jeromedecinco/tuned-in-linux-optimizing-system-performance-with-profiles-1c852acfb02e) kullanın.
- Yapılandırma dosyasını düzenlerken aşağıda bahsedilen **her seçeneğin başındaki # işaretini kaldırdığınızdan** emin olun.
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
## Küçük Performans Ayarlamaları
### vm.swappiness Değerini Düşürme
- Eğer **16 GB veya daha fazla RAM'e** sahipseniz, `vm.swappiness` değerini düşürmek **daha yüksek performans** almanızı sağlar.
  - Ancak, eğer **16 GB'dan daha az RAM'e sahipseniz, bu adımı atlayın**.
```
sudo nano /etc/sysctl.conf
```
```                            
vm.swappiness=10
```
```
sudo sysctl -p
```
### NetworkManager-wait-online.service Hizmetini Devre Dışı Bırakma
- **Daha çabuk başlatma zamanı** için, `NetworkManager-wait-online.service` hizmetini devre dışı bırakın:
```
sudo systemctl disable NetworkManager-wait-online.service
```
# Terminal Yapılandırması <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/ae34a1ca-71fe-4bf4-b1df-ddee947edaf5" />
## <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/a4a4ce43-0e32-406f-951a-8761be2f9c5e" /> Fish Yapılandırması
Eğer terminalinizin **ne yazacağınızı tahmin etmesini** isterseniz, <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/a4a4ce43-0e32-406f-951a-8761be2f9c5e" /> [Fish](https://fishshell.com/) kullanmanızı tavsiye ederim.
```
sudo pacman -S fish
```
```
chsh -s /usr/bin/fish # komutu çalıştırdıktan sonra bilgisayarınızı yeniden başlatın
```
- Eğer terminaliniz size **işlemin başarısız olduğunu** söylerse, `chsh -s /bin/fish`'i deneyin.
- Ek olarak, terminali her çalıştırdığınızda **fastfetch**'i görmek isterseniz, aşağıdaki komutu çalıştırmalısınız:
```
  function fish_greeting
  fastfetch
  end
```
```
funcsave fish_greeting
```
## fastfetch Yapılandırması
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
# Kapanış
Bu rehber Arch Linux kurulum sonrası hakkındaydı! Umarım rehber faydalı olmuştur. Okuduğunuz için teşekkürler! <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/60e83c84-d8f8-4035-8052-08aabe1d83a1" />

