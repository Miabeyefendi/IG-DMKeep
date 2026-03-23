# 📨 InstaDM-Scraper V2: Herramienta definitiva para Instagram DM | Por: @miabeyefendi

## Exporta, captura y transcribe DMs de Instagram directamente desde tu navegador — Sin API, Sin extensiones
**InstaDM-Scraper V2** es una evolución masiva del script original. Ha pasado de ser un simple script de consola a un **Dashboard Interactivo** completo que se inyecta directamente en tu página de mensajes directos de Instagram.

Desarrollada por **@miabeyefendi**, la V2 ahora cuenta con **Captura de medios en vivo**, **Salidas localizadas (ES/EN/TR)**, **Transcripción de mensajes de voz** y **Exportación binaria en ZIP**. Evita la espera de 24 horas para la descarga de datos de Instagram extrayendo la información al instante con una interfaz de usuario amigable.

[![JavaScript](https://img.shields.io/badge/JavaScript-ES2020+-F7DF1E.svg?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Platform](https://img.shields.io/badge/Platform-Consola_del_Navegador-4285F4.svg?style=for-the-badge&logo=googlechrome&logoColor=white)](https://github.com/Miabeyefendi/InstaDM-Scraper)
[![Localization](https://img.shields.io/badge/Idiomas-ES%20|%20EN%20|%20TR-rebeccapurple.svg?style=for-the-badge)](https://github.com/Miabeyefendi/InstaDM-Scraper)
[![No API](https://img.shields.io/badge/API-No_Requerida-success.svg?style=for-the-badge)](https://github.com/Miabeyefendi/InstaDM-Scraper)

[EN | Read in English](README.md) | [TR | Türkçe Oku](README.tr.md)

---

## 🔥 ¿Por qué actualizar a la V2?

La V1 era un script; **la V2 es un kit de herramientas profesional.**

- 🖥️ **Panel de control interactivo (Overlay UI)**  
  Ya no necesitas mirar la consola. Controla el escaneo, filtra mensajes y elige opciones de exportación desde un dashboard moderno integrado en la página.

- 🌍 **Exportaciones totalmente localizadas**  
  La herramienta y los archivos de salida ahora respetan tu elección de idioma. Si seleccionas español, los encabezados serán `Enviado:`, si es inglés `Sent:`, y si es turco `Gönderilen:`.

- 📸 **Captura de medios en vivo (Hooks)**  
  V2 intercepta solicitudes de red (XHR/Fetch) y monitorea el `PerformanceObserver` para capturar enlaces directos de Reels, mensajes de voz e imágenes de alta resolución que normalmente no son visibles en el DOM.

- 📦 **Exportación binaria en ZIP**  
  No solo exportes texto. V2 puede intentar descargar los archivos multimedia físicos (imágenes, audios, MP4 de Reels) y empaquetarlos en un único archivo ZIP estructurado.

- 🎙️ **Voz a texto (Transcripción)**  
  Un modo especializado que automatiza la recopilación de las transcripciones internas de Instagram para los mensajes de voz.

---

## ✨ Características principales

- **Exportación multiformato**  
  Descarga tu historial de chat como **JSON**, **TXT**, **Markdown (MD)** o un archivo **ZIP** completo.

- **Descubrimiento profundo de medios**  
  Resuelve automáticamente los metadatos de los Reels para encontrar URLs directas de video MP4 y miniaturas.

- **Filtrado y búsqueda inteligente**  
  Encuentra mensajes al instante usando palabras clave o filtra el historial por "Solo imágenes", "Solo audio" o "Solo Reels".

- **Selección de mensajes**  
  Exporta toda la conversación o usa las casillas de verificación para seleccionar solo los mensajes específicos que necesitas.

- **Privacidad garantizada**  
  Funciona 100% localmente en tu navegador. Tus datos nunca salen de tu computadora. Sin servidores de terceros, sin extensiones y sin analíticas.

---

## 🛠️ Cómo empezar

### Uso

1. Abre una conversación de DM en Instagram: `https://www.instagram.com/direct/t/XXXXXXXXX/`
2. Abre las herramientas de desarrollador (**F12** o **Ctrl+Shift+I**) y haz clic en la pestaña **Console** (Consola).
3. Pega todo el contenido de `instadm-scraper-v2.js` y presiona **Enter**.
4. El **InstaDM Dashboard** aparecerá en tu pantalla.
5. Selecciona tu idioma (ES/EN/TR) y haz clic en **"Iniciar escaneo"** (Start Scan).
6. Espera a que el auto-scroller termine. Una vez finalizado, usa la barra lateral para filtrar, buscar o descargar tus datos.

---

## 📋 Ejemplo de salida localizada (ES vs EN)

V2 adapta sus etiquetas según el idioma seleccionado en la interfaz:

| Característica | Salida en Español | Salida en Inglés |
|---|---|---|
| **Encabezado de fecha** | `Fecha: 12 May 2025` | `Date: 12 May 2025` |
| **Etiqueta de remitente** | `Enviado:` / `Recibido:` | `Sent:` / `Received:` |
| **Etiqueta de medios** | `[Imagen]`, `[Audio]` | `[Image]`, `[Audio]` |
| **Reacción** | `-❤️ me gusta` | `-❤️ liked` |

---

## 🔧 Resumen técnico (Mejoras V2)

| Característica | Implementación técnica |
|---|---|
| **Intercepción de red** | Sobrescribe `window.fetch` y `XMLHttpRequest` para capturar metadatos de medios. |
| **Gestión de Blobs** | Se engancha a `URL.createObjectURL` para identificar los blobs de mensajes de voz. |
| **Generación de ZIP** | Utiliza un constructor ZIP personalizado sin dependencias con sumas de comprobación CRC32. |
| **Resolutor de Reels** | Analiza de forma asíncrona las páginas de Reels para extraer etiquetas `og:video` y `og:image`. |
| **Interfaz Adaptativa** | Construida con CSS/JS puro (estilo Blur-morphism), sensible a cambios en el viewport. |

---

## 📈 Historial de versiones

**v2.0.0 (Actual)**
- Se añadió el Dashboard interactivo (Overlay UI).
- Soporte multi-idioma (ES, EN, TR) para UI y archivos de salida.
- Se añadieron formatos de exportación ZIP, JSON y Markdown.
- Intercepción de medios en tiempo real (Voz, Reels, Imágenes).
- Herramienta de extracción de transcripciones de voz.
- Funciones de selección, búsqueda y filtrado por categoría.

**v1.0.0**
- Lanzamiento inicial. Exportador de .txt basado en consola.

---

## 👨‍💻 Autor

**Miabeyefendi**
- GitHub: [@Miabeyefendi](https://github.com/Miabeyefendi)
- Proyecto: **InstaDM-Scraper**

*Construido para la privacidad, actualizado para el poder.*
