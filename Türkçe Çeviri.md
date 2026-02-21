# İçindekiler
- [Özel DNS Kullanma](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri.md#%C3%B6zel-dns-kullanma)
- [NetworkManager-wait-online.service Hizmetini Devre Dışı Bırakma](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri.md#networkmanager-wait-onlineservice-hizmetini-devre-d%C4%B1%C5%9F%C4%B1-b%C4%B1rakma)
- [Terminal Yapılandırması](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri.md#terminal-yap%C4%B1land%C4%B1rmas%C4%B1-) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/ae34a1ca-71fe-4bf4-b1df-ddee947edaf5" />
  - [Fish Yapılandırması](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri.md#-fish-yap%C4%B1land%C4%B1rmas%C4%B1) <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/a4a4ce43-0e32-406f-951a-8761be2f9c5e" />
  - [fastfetch Yapılandırması](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri.md#fastfetch-yap%C4%B1land%C4%B1rmas%C4%B1)
- [Kapanış](https://github.com/cagla-su/Linux-Post-Installation-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri.md#kapan%C4%B1%C5%9F)
# Özel DNS Kullanma
```
sudo systemctl enable --now systemd-resolved
```
- `systemd-resolved` hizmetini etkinleştirdikten sonra, kullanmak istediğiniz özel DNS'in adımlarını takip edin. Benim tavsiyelerim aşağıdadır:
- <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/c80c1141-f1a6-43ce-a153-2566c6a28295" /> [Cloudflare DNS](https://developers.cloudflare.com/1.1.1.1/setup/linux/)
    - **En hızlısıdır** fakat **gizlilik** konusunda **en zayıfıdır**.
- <img width="16" height="25" alt="image-removebg-preview" src="https://github.com/user-attachments/assets/17f508fa-4c9c-4d74-9f27-f7afaed205c6" /> [NextDNS](https://nextdns.io/)
    - <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/c80c1141-f1a6-43ce-a153-2566c6a28295" /> Cloudflare'den sonra **en hızlı ikinci** DNS'tir fakat **gizlilik** konusunda **oldukça iyidir**.
-   <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/b3b22da0-bb93-4ad8-897d-60023db6aa5c" /> [Mullvad DNS](https://mullvad.net/en/help/dns-over-https-and-dns-over-tls)
    - **Hız** konusunda **fena değildir** fakat **gizlilik** konusunda **en iyisidir**.
# Oyun Oynama
**Linux'ta oyun oynama** hakkında ayrı bir rehberim mevcuttur. Rehbere [buradan ulaşabilirsiniz](https://github.com/cagla-su/Linux-Gaming-Guide/blob/main/T%C3%BCrk%C3%A7e%20%C3%87eviri/linuxta-oyun-oynama-rehberi.md).
# Dizüstü Bilgisayarlar
**Dizüstü bilgisayarlar** ama **esas olarak Thinkpad bilgisayarlar için** ayrı bir rehberim mevcuttur. Rehbere [buradan ulaşabilirsiniz](https://github.com/cagla-su/Thinkpad-Linux-Optimization-Guide).
# Linux'ta Android Kullanma
**Linux'ta <img width="16" height="25" alt="image-removebg-preview(1)" src="https://github.com/user-attachments/assets/cec27060-1d67-48e1-8f29-a3a5b639fde8" /> Android kullanma** hakkında ayrı bir rehberim mevcuttur. Rehbere [buradan ulaşabilirsiniz](https://github.com/cagla-su/Waydroid-Guide/blob/main/Waydroid-Rehberi.md).
# NetworkManager-wait-online.service Hizmetini Devre Dışı Bırakma
**Daha çabuk başlatma zamanı** için, `NetworkManager-wait-online.service` hizmetini devre dışı bırakın:
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
> [!NOTE]
> - Eğer terminaliniz size **işlemin başarısız olduğunu** söylerse, `chsh -s /bin/fish`'i deneyin.
> - Ek olarak, **terminali her çalıştırdığınızda** **fastfetch**'i görmek isterseniz, **aşağıdaki komutları çalıştırmalısınız**:
```
  function fish_greeting
  fastfetch
  end
```
```
funcsave fish_greeting
```
## fastfetch Yapılandırması
> [!WARNING]
> - Fastfetch'in varsayılan teması *genellikle kullanışlıdır* fakat **benim** fastfetch **temamı denemek** isterseniz, **aşağıda bulunan komutları çalıştırmalısınız**.
> - Aşağıda **kendi** fastfetch temamın bir **örneği** bulunmaktadır. Beğenmediyseniz lütfen **bu adımı atlayın**.
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
# Kapanış
Bu rehber Linux kurulum sonrası hakkındaydı! Umarım rehber faydalı olmuştur. Okuduğunuz için teşekkürler! <img width="16" height="25" alt="image" src="https://github.com/user-attachments/assets/60e83c84-d8f8-4035-8052-08aabe1d83a1" />

