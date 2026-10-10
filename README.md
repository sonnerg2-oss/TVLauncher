# 📺 TV Launcher

![Android TV](https://img.shields.io/badge/Platform-Android%20TV%20%7C%20Google%20TV-3DDC84?style=for-the-badge&logo=android)
![Kotlin](https://img.shields.io/badge/Language-Kotlin-7F52FF?style=for-the-badge&logo=kotlin)
![Compose for TV](https://img.shields.io/badge/UI-Jetpack%20Compose%20for%20TV-4285F4?style=for-the-badge&logo=jetpackcompose)
![Min SDK](https://img.shields.io/badge/Min%20SDK-24%20%28Android%207.0%2B%29-orange?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

**TV Launcher**, Android TV, Google TV ve Clone TV Box (Android 9, 10, 11, 12, 13, 14) cihazlar için geliştirilmiş, 4 slotlu, hızlı ve verimlilik odaklı modern ana ekran uygulamasıdır. **Kotlin** ve **Jetpack Compose for TV** (`androidx.tv.material3`) mimarisi kullanılarak %100 yerli ve performanslı bir yapıda inşa edilmiştir.

---

## ✨ Öne Çıkan Özellikler

- 🟡🔴🟢🔵 **4 Renkli Özelleştirilebilir Slot Kartları:**
  - **Slot 1:** Sarı (`#FFD700`) Çerçeve
  - **Slot 2:** Kırmızı (`#FF3B30`) Çerçeve
  - **Slot 3:** Yeşil (`#34C759`) Çerçeve
  - **Slot 4:** Mavi (`#007AFF`) Çerçeve
  - Boş slotlara tıklayarak cihazdaki herhangi bir uygulamayı tek tıkla atayabilirsiniz.

- 🎮 **Xiaomi / TV Kumanda Tuş Değiştirici (Button Remapper):**
  - Cihazdaki kaynak uygulamaları (**Netflix**, **Prime Video**, **YouTube**, **Canlı TV**) otomatik analiz eder.
  - Kumanda üzerindeki fiziksel tuşlara basıldığında açılacak uygulamayı kendi istediğiniz uygulama veya slota yönlendirmenizi sağlar.
  - Farklı markaların kumanda kod yürütmeleri için **5 adet ekstra özel kumanda tercih profili** içerir.

- 🏠 **Akıllı Home Tuşu Devralma (Erişilebilirlik Hizmeti):**
  - Google TV, Chromecast, TCL, Sony, Xiaomi gibi fabrika kilitli launcher değişimine izin vermeyen cihazlarda Erişilebilirlik Hizmeti ile Home tuşu basımlarını dinamik devralır.

- 🛡️ **Google Play & Play Protect Politikalarına %100 Uyum:**
  - En düşük yetki ilkesi (`canRetrieveWindowContent="false"`, `canPerformGestures="false"`, `typeWindowStateChanged`) kullanır.
  - Şeffaf ve kullanıcı onaylı **Prominent Disclosure (Açık Rıza Bildirimi)** diyaloğu içerir.

- ⚡ **Clone TV Box (Android 9, 10, 11, 12) Tam Desteği:**
  - `QUERY_ALL_PACKAGES` izni ile Android 11+ (API 30, 31, 32) cihazlarda gizlenen tüm 3. taraf APK'ları eksiksiz tarar.
  - Amlogic (Droidlogic), Rockchip, Allwinner, Softwinner sistem ayarları yönlendirme katmanına sahiptir.

- 🟠 **Turuncu Odak Çerçeveli TV Arayüzü:**
  - D-Pad kumanda ile gezinirken menü ve uygulama seçimlerinde turuncu (`#FF9800`) odak çerçevesi ve 60/120 FPS akıcı performans.

- 🌐 **Ağ & Canlı Saat Göstergesi:**
  - Anlık Wi-Fi sinyal seviyesi, internet bağlantı doğrulama noktası (Online/No Internet/Offline) ve canlı saat gösterimi.

---

## 🛠️ Google TV & Android TV'de Varsayılan Launcher Yapma

Google TV cihazlarda (`com.google.android.apps.tv.launcherx` / `com.google.android.tvlauncher`) fabrika çıkışlı launcher değişimi kilitli olabilir. Uygulama içerisinde sunulan yöntemler:

### 1. Erişilebilirlik Hizmeti İle Devralma (En Etkili Çözüm)
1. TV Launcher ana ekranında üst bardaki **Home (🏠)** ikonuna veya uyarı bandına tıklayın.
2. **2. Home Tuşunu Yakala (Erişilebilirlik)** seçeneğine tıklayın.
3. Güvenlik bilgilendirme diyalogunu onaylayıp cihazın **Erişilebilirlik (Accessibility)** ayarlarından **TV Launcher** hizmetini açık konuma getirin.
4. Artık kumandanızdaki Home tuşuna basıldığında doğrudan TV Launcher açılacaktır.

### 2. Uygulama İçi Sistem Ayarları
- **Varsayılan Ev Uygulaması Seç:** Cihazın sistem launcher seçim ekranını açar.
- **Google TV Launcher Varsayılanlarını Temizle:** Varsayılan Google Launcher uygulamasının yetkilerini sıfırlamak için detay sayfasını açar.

### 3. ADB Komutları İle Yapılandırma
Bilgisayarınızdan ADB bağlantısı kurarak varsayılan launcher yapabilirsiniz:

```bash
# TV Launcher'ı varsayılan ev uygulaması olarak belirler:
adb shell cmd package set-home-activity com.example.tvlauncher/.MainActivity

# İsteğe bağlı: Google TV Launcher'ı devre dışı bırakır:
adb shell pm disable-user --user 0 com.google.android.apps.tv.launcherx

# İsteğe bağlı: Android TV Launcher'ı devre dışı bırakır:
adb shell pm disable-user --user 0 com.google.android.tvlauncher

# Google TV Launcher'ı tekrar açmak isterseniz:
adb shell pm enable com.google.android.apps.tv.launcherx
```

---

## 🚀 Çalıştırma ve Kurulum

1. Projeyi **Android Studio** ile açın ve Gradle Sync işleminin tamamlanmasını bekleyin.
2. Android TV emülatörünü veya gerçek TV cihazını bağlayın:
   ```bash
   adb connect <TV-IP-ADRESI>:5555
   ```
3. **Run ▶** butonu ile kurun veya derlenmiş APK'yı yükleyin:
   ```bash
   adb install -r app/build/outputs/apk/debug/app-debug.apk
   ```

---

## 🕹️ Kumanda Kısayolları

- **Sol / Sağ:** Slot kartları arasında gezinme
- **OK (Orta Tuş):** Slot doluysa uygulamayı açar, boşsa uygulama seçiciyi açar.
- **Uzun Basma (OK):** Slot içerisindeki uygulamayı değiştirir veya sıfırlar.
- **Yukarı:** Home kurulum menüsü (🏠) ve sistem ayarlarını (⚙️) açar.

---

## 🏗️ Mimari ve Teknoloji Yığını

- **Dil:** Kotlin
- **Arayüz Katmanı:** Jetpack Compose for TV (`androidx.tv.material3`) + Foundation
- **Asenkron Akış:** Kotlin Coroutines + Flow + StateFlow (`Dispatchers.IO`)
- **Yerel Depolama:** Jetpack DataStore Preferences
- **Servis Katmanı:** AccessibilityService API (Key Filtering & Redirection)
- **Minimum SDK:** API 24 (Android 7.0 Nougat)
- **Hedef SDK:** API 34 (Android 14)

---

## 📄 Lisans

Bu proje **MIT Lisansı** ile lisanslanmıştır. Detaylar için `LICENSE` dosyasına göz atabilirsiniz.
