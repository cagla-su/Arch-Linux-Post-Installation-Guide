# İçindekiler
- [Başlangıç](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e-%C3%87eviri.md#ba%C5%9Flang%C4%B1%C3%A7)  
  - [AUR Yardımcısı Yükleme](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e-%C3%87eviri.md#aur-yard%C4%B1mc%C4%B1s%C4%B1-y%C3%BCkleme)
  - [En Uygun Mirror'ları Ayarlama](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e-%C3%87eviri.md#en-uygun-mirrorlar%C4%B1-ayarlama)
  - [CachyOS Depolarını ve Çekirdeğini Yükleme](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e-%C3%87eviri.md#-cachyos-depolar%C4%B1n%C4%B1-ve-%C3%A7ekirde%C4%9Fini-y%C3%BCkleme) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" />
  - [Gerekli Paketleri Yükleme](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e-%C3%87eviri.md#gerekli-paketleri-y%C3%BCkleme)
  - [Oyun Oynama Paketlerini Yükleme](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e-%C3%87eviri.md#oyun-oynama-paketlerini-y%C3%BCkleme)
- [Kapanış](https://github.com/cagla-su/Arch-Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e-%C3%87eviri.md#kapan%C4%B1%C5%9F)
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
## <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" /> CachyOS Depolarını ve Çekirdeğini Yükleme
<img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/9077599c-872d-4ff0-8cf6-81377867c7e5" /> CachyOS **performans odaklı** bir Linux dağıtımıdır, bu yüzden **daha yüksek performans için** onların **depolarını** ve **çekirdeğini** kullanıyorum.
```
curl -O https://mirror.cachyos.org/cachyos-repo.tar.xz
tar xvf cachyos-repo.tar.xz && cd cachyos-repo
sudo ./cachyos-repo.sh
sudo pacman -S linux-cachyos-bore
```
## Gerekli Paketleri Yükleme
```
sudo pacman -S unrar unzip ufw flatpak fwupd fastfetch mpv noto-fonts-cjk noto-fonts-emoji && sudo systemctl enable --now ufw.service
```
## Oyun Oynama Paketlerini Yükleme
```
sudo pacman -S gamemode lib32-gamemode steam lutris discord && flatpak install flathub com.heroicgameslauncher.hgl com.vysp3r.ProtonPlus
```
Ek olarak, **Vulkan sürücüleri** için [bu rehberi](https://github.com/lutris/docs/blob/master/InstallingDrivers.md#arch--manjaro--other-arch-linux-derivatives) takip ediyorum. **Linux'ta oyun oynama hakkında daha fazla bilgi edinmek** isterseniz, [Linux'ta oyun oynama rehberime](https://github.com/cagla-su/Linux-Gaming-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri/linuxta-oyun-oynama-rehberi.md) göz atmanızı tavsiye ederim.
# Kapanış
Bu rehber Arch Linux kurulum sonrası hakkındaydı! Umarım rehber faydalı olmuştur. Okuduğunuz için teşekkürler! <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/60e83c84-d8f8-4035-8052-08aabe1d83a1" />

