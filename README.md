# Ses Atlası

Türkçe, responsive ve interaktif müzik teorisi öğrenme sitesi. HTML, CSS ve tarayıcı JavaScript’i ile hazırlanmıştır. Çalışma sırasında üçüncü taraf paket, API anahtarı, harici font, veritabanı veya ücretli servis gerekmez.

## İçerik kaynağı ve kapsam

Önceki ChatGPT sohbetinin erişilebilir özeti kullanıldı: 21 bölüm, 33 alıştırma, 8 haftalık çalışma programı; nota, porte, oktav, frekans, cent, ritim, dizi, armoni ve uygulama konuları.

**Özgün `/mnt/data/Muzik_Teorisi_ve_Matematigi_Basucu_Kitabi.pdf` ve özgün hızlı başvuru dosyası bu oturuma aktarılmamıştır. Dolayısıyla içerik birebir PDF dönüşümü değildir.** Dersler ve açıklamalı sorular, doğrulanabilen kapsama göre yeniden yazılmıştır. Paketteki 27 sayfalık kitap ile tek sayfalık kart, açıkça etiketlenmiş yeni **web edisyonlarıdır**. Özgün içerikle sayfa sayfa karşılaştırma yapılamamıştır.

Site 12 eşit aralıklı akort kullanır. La4 = 440 Hz, orta Do = C4 = MIDI 60. Türk makam müziğinin koma ve seyir yapıları bu sistemin kapsamı dışındadır.

## Başlatma

Node.js 20 veya üstü gerekir. Terminali ZIP’ten çıkan `ses-atlasi` klasöründe açın:

```sh
npm run dev
```

Tarayıcıda `http://127.0.0.1:4173` adresini açın. `file://` ile HTML’yi çift tıklamak, tarayıcıların JavaScript modülü sınırlamaları nedeniyle önerilmez. Yerel çalıştırmada paket kurulumu gerekmez.

## Build ve doğrulama

```sh
npm test
npm run build
npm run check
npm run preview
```

`dist/` yayınlanacak statik çıktıdır. Build, `src/` içeriğini kopyalar ve özgün PDF’lerin bulunup bulunmadığını tespit eden manifesti oluşturur. `check` çıktı asset’lerini, PDF imzalarını, manifesti ve dil/viewport bilgilerini denetler. `tests/` frekans, oktav, cent, transpozisyon, nota yazımı, tempo ve içerik bağlantılarının 11 anlamlı test grubunu içerir.

Hazır `dist/` klasörü ZIP’e dahildir. Kaynakta bir şey değiştirirseniz yeniden build alın.

## Vercel’de yayınlama — GitHub ile

