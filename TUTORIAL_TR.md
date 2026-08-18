<div align="center">

# 📖 IG-DMKeep Rehberi

**v2.0.0 · Son güncelleme 2026-08-18**

[English](./TUTORIAL.md) · **Türkçe** · [Español](./TUTORIAL_ES.md) · [简体中文](./TUTORIAL_ZH.md) · [Русский](./TUTORIAL_RU.md)

[README'ye dön](./README_TR.md) · [Değişiklikler](./CHANGELOG.md)

</div>

---

Bu belge IG-DMKeep'in arka planda nasıl çalıştığını anlatır. Sadece çalıştırmak istiyorsan [README](./README_TR.md) daha kısa.

## 📑 İçindekiler

- [Genel bakış](#-genel-bakış)
- [Kurulum](#-kurulum)
- [Arayüz turu](#️-arayüz-turu)
- [Özellik referansı](#-özellik-referansı)
- [Yapılandırma referansı](#️-yapılandırma-referansı)
- [Sorun giderme](#-sorun-giderme)
- [Sık sorulanlar](#-sık-sorulanlar)
- [Sözlük](#-sözlük)

---

## 🔭 Genel bakış

### Ne yapar

Instagram sana bir veri indirme seçeneği sunuyor, ama gelen arşiv okumak için değil mevzuata uymak için hazırlanmış. IG-DMKeep tersini yapıyor: baktığın konuşmayı, zaten giriş yapmış olduğun tarayıcıda okuyor ve gerçekten kullanabileceğin bir biçimde yazıyor.

### Nasıl çalışır

```
  Sayfada acik DM sohbeti
        |
        |  kaydirma surucusu sohbette geriye yuruyor
        v
  DOM ayristirici  -------------> mesaj kayitlari
        |                          metin, zaman damgasi, gonderici, tepkiler
        |
  ag kancalari (fetch / XHR / PerformanceObserver)
        |                          DOM'un hic gostermedigi dogrudan medya URL'leri
        v
  mesaj kimligine gore birlestirme
        |
        +--> JSON        yapili, islemek icin
        +--> TXT         duz, okumak icin
        +--> Markdown    yayimlamak icin
        +--> ZIP         metin artik indirilen medya dosyalari
```

Önemli olan ikinci girdi. Instagram bir reels'in veya sesli notun kullanılabilir bağlantısını DOM'a koymuyor, dolayısıyla sadece sayfayı ayrıştırırsan elinde "burada bir video vardı" diyen bir mesaj kalıyor. Kancalar, sayfanın kendi ürettiği trafiği izliyor ve geçen URL'leri saklıyor.

### Dosya düzeni

| Yol | Nedir |
|---|---|
| `instadm-scraper-v2.js` | Güncel araç, 3700 satır, burada anlatılan her şey |
| `instadm-scraper.js` | İlk sürüm, 342 satır, konsol çıktısı ve metin dışa aktarma |

---

## 📦 Kurulum

### Gereksinimler

- Masaüstü tarayıcı. Mobil site konuşmayı aynı şekilde işlemiyor, desteklenmiyor.
- `www.instagram.com` adresinde giriş yapmış kendi hesabın.
- Başka bir şey yok. Eklenti yok, derleme yok, API anahtarı yok.

### Adım adım

1. `www.instagram.com` adresini aç ve giriş yap.
2. Kaydetmek istediğin DM sohbetini aç. **Gelen kutusu listesi değil, sohbetin kendisi.** Script işlenmiş olanı okuyor, gelen kutusunda okunacak bir konuşma yok.
3. Mesajlar görünene kadar bekle.
4. Konsolu aç: `F12`, Chrome ve Edge'de `Ctrl + Shift + J`, Firefox'ta `Ctrl + Shift + K`, Mac'te `Cmd + Option + J`.
5. `instadm-scraper-v2.js` dosyasının tamamını yapıştır ve Enter'a bas.

Bazı tarayıcılar sen bir kez `allow pasting` yazana kadar konsola yapıştırılan kodu engelliyor. Bu tarayıcının güvenlik önlemi, bu scriptin hatası değil.

### Çalıştığını doğrulama

Panel sayfanın üstünde belirir. Bunun yerine `Conversation container not found` görüyorsan 2. adım gerçekleşmemiş demektir: sohbetin içine gir ve tekrar dene.

### Kaldırma

Sayfayı yenile. Hiçbir şey kurulmuyor ve hiçbir şey kalıcı olmuyor.

---

## 🖥️ Arayüz turu

Panel sayfaya enjekte edilir ve üstünde yüzer. Alttaki düzene dokunulmaz, panel açıkken Instagram çalışmaya devam eder.

| Bölge | Ne var |
|---|---|
| Scan | Başlat, ilerleme ve anlık mesaj sayacı |
| Filter | Anahtar kelime kutusu, görsel/ses/reels tür filtreleri |
| Timeline | Toplanan mesajlar, her birinde bir onay kutusu |
| Export | Biçim seçici, dil seçici, medya ve transkript anahtarları |

---

## 🧩 Özellik referansı

### Medya yakalama ve kanca sistemi

**Ne yapar.** Reels, sesli mesaj ve tam çözünürlüklü görsellerin doğrudan URL'lerini çıkarır.

**Nasıl çalışır.** Tarama başlamadan önce `fetch` ve `XMLHttpRequest` sarmalanır, böylece sayfanın yaptığı her istek önce araçtan geçer. Paralel olarak bir `PerformanceObserver` kaynak zamanlama kayıtlarını izler; bu, sarmalayıcıların göremediği yollardan yüklenen medyayı yakalar. Blob URL'leri de dinlenir, çünkü Instagram bazı medyayı blob olarak sunuyor ve sayfa ilerledikten sonra bunlara erişilemiyor. Medyaya benzeyen ne varsa mesaj bazlı bir tabloda tutulur.

**Sınırları.** Bir kanca yalnızca araç çalışırken gerçekleşen trafiği görür. Sen scripti yapıştırmadan önce yüklenmiş medya çoktan gelip geçmiştir; taramanın ekrandakini okumak yerine sohbette yürümesinin bir sebebi de bu.

### Gönderici tespiti

**Ne yapar.** Her mesaj için, onu senin mi karşı tarafın mı gönderdiğine karar verir.

**Nasıl çalışır.** Instagram bunu kendi yeniden tasarımlarından sağ çıkacak biçimde etiketlemiyor, bu yüzden yön; birkaç ayda bir değişen bir class adından değil, yerleşimden ve yapısal konumdan çıkarılıyor. Mesajlar seri halinde gruplanıyor, çünkü aynı kişiden gelen ardışık mesaj bloğu aynı yönü paylaşır.

**Sınırları.** Birden fazla katılımcılı grup sohbetleri, birebir konuşmalara göre daha zor; alışılmadık mesaj türleri yanlış atfedilebilir.

### Sesli mesaj transkripti

**Ne yapar.** Sesli notları dışa aktarmada aranabilir metne çevirir.

**Nasıl çalışır.** Konuşma tanıma çalıştırmıyor. Instagram sesli mesajlar için zaten transkript üretiyor; bu mod onları isteyip topluyor ve her birini kendi mesajına ekliyor.

**Sınırları.** Instagram'ın bir not için transkripti yoksa toplanacak bir şey de yok. Doğruluk bu aracın değil Instagram'ın.

### ZIP dışa aktarma

**Ne yapar.** Konuşma metnini gerçek medya dosyalarıyla birlikte tek bir arşive paketler.

**Nasıl çalışır.** Arşiv tarayıcı içinde kurulur. Yakalanan her medya URL'si çekilir, bellekte tutulur ve metin çıktısıyla birlikte yapılandırılmış bir ZIP'e yazılır.

**Sınırları.** Bu yavaş yol, çünkü her dosyayı indiriyor. Çok sayıda reels içeren uzun sohbetler zaman ve gerçek bant genişliği harcar. Çok büyük konuşmalar tarayıcı bellek sınırlarına takılabilir; öyle olursa bölümler halinde dışa aktar.

---

## ⚙️ Yapılandırma referansı

### Export

| Seçenek | Değerler | Etkisi |
|---|---|---|
| Format | JSON, TXT, Markdown, ZIP | Çıktı biçimi. Medya dosyalarını içeren tek seçenek ZIP. |
| Selection | Tümü, veya işaretlenen mesajlar | Her şeyi ya da yalnızca seçtiğini aktar |
| Language | İngilizce, Türkçe, İspanyolca | Dosyaya yazılan başlıkların dili |

### Filter

| Seçenek | Etkisi |
|---|---|
| Keyword | Yalnızca metni içeren mesajları göster |
| Type | Yalnızca görsel, yalnızca ses veya yalnızca reels |

### Media

| Seçenek | Etkisi |
|---|---|
| Download media | Gerçek dosyaları çek ve ZIP'e dahil et |
| Transcription | Sesli mesajlar için Instagram transkriptlerini topla |

### Hiçbir şeyin saklandığı yer

Hiçbir yer. Tarayıcının kaydettiği dışa aktarma dosyası dışında hiçbir şey yazılmaz ve çalıştırmalar arasında hiçbir şey tutulmaz. Sayfayı yenilemek her şeyi bitirir.

---

## 🔧 Sorun giderme

### "Conversation container not found. Open a DM thread first."

**Sebep.** Script işlenmiş bir konuşma bulamadı. Giriş yapmış olmak ya da gelen kutusu listesinde durmak yetmiyor.
**Çözüm.** Sohbetin içine tıkla, mesajlar görünene kadar bekle, sonra yapıştır. Sohbet açıkken de hata sürüyorsa Instagram işaretlemesini değiştirmiştir; tarayıcı ve sürümünle bir issue aç.

### Dışa aktarmada eski mesajlar eksik

**Sebep.** Instagram sen kaydırdıkça mesajları sayfadan atıyor, okunacak şekilde DOM'da değiller.
**Çözüm.** Taramanın bitmesini bekle. Sohbette bilerek geriye yürüyor. Uzun konuşmalar zaman alır.

### Medya eksik, veya ZIP beklenenden az dosya içeriyor

**Sebep.** Medya kancalar kurulmadan önce yüklenmiş, ya da URL'si indirme çalışmadan önce süresi dolmuş.
**Çözüm.** Sayfayı yenile, önce scripti yapıştır, ancak ondan sonra tara. Başlamadan önce sohbette elle gezinme.

### Tarayıcı yapıştırılan scripti kabul etmiyor

**Sebep.** Yapıştırma yoluyla yapılan sosyal mühendisliğe karşı bir tarayıcı önlemi.
**Çözüm.** Konsola bir kez `allow pasting` yaz, sonra yapıştır.

### Sekme donuyor veya bellek yetmiyor

**Sebep.** ZIP için bellekte tutulan çok medyalı, çok uzun bir sohbet.
**Çözüm.** Bunun yerine TXT veya JSON olarak aktar, ya da mesaj seçimini kullanarak bölümler halinde aktar.

### Hata bildirimi için log toplama

Konsol çıktısını kopyala. **Paylaşmadan önce seni veya karşı tarafı tanımlayan her şeyi çıkar:** kullanıcı adları, mesaj metni, oturum çerezleri ve token içeren her URL. Issue halka açık ve kalıcıdır.

---

## ❓ Sık sorulanlar

**Makinemden bir şey çıkıyor mu?**
Yalnızca Instagram'ın zaten yapacağı istekler. Bu projeye ait bir sunucu yok, analitik yok.

**Parçası olmadığım konuşmaları okuyabilir mi?**
Hayır. Yalnızca senin giriş yapmış oturumunun zaten gösterebildiğini görebilir.

**v1 dosyası neden hâlâ duruyor?**
Çünkü 342 satır tek oturuşta okunup gözle doğrulanabilir. Bazı insanlar büyük bir scripte güvenmektense küçük olanı denetlemeyi tercih eder.

**Mobil sitede çalışır mı?**
Hayır. Konuşma farklı işleniyor ve seçiciler geçerli olmuyor.

---

## 📕 Sözlük

| Terim | Anlamı |
|---|---|
| Kanca (hook) | `fetch` veya `XHR` etrafına sarılan, sayfanın isteklerini araca gösteren sarmalayıcı |
| PerformanceObserver | Yüklenen kaynakları bildiren tarayıcı API'si, kancaların kaçırdığı medyayı yakalamak için |
| Blob URL | Bellekte geçici URL, Instagram bazı medyayı böyle sunuyor |
| Sanal kaydırma | Bellek için ekran dışı öğeleri sayfadan atmak, taramanın sohbette yürümesinin sebebi |
| Yön | Bir mesajın senin tarafından mı gönderildiği yoksa alındığı mı |

---

<div align="center">
<img src="./assets/divider.svg" width="100%" height="3" alt="">
<br/>
<sub><b><a href="https://github.com/Miabeyefendi">Miabeyefendi</a></b> tarafından yapıldı · <a href="./README_TR.md">README'ye dön</a></sub>
</div>
