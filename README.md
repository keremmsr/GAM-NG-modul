# Kernel Redline (OnePlus 13)

OnePlus 13 için hobi olarak hazırladığım Magisk/KernelSU modülleri. Oyun sırasında akıcılık ve dokunmatik tepkisi üzerine denemeler yapıyorum.

> **Uyarı:** Modüller root gerektirir ve sistem/kernel düğümlerine yazar. Kendi cihazımda, OnePlus 13 üzerinde denedim; başka cihazlarda test edilmedi. Kullanım sorumluluğu sana aittir. Takılma yaşarsan modülü Magisk/KernelSU içinden devre dışı bırakıp yeniden başlat.

## İçindekiler

| Klasör | Zip | Açıklama |
|---|---|---|
| `KernelRedline/` | `KernelRedline-v2.7.3.zip` | CPU/GPU ayarları, oyun modu, GPU test döngüsü |
| `GyroAxisLock/` | `GyroAxisLock-v2.6.zip` | Jiroskop ayarları (yalnızca prop) |
| `ReactTouch/` | `ReactTouch-v1.2.zip` | Dokunmatik ekran tepkisi (üçüncü taraf, aşağıya bak) |

## Kernel Redline

- **İki mod:** *Aggressive* (oyun) ve *Stock* (fabrika değerleri). Aggressive modda WALT zamanlayıcı ayarları, animasyonların kapatılması ve HW overlay kapatma uygulanır.
- **Öncelik modu (`priority.mode=aktune`):** Cihaz veya başka bir modül bir değeri değiştirirse modül kendi değerini geri yazar. Kontrol hafif tutulur; ekran kapalıyken seyrek çalışır.
- **GPU profilleri (Adreno 830):** `balanced` (443 MHz), `performance` (660 MHz, varsayılan), `extreme` (832 MHz) veya `custom`. Değer, cihazın desteklediği frekans basamağına yuvarlanır.
- **GPU termal koruma:** GPU 80°C'ye ulaşınca GPU ayarları bırakılır, 72°C'ye inince geri uygulanır. Kernel'in kendi termal sınırları aşılmaz.
- **Action tuşu = GPU test döngüsü:** Magisk/KernelSU'daki *Action* tuşuna her basışta sıradaki adıma geçilir:
  1. Yalnızca `force_no_nap` açık, diğer üçü kapalı
  2. Yalnızca `force_clk_on` kapalı, diğer üçü açık
  3. `force_clk_on` + `force_bus_on` kapalı, diğer ikisi açık
  4. 3. adım + `msm-adreno-tz` governor (kernel listeliyorsa)
  5. Dört `force_*` kapalı (bus değerleri cihazda kalır)
  6. Stok mod
- **Ayar dosyası:** Kurulumdan sonra `/data/adb/aktune/config.props`. Değişiklikler yeniden başlatma gerekmeden birkaç saniye içinde uygulanır. Durum bilgisi `/data/adb/aktune/state/status` dosyasında.

Not: GPU governor olarak cihazda yalnızca `msm-adreno-tz` listeleniyor; modül yeni bir governor eklemez.

## Gyro Axis Lock

Ham jiroskop 1000 Hz, `gyro_fifo=0`, eksen yeniden eşleme ve koordinat dönüşümü; sensör temizliği ve yakınlık sensörü açık kalır. Sadece sistem prop'ları değiştirir.

## ReactTouch

Bu modül **bana ait değil**: yazarı [@Zyarexx](https://t.me/Zyarexx). Burada yalnızca kendi kurulumumun parçası olduğu için, değiştirilmeden bulunuyor. Hakları ve emeği orijinal yazara aittir.

## Kurulum

1. İlgili `.zip` dosyasını telefona kopyala.
2. Magisk veya KernelSU'da *Modüller* bölümünden zip'i yükle.
3. Cihazı yeniden başlat.

## Kaynak ve teşekkür

Kernel Redline, **AKTune** (NSLabs / KaijinLab) tabanlı olup OnePlus 13 için değiştirilmiş ve genişletilmiştir. Orijinal proje ve yazarları için teşekkürler.

## Yazar

kerems