1. ZIP’i açın. `package.json` ve `vercel.json` bulunan **ses-atlasi** klasörünün içeriğini yeni bir GitHub reposuna yükleyin. Repo üstünde fazladan bir klasör varsa Vercel’de Root Directory alanını `ses-atlasi` seçin.
2. [Vercel](https://vercel.com/new) hesabınızda **Add New → Project** ile repoyu içe aktarın.
3. **Framework Preset: Other** seçin. `vercel.json` ayarları otomatik uygulanır:
   - Build Command: `npm run build`
   - Output Directory: `dist`
   - Install Command: `npm install --ignore-scripts`
4. Ortam değişkeni gerekmez. **Deploy** düğmesine basın.
5. Oluşan adresi açın. `/#/piyano` ve `/#/hesapla` sayfalarını, PDF indirmelerini ve telefondaki menüyü kontrol edin.
6. Sonraki repo güncellemeleri yeni Vercel deployment’ı başlatır.

Vercel paneline ZIP sürükleyerek yükleme adımı yoktur; Git içe aktarma veya aşağıdaki CLI yolu kullanılır.

## Vercel’de yayınlama — terminal ile

ZIP’ten çıkan proje klasöründe:

```sh
npm test
npm run build
npm run check
npx vercel
```

İlk çalıştırmada Vercel’e giriş yapın, kendi hesabınızı ve projeyi seçin. Mevcut klasörü kullanın. Framework Other, build `npm run build`, çıktı `dist` olmalıdır. Önizlemeyi kontrol ettikten sonra:

```sh
npx vercel --prod
```

Bu komut hesabınızda üretim yayını oluşturur. Bu teslim sırasında Vercel hesabınızda bir yayın yapılmadı.

Resmî belgeler: [Build ayarları](https://vercel.com/docs/builds/configure-a-build), [vercel.json](https://vercel.com/docs/project-configuration/vercel-json).

## Özellikler ve kullanım

- 21 ders; bölüm filtresi, bölüm içi gezinme ve Türkçe arama. `⌘K` / `Ctrl+K` aramayı açar.
- 25 tuşlu sesli piyano, 3.–5. başlangıç oktavı, Sol anahtarında nota ve şematik sinüs dalgası.
- Piyano kısayolları: `A W S E D F T G Y H U J K`. Ana sayfada ve ses laboratuvarında çalışır. Ses yalnızca kullanıcı etkileşimiyle başlar. İlk dokunuşta tarayıcı ses sistemini açabilir.
- Frekans transpozisyonu, oktav kaydırma, nota → frekans ve frekans → en yakın nota / cent hesabı. Sıfır, negatif, boş ve aralık dışı girdiler için açıklama.
- Majör, doğal minör, armonik minör, majör pentatonik ve kromatik diziler; nota yazımı, tuş vurguları ve sesli dinleme.
- Üçlü/yedili akor türleri, birlikte ve kırık çalma; beşliler çemberi ve göreli minörler.
- 30–240 BPM metronom; 3/4, 4/4, 6/8. **6/8’de BPM birimi noktalı dörtlüktür**; ışıklar sekizlik alt bölümleri gösterir. 3:2 poliritim örneği sabit iki saniyelik döngü kullanır.
- 33 çoktan seçmeli soru, yeniden deneme, açıklamalı cevap anahtarı ve ilgili derse bağlantı.
- Sekiz haftalık program ve PDF indirmeleri.

Sesler Web Audio API ile cihazda sentezlenir. Mikrofon kullanılmaz. Metronom sayfa değişince veya sekme arka plana geçince durur. İşletim sistemi ve cihaz gecikmesi nedeniyle stüdyo düzeyinde hassas saat olarak değerlendirilmemelidir.

## PDF’ler ve özgün dosyaları ekleme

Pakette çalışan indirmeler:

- `src/downloads/Ses_Atlasi_Web_Edisyonu.pdf` — yeni, 27 sayfalık web edisyonu.
- `src/downloads/Ses_Atlasi_Hizli_Basvuru.pdf` — yeni, tek sayfalık A4 kart.

Özgün PDF’ler elinize geçtiğinde dosyaları aşağıdaki **tam adlarla** `src/downloads/` içine koyup `npm run build` çalıştırın:

```text
Muzik_Teorisi_ve_Matematigi_Basucu_Kitabi.pdf
Muzik_Teorisi_Tek_Sayfalik_Hizli_Basvuru.pdf
```

Kütüphane ekranında ek özgün indirme bağlantıları otomatik açılır. Bu işlem web metnini değiştirmez; birebir içerik eşleştirmesi için `src/assets/content.js` dersleri özgün PDF ile ayrıca karşılaştırılmalıdır. Kaynak notu da eşleştirme tamamlandığında güncellenmelidir. Geliştirme sunucusunda da özgün bağlantıları görmek için build sonrası `npm run preview` kullanın.

## Dosya düzeni

```text
src/
  index.html
  assets/
    app.js       # Ekranlar, etkileşimler, ses ve yerel ilerleme
    content.js   # 21 ders, 33 soru, 8 hafta ve kaynaklar
    music.js     # Saf müzik matematiği fonksiyonları
    styles.css
    favicon.svg
  downloads/
scripts/
  build.mjs
  serve.mjs
  verify.mjs
tests/
  music.test.mjs
dist/            # Hazır yayın çıktısı
README.md
TEST_RAPORU.md
vercel.json
```

Dersleri/soruları `content.js`, renkleri `styles.css` içindeki `:root` değişkenlerinden değiştirebilirsiniz. Ses asset’i veya harici görsel yoktur; ikonlar ve çizimler SVG, sesler sentezdir. Tüm gerekli kaynaklar pakettedir.

## İlerleme, erişilebilirlik ve teknik sınırlar

Tamamlanan dersler ve yanıtlar `localStorage` içinde yalnızca kullanılan tarayıcıya kaydedilir. Cihazlar arasında eşitlenmez. Tarayıcı verilerini silmek ilerlemeyi siler. Depolama engelliyse uygulama oturum belleğiyle çalışır. Alıştırma sıfırlama düğmesi ders tamamlamalarını korur.

Türkçe belge dili, etiketli girişler, klavyeyle erişim, görünür odak, içerik atlama bağlantısı, arama diyaloğu, hareket azaltma tercihi ve mobil menü mevcuttur. Dar ekranda iki oktavlık piyano kendi alanında yatay kaydırılır; sayfa yatay taşmaz.

Mobil/masaüstü görünüm ve fonksiyon testlerinin kapsamı `TEST_RAPORU.md` içindedir. Bu çalışma otomatik tam WCAG uygunluk sertifikası veya bütün cihazlarda işitsel kalite testi değildir.

## Müzik matematiği kaynağı

[UNSW: Note names, MIDI numbers and frequencies](https://newt.phys.unsw.edu.au/music/notes.html). Web edisyonunun anlatımı ve soruları bu proje için yeniden yazılmıştır; özgün kitaba ait oldukları ileri sürülmez.
# ses-atlasi
