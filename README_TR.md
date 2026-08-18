<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/logo-dark.svg">
  <img src="./assets/logo.svg" width="120" alt="IG-DMKeep">
</picture>

# IG-DMKeep

**Kendi Instagram konuşmalarını kaybetmeden önce kaydet. Zaman damgaları, gönderici bilgisi, tepkiler ve medyayla birlikte tüm geçmiş; JSON, TXT, Markdown veya ZIP olarak. Her şey senin tarayıcında olup biter.**

[![Lisans: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-A78BFA?style=for-the-badge&logo=gnu&logoColor=white)](./LICENSE)
[![Sürüm](https://img.shields.io/github/v/release/Miabeyefendi/IG-DMKeep?style=for-the-badge&color=F59E0B&label=version)](https://github.com/Miabeyefendi/IG-DMKeep/releases/latest)
[![Platform](https://img.shields.io/badge/Browser_Console-1E293B?style=for-the-badge&logo=googlechrome&logoColor=white)](#-kurulum)
[![Durum](https://img.shields.io/badge/status-active-22C55E?style=for-the-badge)](#)
[![Yazar](https://img.shields.io/badge/by-Miabeyefendi-0EA5E9?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Miabeyefendi)

[English](./README.md) · **Türkçe** · [Español](./README_ES.md) · [简体中文](./README_ZH.md) · [Русский](./README_RU.md)

[Kurulum](#-kurulum) · [Özellikler](#-öne-çıkanlar) · [Kullanım](#-hızlı-başlangıç) · [Rehber](./TUTORIAL_TR.md) · [Değişiklikler](./CHANGELOG.md)

<a href="https://github.com/Miabeyefendi/IG-DMKeep/releases/latest">
  <img src="./assets/btn-download.svg" height="52" alt="En son sürümü indir">
</a>
<a href="./TUTORIAL_TR.md">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-tutorial-dark.svg">
    <img src="./assets/btn-tutorial.svg" height="52" alt="Rehberi oku">
  </picture>
</a>

</div>

---

## ✨ Öne çıkanlar

- **Verin sende kalır** - her şey tarayıcında yerel olarak çalışır. Sunucu yok, eklenti yok, API anahtarı yok, analitik yok. Konuşmalarına dair hiçbir şey makineni terk etmez.
- **Konsol çıktısı duvarı değil, bir arayüz** - sayfaya bir panel enjekte edilir; taramayı oradan yönetir, zaman çizelgesini filtreler, neyi dışa aktaracağını orada seçersin.
- **Dört dışa aktarma biçimi** - işlemek için JSON, okumak için TXT, yayımlamak için Markdown, ya da medyayı metinle birlikte paketleyen ZIP.
- **Sayfanın sana göstermediği medya** - araç ağ trafiğini ve `PerformanceObserver`'ı izleyerek reels, sesli mesaj ve tam çözünürlüklü görsellerin DOM'da hiç görünmeyen doğrudan bağlantılarını çıkarır.
- **Sesli mesajlar metin olarak** - özel bir mod, Instagram'ın kendi transkriptlerini toplar, böylece dışa aktarma aranabilir olur.
- **Dışa aktarmadan önce filtrele ve ara** - anahtar kelimeyle mesaj bul, veya zaman çizelgesini yalnızca görsel, ses ya da reels'e daralt.
- **Hepsini değil, seçtiğini aktar** - gerçekten istediğin mesajları işaretle.
- **Çıktı senin dilinde** - dışa aktarma başlıkları dil seçimini izler; Türkçe bir çıktı `Sent:` değil `Gönderilen:` yazar.
- **Sanal kaydırmayla başa çıkar** - Instagram sen kaydırdıkça mesajları bellekten atar; tarama bununla savaşmak yerine buna göre kurulmuştur.

---

## 📦 Kurulum

### Gereksinimler

| | |
|---|---|
| Tarayıcı | Masaüstünde Chrome, Edge veya Firefox |
| Hesap | Kendi Instagram hesabın, açık bir DM sohbetiyle |
| Kurulum | Yok. Bu bir konsol scripti. |

![JavaScript](https://img.shields.io/badge/JavaScript-1E293B?style=for-the-badge&logo=javascript&logoColor=A78BFA)
![Instagram](https://img.shields.io/badge/Instagram-1E293B?style=for-the-badge&logo=instagram&logoColor=A78BFA)

### Bir sürüm seç

| Sürüm | Dosya | Nedir |
|---|---|---|
| **v2** | [`instadm-scraper-v2.js`](./instadm-scraper-v2.js) | Güncel olan. Arayüz, medya yakalama, ZIP, transkript. |
| **v1** | [`instadm-scraper.js`](./instadm-scraper.js) | İlk sürüm. Sadece konsol çıktısı, metin dışa aktarma, 342 satır. Baştan sona okuyabileceği küçük bir şey isteyenler için duruyor. |

<details>
<summary><b>Klonlamayı mı tercih edersin?</b></summary>

```bash
git clone https://github.com/Miabeyefendi/IG-DMKeep.git
```

Derleme adımı yok, bağımlılık yok.

</details>

---

## 🚀 Hızlı başlangıç

1. Masaüstünde [www.instagram.com](https://www.instagram.com/) adresine git ve giriş yap.
2. **Kaydetmek istediğin DM sohbetini aç.** Script ekranda açık olan konuşmayı okur, yani bu adım isteğe bağlı değil.
3. Konsolu aç. Chrome ve Edge'de `F12` veya `Ctrl + Shift + J`, Firefox'ta `Ctrl + Shift + K`. Mac'te `Cmd + Option + J`.
4. [`instadm-scraper-v2.js`](./instadm-scraper-v2.js) dosyasının tamamını yapıştır ve Enter'a bas.
5. Arayüz belirir. Taramayı başlat, sohbette geriye doğru yürümesini bekle, sonra bir dışa aktarma biçimi seç.

> **"Conversation container not found" hatası alıyorsan bir sohbetin içinde değilsin.** Gelen kutusunu açmak yetmez. Önce sohbetin kendisine tıkla, mesajlar görünene kadar bekle, sonra scripti yapıştır.

---

## ⚙️ Yapılandırma

Her şey arayüzden ayarlanır, dosyada hiçbir şey düzenlenmez.

| Grup | Seçenek | Ne yapar |
|---|---|---|
| Export | Format | JSON, TXT, Markdown veya ZIP |
| Export | Selection | Tüm konuşma, veya yalnızca işaretlediğin mesajlar |
| Export | Language | Dışa aktarma dosyasına yazılan başlıkların dili |
| Filter | Keyword | Yalnızca belirli bir kelime veya ifadeyi içeren mesajlar |
| Filter | Type | Yalnızca görsel, yalnızca ses, veya yalnızca reels |
| Media | Download media | Gerçek dosyaları indir ve ZIP içine paketle |
| Media | Transcription | Sesli mesajlar için Instagram transkriptlerini topla |

Bunların arka planda nasıl çalıştığı ve biri aksadığında ne yapılacağı [rehberde](./TUTORIAL_TR.md).

---

## 📖 Belgeler

- [**Rehber**](./TUTORIAL_TR.md) - yakalama, gönderici tespiti, transkript ve ZIP motorlarının gerçekte nasıl çalıştığı
- [**Değişiklikler**](./CHANGELOG.md) - her sürümde ne değişti
- [**Katkıda bulunma**](./CONTRIBUTING.md) - nasıl değişiklik gönderilir
- [**Güvenlik**](./SECURITY.md) - zafiyet nasıl özel olarak bildirilir

---

## ❓ Sık sorulanlar

<details>
<summary><b>"Conversation container not found. Open a DM thread first."</b></summary>

Script sayfada işlenmiş bir konuşma bulamadı. Giriş yapmış olmak veya gelen kutusu listesinde durmak yetmiyor. İlgili sohbeti aç, mesajlar görünene kadar bekle, ancak ondan sonra scripti yapıştır. Sohbet açıkken de bu hatayı alıyorsan Instagram işaretlemesini değiştirmiş demektir; tarayıcı sürümünle birlikte bir issue aç.

</details>

<details>
<summary><b>Mesajlarımı bir yere gönderiyor mu?</b></summary>

Hayır. Her şey zaten açık olan sayfanın içinde çalışır ve dışa aktarma dosyasını senin tarayıcın senin diskine yazar. Sunucu yok, eklenti yok, analitik yok. Bunun bir konsol scripti olmasının tüm sebebi bu.

</details>

<details>
<summary><b>Başkasının DM'lerini dışa aktarabilir miyim?</b></summary>

Hayır. Script yalnızca senin giriş yapmış oturumunun zaten gösterebildiği şeyi okuyabilir. Bu, kendi konuşmalarının bir kopyasını saklamanın yolu, fazlası değil.

</details>

<details>
<summary><b>ZIP neden bu kadar uzun sürüyor?</b></summary>

Çünkü gerçek medya dosyalarını tek tek indirip tarayıcı içinde paketliyor. Çok sayıda reels ve sesli not içeren uzun bir sohbet epey trafik demek. Yalnızca metin dışa aktarması neredeyse anında biter.

</details>

<details>
<summary><b>Bazı eski mesajlar eksik.</b></summary>

Instagram sen kaydırdıkça mesajları bellekten atıyor, bu yüzden taramanın onları sayfaya geri getirmek için sohbette geriye yürümesi gerekiyor. Bitmesini bekle. Çok uzun konuşmalarda bu zaman alır.

</details>

<details>
<summary><b>v1 mi v2 mi kullanmalıyım?</b></summary>

v2, tek oturuşta okuyabileceğin kadar küçük bir şey istemiyorsan. v1 342 satır ve düz metin veriyor; v2 aracın tamamı.

</details>

---

## 🤝 Katkıda bulunma

Katkılar memnuniyetle karşılanır. Önce [CONTRIBUTING.md](./CONTRIBUTING.md) ve [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) dosyalarını oku. Katkıda bulunarak eserini AGPL-3.0 altında lisanslamayı kabul edersin.

<div align="center">
<a href="https://github.com/Miabeyefendi/IG-DMKeep/issues/new?template=bug_report.yml">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-report-bug-dark.svg">
    <img src="./assets/btn-report-bug.svg" height="52" alt="Hata bildir">
  </picture>
</a>
<a href="https://github.com/Miabeyefendi/IG-DMKeep/stargazers">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-star-dark.svg">
    <img src="./assets/btn-star.svg" height="52" alt="Bu depoya yıldız ver">
  </picture>
</a>
</div>

---

## 🛡️ Güvenlik

Bir zafiyet mi buldun? Halka açık issue açma. [SECURITY.md](./SECURITY.md) dosyasındaki özel süreci izle.

---

## 📜 Lisans

IG-DMKeep; [NOTICE](./NOTICE) dosyasındaki ek şartlarla birlikte **GNU Affero General Public License v3.0 (AGPL-3.0)** altında lisanslanmıştır. Kısaca:

- Eksiksiz kaynak kodu AGPL-3.0 altında erişilebilir tuttuğun sürece (barındırılan, SaaS veya ağ kullanımı dahil, AGPL Bölüm 13) ve aşağıdaki yazar atfını koruduğun sürece bu eseri **ücretsiz** kullanabilir, inceleyebilir, değiştirebilir, dağıtabilir ve hatta para kazanabilirsin.
- Bu eseri kapalı kaynaklı veya tescilli bir üründe kullanmak ya da kapalı bir SaaS olarak çalıştırmak için **ayrı, yazılı bir ticari lisans** gerekir; royalti veya gelir payı içerebilir. Bkz. [NOTICE](./NOTICE), Bölüm 8; benimle iletişime geç.

### Atıf (zorunlu)

AGPL-3.0 Bölüm 7(b) uyarınca aşağıdaki atıf; bu projenin her kopyasında, fork'unda veya dağıtımında görünür ve değiştirilmeden korunmalıdır:

> **Miabeyefendi (Mustafa İhsan Albayrak)** - https://github.com/Miabeyefendi

### Sorumluluk reddi

Bu yazılım, hiçbir garanti olmaksızın "olduğu gibi" sunulur. Tamamen kendi riskinle çalıştırırsın ve kendi kullanımından, etkileştiği herhangi bir üçüncü taraf platformun (özellikle Instagram) kullanım koşullarına uymak dahil, yalnızca sen sorumlusun. Instagram bu projeyle bağlı veya onu onaylamış değildir; adı ve ticari markaları sahibine aittir. Yazar; hesap yasakları, veri kaybı veya başka herhangi bir zarardan, uygulanabilir yasanın izin verdiği azami ölçüde sorumlu değildir. Tam şartlar [LICENSE](./LICENSE) ve [NOTICE](./NOTICE) dosyalarındadır.

---

## 📬 İletişim

- GitHub: [@Miabeyefendi](https://github.com/Miabeyefendi)
- Ticari lisanslama veya gelir paylaşımı için GitHub profilim üzerinden bana ulaş.

<div align="center">
<br/>
<img src="./assets/divider.svg" width="100%" height="3" alt="">
<br/>
<sub><b><a href="https://github.com/Miabeyefendi">Miabeyefendi</a></b> tarafından yapıldı</sub>
</div>
