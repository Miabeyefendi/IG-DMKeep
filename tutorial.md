```markdown
# 📘 InstaDM-Scraper V2: Technical Tutorial / Teknik Rehber / Guía Técnica

Welcome to the technical documentation for InstaDM-Scraper V2. Choose your language below to continue:
Bu teknik rehbere hoş geldiniz. Devam etmek için aşağıdan dilinizi seçin:
Bienvenido a la documentación técnica. Elija su idioma a continuación para continuar:

- [🇬🇧 English Version](#-english-version)
- [🇹🇷 Türkçe Versiyon](#-türkçe-versiyon)
- [🇪🇸 Versión en Español](#-versión-en-español)

---

<br><br>

# 🇬🇧 English Version

Welcome to the technical deep-dive for **InstaDM-Scraper V2**. This document explains how the script evolved from a simple console output to a full-fledged Dashboard, how it intercepts network requests, and how it captures hidden media (Reel MP4s, Audio files) directly from Instagram.

## 🏗️ Architecture Overview

Although V2 runs in your browser's DevTools Console, it acts like a standalone Single Page Application (SPA). Its core components are:

1. **Overlay UI:** An interactive control panel injected over the Instagram DOM.
2. **Hook System (Network Listener):** Manipulates `fetch`, `XHR`, and `PerformanceObserver` APIs to steal hidden media links.
3. **Scroll Engine:** Manages Instagram's inverted virtual scrolling.
4. **DOM Scraper & Reel Resolver:** Extracts messages, asynchronously scans Reel pages, and simulates clicks on Popups (Dialogs) to capture content.
5. **Transcript Engine:** Automates the text transcription of voice messages.
6. **ZIP & Binary Builder:** Compiles all captured media into a ZIP file in the browser memory using CRC32 checksums.

## 🔍 1. Media Capture & Hook System (The Heart of V2)

Instagram does not write audio files and high-res media directly to the DOM; it loads them in the background as Blob objects or via XHR requests. V2 bypasses this by hooking into the browser's core functions:

### Fetch and XHR Interception
As soon as the script runs, it backs up the original `window.fetch` and `XMLHttpRequest` methods and overrides them:
```javascript
state.originalFetch = window.fetch.bind(window);
window.fetch = async function (...args) {
  const response = await state.originalFetch(...args);
  // Clone the response and inspect its content
  inspectResponseBody(response.clone(), 'fetch-response'); 
  return response;
};
```
By inspecting JSON responses (`inspectJsonTree`), it catches `.mp4`, `.m4a`, or `.jpg` links and adds them to the global `state.resources` pool.

### Blob URL Interception
Voice messages are often kept in the browser as `blob:https://...`.
```javascript
URL.createObjectURL = function (value) {
  const url = state.originalCreateObjectURL(value);
  if (value instanceof Blob && value.type.includes('audio')) {
    registerResource(url, 'blob-url', { blob: value, mime: value.type });
  }
  return url;
};
```

## 🧭 2. Direction (Sender) Detection

In V1, only color analysis was used. In V2, **Bounding Box (Screen Position) Analysis** was added to counter potential CSS changes by Instagram.

```javascript
function detectIsSent(bubble, containerRect) {
  const rect = bubble.getBoundingClientRect();
  const bg = window.getComputedStyle(bubble).backgroundColor;
  
  // Rule 1: Blue shades (Sent colors)
  if (b > 160 && r < 170 && g < 170) return true;
  
  // Rule 2: Dark Theme gray color + Positioned on the right side of the screen
  if (r > 45 && g > 45 && b > 45 && rect.left > containerRect.left + containerRect.width * 0.45) return true;
  
  // Fallback Rule: If the center of the bubble is further right than 58% of the screen
  return rect.left + rect.width / 2 > containerRect.left + containerRect.width * 0.58;
}
```

## 🎙️ 3. Voice-to-Text: Transcription Engine

One of the most distinctive features of V2 is its automation of Instagram's internal voice-to-text feature.

