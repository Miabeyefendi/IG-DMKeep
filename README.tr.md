# 📨 InstaDM-Scraper V2: Gelişmiş Instagram DM Araç Seti | Yazar: @miabeyefendi

## Instagram DM'lerini Doğrudan Tarayıcıdan Aktarın, Yakalayın ve Çevirin — Uzantı Yok, API Yok
**InstaDM-Scraper V2**, orijinal konsol betiğinin devrimsel bir evrimidir. Artık sadece bir kod parçası değil; doğrudan Instagram DM sayfanıza enjekte edilen tam kapsamlı, **Etkileşimli bir Dashboard**'dur.

**@miabeyefendi** tarafından geliştirilen V2; **Canlı Medya Yakalama**, **Yerelleştirilmiş Çıktılar (TR/EN/ES)**, **Sesli Mesaj Transkripti** ve **Binary ZIP Çıktısı** özelliklerine sahiptir. Instagram'ın 24 saatlik veri indirme süresini beklemek yerine, aktif oturumunuzdan verileri kullanıcı dostu bir arayüzle anında çeker.

[![JavaScript](https://img.shields.io/badge/JavaScript-ES2020+-F7DF1E.svg?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Platform](https://img.shields.io/badge/Platform-Taray%C4%B1c%C4%B1_Konsolu-4285F4.svg?style=for-the-badge&logo=googlechrome&logoColor=white)](https://github.com/Miabeyefendi/InstaDM-Scraper)
[![Localization](https://img.shields.io/badge/Dil_Deste%C4%9Fi-TR%20|%20EN%20|%20ES-rebeccapurple.svg?style=for-the-badge)](https://github.com/Miabeyefendi/InstaDM-Scraper)
[![No API](https://img.shields.io/badge/API-Gerekmiyor-success.svg?style=for-the-badge)](https://github.com/Miabeyefendi/InstaDM-Scraper)

[EN | Read in English](README.md) | [ES | Leer en Español](README.es.md)

---

## 🔥 Neden V2'ye Geçmelisiniz?

V1 bir betikti; **V2 ise tam bir araç setidir.**

- 🖥️ **Etkileşimli Arayüz Paneli (Overlay UI)**  
  Artık ham konsol çıktılarıyla uğraşmanıza gerek yok. Taramayı kontrol edin, mesajları filtreleyin ve dışa aktarma seçeneklerini sayfaya eklenen modern bir panelden yönetin.

- 🌍 **Tam Yerelleştirilmiş Çıktılar**  
  Araç ve çıktı dosyaları artık seçtiğiniz dile uyum sağlar. Dil Türkçe seçilirse başlıklar `Gönderilen:`, İngilizce seçilirse `Sent:` olarak oluşturulur. Tarih formatları seçilen dile göre otomatik düzenlenir.

- 📸 **Canlı Medya Yakalama (Hook Sistemi)**  
  V2, ağ isteklerini (XHR/Fetch) ve `PerformanceObserver`'ı izleyerek; DOM'da normalde görünmeyen Reels linklerini, sesli mesajları ve yüksek çözünürlüklü görselleri canlı olarak yakalar.

- 📦 **Binary ZIP Dışa Aktarma**  
  Sadece metinleri değil, medyanın kendisini alın. V2; görselleri, sesli mesajları ve Reels videolarını (MP4) doğrudan indirmeye çalışır ve hepsini yapılandırılmış tek bir ZIP dosyası olarak paketler.

- 🎙️ **Sesten Metne (Transkript)**  
  Instagram'ın sesli mesajlar için arka planda oluşturduğu dahili transkriptleri otomatik olarak toplayan özel bir mod içerir.

---

## ✨ Temel Özellikler

- **Çoklu Format Desteği**  
  Sohbet geçmişinizi **JSON**, **TXT**, **Markdown (MD)** veya tam kapsamlı bir **ZIP** arşivi olarak indirin.

- **Derin Medya Çözümleme**  
  Paylaşılan Reels videolarının doğrudan MP4 bağlantılarını ve kapak fotoğraflarını otomatik olarak çözer.

- **Akıllı Filtreleme ve Arama**  
  Anahtar kelimelerle mesajları bulun veya zaman akışını "Sadece Görseller", "Sadece Sesler" veya "Sadece Reels" şeklinde filtreleyin.

- **Mesaj Seçim Sistemi**  
  Tüm sohbeti aktarmak yerine, sadece ihtiyacınız olan mesajları kutucuklarla seçerek dışa aktarın.

- **Gizlilik Odaklı Mimari**  
  %100 yerel olarak tarayıcınızda çalışır. Verileriniz asla bilgisayarınızdan dışarı çıkmaz. Üçüncü taraf sunucu, uzantı veya analiz aracı barındırmaz.

---

## 🛠️ Başlangıç

### Kullanım

1. Instagram DM sohbetini açın: `https://www.instagram.com/direct/t/XXXXXXXXX/`
2. DevTools'u açın (**F12** veya **Ctrl+Shift+I**) ve **Console** (Konsol) sekmesine tıklayın.
3. `instadm-scraper-v2.js` içeriğinin tamamını kopyalayıp Konsol'a yapıştırın ve **Enter**'a basın.
4. Ekranda **InstaDM Dashboard** paneli belirecektir.
5. Dilinizi seçin (TR/EN/ES) ve **"Taramayı Başlat"** butonuna tıklayın.
6. Otomatik kaydırmanın bitmesini bekleyin. İşlem tamamlandığında yan paneli kullanarak verilerinizi filtreleyebilir, arayabilir veya indirebilirsiniz.

---

## 📋 Yerelleştirilmiş Çıktı Örneği (TR vs EN)

V2, seçtiğiniz dile göre etiketlerini dinamik olarak değiştirir:

| Özellik | Türkçe Çıktı | İngilizce Çıktı |
|---|---|---|
| **Tarih Başlığı** | `Tarih: 12 May 2025` | `Date: 12 May 2025` |
| **Gönderici** | `Gönderilen:` / `Gelen:` | `Sent:` / `Received:` |
| **Medya Etiketi** | `[Görsel]`, `[Ses]` | `[Image]`, `[Audio]` |
| **Beğeni** | `-❤️ beğenildi` | `-❤️ liked` |

---

## 🔧 Teknik Bakış (V2 Yenilikleri)

| Özellik | Teknik Uygulama |
|---|---|
| **Ağ Müdahalesi** | Medya meta verilerini yakalamak için `window.fetch` ve `XMLHttpRequest`'i override eder. |
| **Blob Yönetimi** | Sesli mesaj blob'larını tanımlamak için `URL.createObjectURL` sistemine kanca (hook) atar. |
| **ZIP Oluşturma** | CRC32 sağlama toplamına sahip, bağımlılıksız özel bir ZIP oluşturucu kullanır. |
| **Reels Çözücü** | `og:video` ve `og:image` etiketlerini ayıklamak için Reels sayfalarını asenkron olarak analiz eder. |
| **Adaptif Arayüz** | Saf CSS/JS Blur-morphism (buzlu cam efekti) ile viewport değişimlerine duyarlı arayüz. |

---

## 📈 Versiyon Geçmişi

**v2.0.0 (Güncel)**
- Etkileşimli Dashboard (Arayüz) eklendi.
- Arayüz ve Çıktı için çoklu dil desteği (TR, EN, ES).
- ZIP, JSON ve Markdown formatları eklendi.
- Gerçek zamanlı medya yakalama (Ses, Reels, Görsel).
- Sesli mesaj transkript ayıklama aracı.
- Seçim, Arama ve Kategori filtreleme özellikleri.

**v1.0.0**
- İlk sürüm. Konsol tabanlı .txt dışa aktarıcı.

---

## 👨‍💻 Yazar

**Miabeyefendi**
- GitHub: [@Miabeyefendi](https://github.com/Miabeyefendi)
- Proje: **InstaDM-Scraper**

*Gizlilik için tasarlandı, sadelik için inşa edildi.*
