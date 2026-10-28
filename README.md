# Görev Takip — Android APK

Bu klasör, Görev Takip uygulamasını gerçek bir Android `.apk` dosyasına
dönüştürmek için hazır bir [Capacitor](https://capacitorjs.com) projesidir.
Uygulamanın arayüzü `www/index.html` içindedir (aynı pano — bekleyen/cevaplanan
talep listeleri, acil eşiği, kaynak ve öncelik filtreleri); native bildirim
desteği için `@capacitor/local-notifications` eklentisi zaten kurulu ve bağlı.

Bu ortamda (bu konuşmanın çalıştığı bulut korumalı alanda) Google'ın Android SDK
sunucularına ağ erişimi güvenlik politikası gereği kapalı olduğu için APK'yı burada
derleyemiyorum. Bunun yerine `.github/workflows/build-apk.yml` adında bir GitHub
Actions iş akışı hazırladım — bu, senin GitHub hesabında **ücretsiz** olarak,
Google'ın sunucularına tam erişimi olan GitHub'ın kendi sunucularında APK'yı
otomatik olarak derler.

## Kurulum adımları (yaklaşık 3 dakika)

1. [github.com/new](https://github.com/new) adresinden yeni, boş bir repo oluştur
   (Public ya da Private fark etmez, README/`.gitignore` eklemeden "Create repository"
   demen yeterli).
2. Bu klasörün tamamını (zip'i açtıktan sonra) o reponun içine gönder.

   **Terminal/git biliyorsan:**

   ```bash
   cd apk-project
   git init
   git add .
   git commit -m "Görev Takip Android projesi"
   git branch -M main
   git remote add origin https://github.com/KULLANICI_ADIN/REPO_ADIN.git
   git push -u origin main
   ```

   **Terminal kullanmak istemiyorsan:** GitHub'da reponun ana sayfasında
   "Add file → Upload files" butonuna tıkla, bilgisayarındaki `apk-project`
   klasörünün İÇİNDEKİ TÜM dosya ve klasörleri (gizli görünen `.github` klasörü
   dahil) sürükleyip bırak, sonra "Commit changes" de. `.github` klasörünü
   dosya seçme penceresinde göremiyorsan, klasörü doğrudan Finder/Explorer'dan
   tarayıcıya sürüklemeyi dene — bu genelde gizli klasörleri de taşır.

3. GitHub'da reponun **Actions** sekmesine git. "Build APK" iş akışının otomatik
   başladığını göreceksin (birkaç dakika sürer).
4. İş akışı bittiğinde, aynı sayfada "Artifacts" bölümünden
   **gorev-takip-apk** dosyasını indir — içinde `app-debug.apk` var.
5. Bu `.apk` dosyasını Android telefonuna aktarıp açman yeterli (telefonun
   "bilinmeyen kaynaklardan yükleme" iznini bir kerelik açman gerekebilir).

## Notlar

* Bu bir **debug** APK'dır — hızlıca kurup denemen için imzasızdır. Play Store'a
  yüklemek veya resmi dağıtım yapmak istersen "release" imzalama anahtarı
  oluşturup workflow'u ona göre güncellememiz gerekir; istersen bunu da
  ayarlayabilirim.
* Uygulama içindeki tüm veriler (talepler, notlar vb.) yalnızca telefonundaki
  yerel depoda saklanır, hiçbir sunucuya gönderilmez.
* Bildirimler **native Android bildirimleri** üzerinden çalışıyor: uygulama
  kapalı olsa bile, bir talep belirlediğin "acil eşiği"ni aştığı anda bildirim
  gelir. Zil simgesine basıp izin vermen yeterli.
* `www/index.html` dosyasını değiştirip tekrar `git push` yaptığında, GitHub
  Actions otomatik olarak yeni bir APK derler.