1. It looks for buttons on the screen matching `isTranscriptTriggerText` (*"see transcript", "transkripti gör"*).
2. It clicks the button and waits up to 10 seconds.
3. It records the text in the DOM before clicking (`beforeTexts`).
4. It fetches the text after clicking, isolating the new text block that wasn't in `beforeTexts`. This block is the voice message transcript.

## 📦 4. In-Browser ZIP Engine

Traditional web scraping tools require a backend server. V2, however, converts all captured Image, Audio, and Video links into Blobs using `fetch`, and then compiles a ZIP file using pure JavaScript (no external libraries) with `Uint8Array` and `DataView`.

## 🛠️ Troubleshooting

- **ZIP Missing Some Media:** Some Instagram CDN servers enforce strict CORS policies. If a fetch request fails due to CORS, the media isn't added to the ZIP, but the link is preserved in the `links/` text documents.
- **Audio Files Not Captured:** If you opened the page and played the voice messages *before* running the script, the browser already cached them. Refresh the page, immediately paste the script, and start scanning.

---

<br><br>

# 🇹🇷 Türkçe Versiyon

**InstaDM-Scraper V2** teknik derinlemesine inceleme rehberine hoş geldiniz. Bu doküman; betiğin basit bir konsol çıktısından nasıl tam donanımlı bir Dashboard'a (Arayüz) dönüştüğünü, ağ isteklerini nasıl dinlediğini ve Instagram'ın gizli medyalarını nasıl yakaladığını açıklar.

## 🏗️ Mimari Genel Bakış

V2 versiyonu, tarayıcınızın DevTools Console'unda çalışmasına rağmen kendi başına bir mini-uygulama (SPA) gibi davranır. Temel bileşenleri şunlardır:

1. **Overlay UI (Arayüz Sistemi):** Instagram DOM'unun üzerine binen, etkileşimli kontrol paneli.
2. **Hook Sistemi (Ağ Dinleyicisi):** `fetch`, `XHR` ve `PerformanceObserver` API'lerini manipüle ederek gizli medya linklerini çalar.
3. **Scroll Motoru:** Instagram'ın ters çevrilmiş sanal kaydırmasını (virtual scroll) yönetir.
4. **DOM Scraper & Reel Resolver:** Mesajları ayıklar, Reels sayfalarını asenkron tarar ve Popup'ları otomatik tıklayıp kapatarak içerik yakalar.
5. **Transkript Motoru:** Sesli mesajların metin dökümlerini (transcript) otomatize eder.
6. **ZIP & Binary Builder:** Yakalanan tüm medyayı tarayıcı belleğinde CRC32 şifrelemesiyle ZIP dosyasına dönüştürür.

## 🔍 1. Medya Yakalama ve Hook Sistemi (V2'nin Kalbi)

Instagram, ses dosyalarını ve yüksek çözünürlüklü medyaları doğrudan DOM'a yazmaz; bunları arka planda Blob objeleri veya XHR istekleriyle yükler. V2 bunu aşmak için tarayıcının çekirdek fonksiyonlarına kanca (hook) atar:

### Fetch ve XHR Dinleme
Script çalıştığı anda orijinal `window.fetch` ve `XMLHttpRequest` metodlarını yedeğe alır ve kendi metodlarını yazar:
```javascript
state.originalFetch = window.fetch.bind(window);
window.fetch = async function (...args) {
  const response = await state.originalFetch(...args);
  // Yanıtı kopyala (clone) ve içeriğini incele
  inspectResponseBody(response.clone(), 'fetch-response'); 
  return response;
};
```
JSON yanıtları incelenerek (`inspectJsonTree`) içinde geçen `.mp4`, `.m4a` veya `.jpg` bağlantıları yakalanır ve küresel `state.resources` havuzuna eklenir.

### Blob URL Dinleme
Sesli mesajlar genellikle tarayıcıda `blob:https://...` şeklinde tutulur.
```javascript
URL.createObjectURL = function (value) {
  const url = state.originalCreateObjectURL(value);
  if (value instanceof Blob && value.type.includes('audio')) {
    registerResource(url, 'blob-url', { blob: value, mime: value.type });
  }
  return url;
};
```

## 🧭 2. Yön (Gönderici) Tespiti

