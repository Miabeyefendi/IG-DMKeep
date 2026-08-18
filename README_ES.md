<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="./assets/logo-dark.svg">
  <img src="./assets/logo.svg" width="120" alt="IG-DMKeep">
</picture>

# IG-DMKeep

**Guarda tus propias conversaciones de Instagram antes de perderlas. Historial completo con marcas de tiempo, remitente, reacciones y multimedia, exportado a JSON, TXT, Markdown o ZIP. Todo ocurre en tu navegador.**

[![Licencia: AGPL v3](https://img.shields.io/badge/License-AGPL_v3-A78BFA?style=for-the-badge&logo=gnu&logoColor=white)](./LICENSE)
[![Versión](https://img.shields.io/github/v/release/Miabeyefendi/IG-DMKeep?style=for-the-badge&color=F59E0B&label=version)](https://github.com/Miabeyefendi/IG-DMKeep/releases/latest)
[![Plataforma](https://img.shields.io/badge/Browser_Console-1E293B?style=for-the-badge&logo=googlechrome&logoColor=white)](#-instalación)
[![Estado](https://img.shields.io/badge/status-active-22C55E?style=for-the-badge)](#)
[![Autor](https://img.shields.io/badge/by-Miabeyefendi-0EA5E9?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Miabeyefendi)

[English](./README.md) · [Türkçe](./README_TR.md) · **Español** · [简体中文](./README_ZH.md) · [Русский](./README_RU.md)

[Instalación](#-instalación) · [Funciones](#-lo-destacado) · [Uso](#-inicio-rápido) · [Guía](./TUTORIAL_ES.md) · [Cambios](./CHANGELOG.md)

<a href="https://github.com/Miabeyefendi/IG-DMKeep/releases/latest">
  <img src="./assets/btn-download.svg" height="52" alt="Descargar la última versión">
</a>
<a href="./TUTORIAL_ES.md">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-tutorial-dark.svg">
    <img src="./assets/btn-tutorial.svg" height="52" alt="Leer la guía">
  </picture>
</a>

</div>

---

## ✨ Lo destacado

- **Tus datos siguen siendo tuyos** - todo se ejecuta localmente en tu navegador. Sin servidor, sin extensión, sin clave de API, sin analíticas. Nada de tus conversaciones sale de tu máquina.
- **Una interfaz, no un muro de consola** - se inyecta un panel en la página desde el que controlas el escaneo, filtras la línea de tiempo y eliges qué exportar.
- **Cuatro formatos de exportación** - JSON para procesar, TXT para leer, Markdown para publicar, o un ZIP que empaqueta el material junto al texto.
- **Multimedia que la página no te muestra** - la herramienta observa el tráfico de red y el `PerformanceObserver` para recuperar enlaces directos de reels, mensajes de voz e imágenes a resolución completa que nunca aparecen en el DOM.
- **Mensajes de voz como texto** - un modo dedicado recoge las transcripciones propias de Instagram para las notas de voz, de modo que la exportación sea buscable.
- **Filtra y busca antes de exportar** - encuentra mensajes por palabra clave, o reduce la línea de tiempo solo a imágenes, audio o reels.
- **Exporta una selección, no solo todo** - marca los mensajes que realmente quieres.
- **Salida en tu idioma** - las cabeceras de la exportación siguen tu elección de idioma, así que una exportación en turco pone `Gönderilen:` y no `Sent:`.
- **Aguanta el scroll virtual** - Instagram descarga mensajes conforme te desplazas; el escaneo está construido teniendo eso en cuenta en vez de pelearse con ello.

---

## 📦 Instalación

### Requisitos

| | |
|---|---|
| Navegador | Chrome, Edge o Firefox en escritorio |
| Cuenta | Tu propia cuenta de Instagram, con un hilo de DM abierto |
| Instalación | Ninguna. Es un script de consola. |

![JavaScript](https://img.shields.io/badge/JavaScript-1E293B?style=for-the-badge&logo=javascript&logoColor=A78BFA)
![Instagram](https://img.shields.io/badge/Instagram-1E293B?style=for-the-badge&logo=instagram&logoColor=A78BFA)

### Elige una versión

| Versión | Archivo | Qué es |
|---|---|---|
| **v2** | [`instadm-scraper-v2.js`](./instadm-scraper-v2.js) | La actual. Interfaz superpuesta, captura de multimedia, exportación ZIP, transcripción. |
| **v1** | [`instadm-scraper.js`](./instadm-scraper.js) | La original. Solo salida por consola, exportación de texto, 342 líneas. Se mantiene para quien quiera algo pequeño que pueda leer de principio a fin. |

<details>
<summary><b>¿Prefieres clonarlo?</b></summary>

```bash
git clone https://github.com/Miabeyefendi/IG-DMKeep.git
```

Sin compilación y sin dependencias.

</details>

---

## 🚀 Inicio rápido

1. Abre [www.instagram.com](https://www.instagram.com/) en escritorio e inicia sesión.
2. **Abre el hilo de DM que quieres guardar.** El script lee la conversación que está en pantalla, así que este paso no es opcional.
3. Abre la consola. `F12` o `Ctrl + Shift + J` en Chrome y Edge, `Ctrl + Shift + K` en Firefox. En Mac, `Cmd + Option + J`.
4. Pega [`instadm-scraper-v2.js`](./instadm-scraper-v2.js) completo y pulsa Enter.
5. Aparece la interfaz. Inicia el escaneo, espera a que recorra el hilo hacia atrás y luego elige un formato de exportación.

> **Si te sale "Conversation container not found", no estás dentro de un hilo.** Abrir la bandeja de entrada no basta. Entra en la conversación concreta, espera a que se rendericen los mensajes y solo entonces pega el script.

---

## ⚙️ Configuración

Todo se ajusta en la interfaz, no se edita nada en el archivo.

| Grupo | Opción | Qué hace |
|---|---|---|
| Export | Format | JSON, TXT, Markdown o ZIP |
| Export | Selection | La conversación entera, o solo los mensajes que marques |
| Export | Language | Idioma de las cabeceras escritas en el archivo exportado |
| Filter | Keyword | Mostrar solo mensajes que contengan una palabra o frase |
| Filter | Type | Solo imágenes, solo audio o solo reels |
| Media | Download media | Descargar los archivos reales y empaquetarlos en el ZIP |
| Media | Transcription | Recoger las transcripciones de Instagram para los mensajes de voz |

Cómo funciona cada una por dentro, y qué hacer cuando alguna falla, está en la [guía](./TUTORIAL_ES.md).

---

## 📖 Documentación

- [**Guía**](./TUTORIAL_ES.md) - cómo funcionan realmente los motores de captura, detección de remitente, transcripción y ZIP
- [**Cambios**](./CHANGELOG.md) - qué cambió en cada versión
- [**Contribuir**](./CONTRIBUTING.md) - cómo enviar un cambio
- [**Seguridad**](./SECURITY.md) - cómo informar de una vulnerabilidad en privado

---

## ❓ Preguntas frecuentes

<details>
<summary><b>"Conversation container not found. Open a DM thread first."</b></summary>

El script no encontró una conversación renderizada en la página. No basta con haber iniciado sesión ni con estar en la lista de la bandeja de entrada. Abre el hilo concreto, espera a que los mensajes sean visibles y solo entonces pega el script. Si el hilo está abierto y aun así lo ves, Instagram ha cambiado su marcado; abre una incidencia indicando la versión de tu navegador.

</details>

<details>
<summary><b>¿Esto envía mis mensajes a algún sitio?</b></summary>

No. Todo se ejecuta en la página que ya tienes abierta, y la exportación la escribe tu navegador en tu propio disco. No hay servidor, ni extensión, ni analíticas. Esa es toda la razón de que esto sea un script de consola.

</details>

<details>
<summary><b>¿Puedo exportar los DM de otra persona?</b></summary>

No. El script solo puede leer lo que tu propia sesión iniciada ya es capaz de mostrar. Es una forma de conservar una copia de tus propias conversaciones, nada más.

</details>

<details>
<summary><b>¿Por qué tarda tanto el ZIP?</b></summary>

Porque descarga los archivos multimedia uno a uno y los empaqueta en el navegador. Un hilo largo con muchos reels y notas de voz es mucho tráfico. Las exportaciones de solo texto son casi instantáneas.

</details>

<details>
<summary><b>Faltan algunos mensajes antiguos.</b></summary>

Instagram descarga mensajes de la memoria conforme te desplazas, así que el escaneo tiene que recorrer el hilo hacia atrás para traerlos de vuelta a la página. Déjalo terminar. En conversaciones muy largas esto lleva su tiempo.

</details>

<details>
<summary><b>¿Debería usar v1 o v2?</b></summary>

v2, salvo que quieras algo lo bastante pequeño como para leerlo de una sentada. v1 son 342 líneas y exporta texto plano; v2 es la herramienta completa.

</details>

---

## 🤝 Contribuir

Las contribuciones son bienvenidas. Lee primero [CONTRIBUTING.md](./CONTRIBUTING.md) y [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md). Al contribuir aceptas licenciar tu trabajo bajo la AGPL-3.0.

<div align="center">
<a href="https://github.com/Miabeyefendi/IG-DMKeep/issues/new?template=bug_report.yml">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-report-bug-dark.svg">
    <img src="./assets/btn-report-bug.svg" height="52" alt="Informar de un fallo">
  </picture>
</a>
<a href="https://github.com/Miabeyefendi/IG-DMKeep/stargazers">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/btn-star-dark.svg">
    <img src="./assets/btn-star.svg" height="52" alt="Dar una estrella a este repositorio">
  </picture>
</a>
</div>

---

## 🛡️ Seguridad

¿Has encontrado una vulnerabilidad? No abras una incidencia pública. Sigue el proceso privado descrito en [SECURITY.md](./SECURITY.md).

---

## 📜 Licencia

IG-DMKeep está licenciado bajo la **GNU Affero General Public License v3.0 (AGPL-3.0)**, junto con los términos suplementarios del archivo [NOTICE](./NOTICE). En resumen:

- Puedes usar, estudiar, modificar, redistribuir e incluso ganar dinero con esta obra de forma gratuita, **siempre que** mantengas el código fuente completo disponible bajo la AGPL-3.0, incluido cualquier uso alojado, SaaS o en red (AGPL Sección 13), y conserves la atribución de autoría indicada abajo.
- Para usar esta obra en un producto propietario o de código cerrado, o para ejecutarla como un SaaS cerrado, necesitas una **licencia comercial escrita aparte**, que puede incluir regalías o reparto de ingresos. Consulta [NOTICE](./NOTICE), Sección 8, y contacta conmigo.

### Atribución (obligatoria)

Según la Sección 7(b) de la AGPL-3.0, la siguiente atribución debe conservarse de forma visible y sin modificar en cualquier copia, bifurcación o despliegue de este proyecto:

> **Miabeyefendi (Mustafa Ihsan Albayrak)** - https://github.com/Miabeyefendi

### Descargo de responsabilidad

Este software se proporciona "tal cual", sin garantía de ningún tipo. Lo ejecutas por tu cuenta y riesgo y eres la única persona responsable de tu propio uso, incluido el cumplimiento de los términos de servicio de cualquier plataforma de terceros con la que interactúe, en particular Instagram. Instagram no está afiliado a este proyecto ni lo respalda; su nombre y sus marcas pertenecen a su propietario. El autor no acepta responsabilidad alguna por bloqueos de cuenta, pérdida de datos ni ningún otro daño, en la máxima medida permitida por la ley aplicable. Los términos completos están en los archivos [LICENSE](./LICENSE) y [NOTICE](./NOTICE).

---

## 📬 Contacto

- GitHub: [@Miabeyefendi](https://github.com/Miabeyefendi)
- Para licencias comerciales o consultas sobre reparto de ingresos, escríbeme a través de mi perfil de GitHub.

<div align="center">
<br/>
<img src="./assets/divider.svg" width="100%" height="3" alt="">
<br/>
<sub>Creado por <b><a href="https://github.com/Miabeyefendi">Miabeyefendi</a></b></sub>
</div>