V1'de sadece renk analizi yapılıyordu. V2'de Instagram'ın olası CSS değişikliklerine karşı **Ekran Pozisyonu Analizi (Bounding Box)** eklendi.

```javascript
function detectIsSent(bubble, containerRect) {
  const rect = bubble.getBoundingClientRect();
  const bg = window.getComputedStyle(bubble).backgroundColor;
  
  // Kural 1: Mavi tonları (Gönderilen renkleri)
  if (b > 160 && r < 170 && g < 170) return true;
  
  // Kural 2: Koyu Tema gri renk + Ekranın sağında olma (V2 Yeniliği)
  if (r > 45 && g > 45 && b > 45 && rect.left > containerRect.left + containerRect.width * 0.45) return true;
  
  // Fallback Kural: Balonun merkezi ekranın %58'inden daha sağdaysa
  return rect.left + rect.width / 2 > containerRect.left + containerRect.width * 0.58;
}
```

## 🎙️ 3. Sesten Metne: Transkript Çıkarma

V2'nin en ayırt edici özelliklerinden biri, sesli mesajları yazıya döken Instagram özelliğini otomatize etmesidir.

1. Ekranda `isTranscriptTriggerText` ile eşleşen (*"transkripti gör"*) butonları arar.
2. Butona tıklar ve 10 saniyeye kadar bekler.
3. Tıklama öncesi DOM'daki metinleri (`beforeTexts`) kaydeder.
4. Tıklama sonrası DOM'daki metinleri alıp, `beforeTexts` içinde olmayan yeni metin bloğunu tespit eder. Bu blok, sesli mesajın dökümüdür.

## 📦 4. Tarayıcı İçi ZIP Motoru

Geleneksel web kazıma (scraping) araçları sunucuya ihtiyaç duyar. V2 ise yakaladığı tüm Görsel, Ses ve Video bağlantılarını önce `fetch` ile Blob'a çevirir, ardından saf JavaScript ile (harici bir kütüphane kullanmadan) `Uint8Array` ve `DataView` kullanarak bir ZIP dosyası derler.

## 🛠️ Sorun Giderme

- **ZIP İndirmesinde Bazı Medyalar Eksik:** Instagram'ın bazı CDN sunucuları katı CORS politikaları uygular. Script bunu aşmak için çeşitli `fetch` modları dener. CORS'a takılırsa, medya ZIP'e eklenmez ancak `links/` klasöründeki metin belgelerinde link olarak saklanır.
- **Ses Dosyaları Yakalanamıyor:** Eğer sayfayı açıp tüm sesli mesajları kodu çalıştırmadan *önce* dinlediyseniz, tarayıcı bunları çoktan önbelleğe almıştır. Sayfayı yenileyin, sohbet yüklenmeden **hemen** kodu konsola yapıştırıp taramayı başlatın.

---

<br><br>

# 🇪🇸 Versión en Español

Bienvenido al análisis técnico profundo de **InstaDM-Scraper V2**. Este documento explica cómo el script evolucionó de una simple salida de consola a un Dashboard completo, cómo intercepta las solicitudes de red y cómo captura medios ocultos (MP4 de Reels, archivos de audio) directamente desde Instagram.

## 🏗️ Resumen de la Arquitectura

Aunque la V2 se ejecuta en la Consola DevTools de su navegador, actúa como una Aplicación de Página Única (SPA) independiente. Sus componentes principales son:

1. **Overlay UI:** Un panel de control interactivo inyectado sobre el DOM de Instagram.
2. **Sistema de Hooks (Oyente de Red):** Manipula las API `fetch`, `XHR` y `PerformanceObserver` para robar enlaces multimedia ocultos.
3. **Motor de Desplazamiento (Scroll):** Gestiona el desplazamiento virtual invertido de Instagram.
4. **Scraper del DOM y Resolutor de Reels:** Extrae mensajes, escanea asincrónicamente páginas de Reels y simula clics en ventanas emergentes (Diálogos) para capturar contenido.
5. **Motor de Transcripción:** Automatiza la transcripción de texto de los mensajes de voz.
6. **Constructor ZIP y Binario:** Compila todos los medios capturados en un archivo ZIP en la memoria del navegador utilizando sumas de comprobación CRC32.

## 🔍 1. Captura de Medios y Sistema de Hooks (El Corazón de la V2)

Instagram no escribe archivos de audio ni medios de alta resolución directamente en el DOM; los carga en segundo plano como objetos Blob o mediante solicitudes XHR. V2 elude esto enganchándose a las funciones principales del navegador:

### Intercepción de Fetch y XHR
Tan pronto como se ejecuta el script, realiza una copia de seguridad de los métodos originales `window.fetch` y `XMLHttpRequest` y los sobrescribe:
```javascript
state.originalFetch = window.fetch.bind(window);
window.fetch = async function (...args) {
  const response = await state.originalFetch(...args);
  // Clona la respuesta e inspecciona su contenido
  inspectResponseBody(response.clone(), 'fetch-response'); 
  return response;
};
```
Al inspeccionar las respuestas JSON (`inspectJsonTree`), captura los enlaces `.mp4`, `.m4a` o `.jpg` y los agrega al grupo global `state.resources`.

### Intercepción de URL de Blob
Los mensajes de voz a menudo se mantienen en el navegador como `blob:https://...`.
```javascript
URL.createObjectURL = function (value) {
  const url = state.originalCreateObjectURL(value);
  if (value instanceof Blob && value.type.includes('audio')) {
    registerResource(url, 'blob-url', { blob: value, mime: value.type });
  }
  return url;
};
```

## 🧭 2. Detección de Dirección (Remitente)

En la V1, solo se usaba análisis de color. En la V2, se agregó el **Análisis de Cuadro Delimitador (Posición en Pantalla)** para contrarrestar posibles cambios de CSS por parte de Instagram.

```javascript
function detectIsSent(bubble, containerRect) {
  const rect = bubble.getBoundingClientRect();
  const bg = window.getComputedStyle(bubble).backgroundColor;
  
  // Regla 1: Tonos azules (Colores de mensajes enviados)
  if (b > 160 && r < 170 && g < 170) return true;
  
  // Regla 2: Color gris del tema oscuro + Posicionado en el lado derecho de la pantalla
  if (r > 45 && g > 45 && b > 45 && rect.left > containerRect.left + containerRect.width * 0.45) return true;
  
  // Regla de respaldo: Si el centro de la burbuja está más a la derecha que el 58% de la pantalla
  return rect.left + rect.width / 2 > containerRect.left + containerRect.width * 0.58;
}
```

## 🎙️ 3. Voz a Texto: Motor de Transcripción

Una de las características más distintivas de la V2 es la automatización de la función interna de voz a texto de Instagram.

1. Busca botones en la pantalla que coincidan con `isTranscriptTriggerText` (*"ver transcripcion"*).
2. Hace clic en el botón y espera hasta 10 segundos.
3. Registra el texto en el DOM antes de hacer clic (`beforeTexts`).
4. Obtiene el texto después de hacer clic, aislando el nuevo bloque de texto que no estaba en `beforeTexts`. Este bloque es la transcripción del mensaje de voz.

## 📦 4. Motor ZIP en el Navegador

Las herramientas tradicionales de web scraping requieren un servidor backend. Sin embargo, V2 convierte todos los enlaces de imágenes, audio y video capturados en Blobs usando `fetch`, y luego compila un archivo ZIP usando JavaScript puro (sin bibliotecas externas) con `Uint8Array` y `DataView`.

## 🛠️ Solución de Problemas

- **Faltan Algunos Medios en el ZIP:** Algunos servidores CDN de Instagram aplican políticas estrictas de CORS. Si una solicitud fetch falla debido a CORS, el medio no se agrega al ZIP, pero el enlace se conserva en los documentos de texto en la carpeta `links/`.
- **Archivos de Audio no Capturados:** Si abrió la página y reprodujo los mensajes de voz *antes* de ejecutar el script, el navegador ya los almacenó en caché. Actualice la página, pegue el script inmediatamente e inicie el escaneo.
```
