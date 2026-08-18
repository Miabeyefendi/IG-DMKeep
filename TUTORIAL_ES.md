<div align="center">

# 📖 Guía de IG-DMKeep

**v2.0.0 · Última actualización 2026-08-18**

[English](./TUTORIAL.md) · [Türkçe](./TUTORIAL_TR.md) · **Español** · [简体中文](./TUTORIAL_ZH.md) · [Русский](./TUTORIAL_RU.md)

[Volver al README](./README_ES.md) · [Cambios](./CHANGELOG.md)

</div>

---

Este documento explica cómo funciona IG-DMKeep por dentro. Si solo quieres ejecutarlo, el [README](./README_ES.md) es más corto.

## 📑 Contenido

- [Visión general](#-visión-general)
- [Instalación](#-instalación)
- [Recorrido por la interfaz](#️-recorrido-por-la-interfaz)
- [Referencia de funciones](#-referencia-de-funciones)
- [Referencia de configuración](#️-referencia-de-configuración)
- [Resolución de problemas](#-resolución-de-problemas)
- [Preguntas frecuentes](#-preguntas-frecuentes)
- [Glosario](#-glosario)

---

## 🔭 Visión general

### Qué hace

Instagram te ofrece una descarga de datos, pero lo que llega es un archivo pensado para cumplir la normativa, no para leerse. IG-DMKeep hace lo contrario: lee la conversación que tienes delante, en el navegador donde ya has iniciado sesión, y la escribe en un formato que puedes usar de verdad.

### Cómo funciona

```
  Hilo de DM abierto en la pagina
        |
        |  el motor de scroll recorre el hilo hacia atras
        v
  Analizador del DOM  -----------> registros de mensajes
        |                           texto, marca de tiempo, remitente, reacciones
        |
  hooks de red (fetch / XHR / PerformanceObserver)
        |                           URLs directas que el DOM nunca muestra
        v
  fusion por identificador de mensaje
        |
        +--> JSON        estructurado, para procesar
        +--> TXT         plano, para leer
        +--> Markdown    para publicar
        +--> ZIP         texto mas los archivos descargados
```

Lo importante es la segunda entrada. Instagram no pone en el DOM un enlace utilizable a un reel o a una nota de voz, así que analizar solo la página te deja un mensaje que dice "aquí había un vídeo". Los hooks observan el tráfico que genera la propia página y se quedan con las URLs que pasan.

### Estructura de archivos

| Ruta | Qué es |
|---|---|
| `instadm-scraper-v2.js` | La herramienta actual, 3700 líneas, todo lo descrito aquí |
| `instadm-scraper.js` | La versión original, 342 líneas, salida por consola y exportación de texto |

---

## 📦 Instalación

### Requisitos

- Un navegador de escritorio. La versión móvil no renderiza la conversación igual y no está soportada.
- Tu propia cuenta de Instagram, con la sesión iniciada en `www.instagram.com`.
- Nada más. Sin extensión, sin compilación, sin clave de API.

### Paso a paso

1. Abre `www.instagram.com` e inicia sesión.
2. Abre el hilo de DM que quieres guardar. **No la lista de la bandeja de entrada, el hilo en sí.** El script lee lo que está renderizado, y en la bandeja no hay conversación que leer.
3. Espera a que los mensajes sean visibles.
4. Abre la consola con `F12`, o `Ctrl + Shift + J` en Chrome y Edge, `Ctrl + Shift + K` en Firefox, `Cmd + Option + J` en Mac.
5. Pega `instadm-scraper-v2.js` completo y pulsa Enter.

Algunos navegadores bloquean el código pegado en la consola hasta que escribes `allow pasting` una vez. Es una medida de seguridad del navegador, no un error de este script.

### Verificar que ha funcionado

El panel aparece sobre la página. Si en su lugar ves `Conversation container not found`, el paso 2 no ocurrió: entra en el hilo e inténtalo otra vez.

### Desinstalar

Recarga la página. No se instala nada y nada persiste.

---

## 🖥️ Recorrido por la interfaz

El panel se inyecta en la página y flota sobre ella. La maquetación de debajo queda intacta, así que Instagram sigue funcionando con el panel abierto.

| Zona | Qué contiene |
|---|---|
| Scan | Inicio, progreso y el recuento de mensajes en curso |
| Filter | Caja de palabra clave y filtros de tipo para imágenes, audio y reels |
| Timeline | Los mensajes recogidos, cada uno con una casilla |
| Export | Selector de formato, selector de idioma, interruptores de medios y transcripción |

---

## 🧩 Referencia de funciones

### Captura de medios y sistema de hooks

**Qué hace.** Recupera URLs directas de reels, mensajes de voz e imágenes a resolución completa.

**Cómo funciona.** Antes de empezar el escaneo se envuelven `fetch` y `XMLHttpRequest`, de modo que toda petición que hace la página pasa primero por la herramienta. En paralelo, un `PerformanceObserver` observa las entradas de tiempos de recursos, lo que atrapa medios que la página carga por vías que los envoltorios no ven. También se interceptan las URL de tipo blob, porque Instagram sirve parte del material como blobs que de otro modo quedarían inalcanzables. Todo lo que parece un medio se guarda en una tabla indexada por mensaje.

**Límites.** Un hook solo ve el tráfico que ocurre mientras la herramienta está en marcha. El material que se cargó antes de pegar el script ya pasó, y esa es una de las razones por las que el escaneo recorre el hilo en vez de leer lo que hay en pantalla.

### Detección del remitente

**Qué hace.** Decide, para cada mensaje, si lo enviaste tú o la otra persona.

**Cómo funciona.** Instagram no etiqueta esto de forma que sobreviva a sus propios rediseños, así que la dirección se deduce de la disposición y la posición estructural, no de un nombre de clase que cambia cada pocos meses. Los mensajes se agrupan por tandas, porque un bloque de mensajes consecutivos de una misma persona comparte dirección.

**Límites.** Los grupos con varios participantes son más difíciles que las conversaciones de dos, y los tipos de mensaje poco habituales pueden atribuirse mal.

### Transcripción de mensajes de voz

**Qué hace.** Convierte las notas de voz en texto buscable dentro de la exportación.

**Cómo funciona.** No ejecuta reconocimiento de voz. Instagram ya genera transcripciones para los mensajes de voz; este modo las solicita y las recoge, y adjunta cada una a su mensaje.

**Límites.** Si Instagram no tiene transcripción para una nota, no hay nada que recoger. La precisión es de Instagram, no de esta herramienta.

### Exportación ZIP

**Qué hace.** Empaqueta el texto de la conversación junto con los archivos multimedia reales en un solo archivo.

**Cómo funciona.** El archivo se construye en el navegador. Cada URL de medio capturada se descarga, se mantiene en memoria y se escribe en un ZIP estructurado junto a la exportación de texto.

**Límites.** Este es el camino lento, porque descarga cada archivo. Los hilos largos con muchos reels tardan y consumen ancho de banda real. Las conversaciones muy grandes pueden chocar con los límites de memoria del navegador; en ese caso, exporta por partes.

---

## ⚙️ Referencia de configuración

### Export

| Opción | Valores | Efecto |
|---|---|---|
| Format | JSON, TXT, Markdown, ZIP | Forma de la salida. ZIP es la única que incluye archivos multimedia. |
| Selection | Todo, o los mensajes marcados | Exportar todo, o solo lo seleccionado |
| Language | Inglés, turco, español | Idioma de las cabeceras escritas en el archivo |

### Filter

| Opción | Efecto |
|---|---|
| Keyword | Mostrar solo los mensajes que contienen el texto |
| Type | Reducir a solo imágenes, solo audio o solo reels |

### Media

| Opción | Efecto |
|---|---|
| Download media | Descargar los archivos reales e incluirlos en el ZIP |
| Transcription | Recoger las transcripciones de Instagram para los mensajes de voz |

### Dónde se guarda algo

En ningún sitio. No se escribe nada fuera del archivo de exportación que guarda tu navegador, y no se conserva nada entre ejecuciones. Recargar la página lo termina todo.

---

## 🔧 Resolución de problemas

### "Conversation container not found. Open a DM thread first."

**Causa.** El script no encontró una conversación renderizada. No basta con haber iniciado sesión ni con estar en la lista de la bandeja.
**Solución.** Entra en el hilo, espera a que los mensajes sean visibles y luego pega. Si el hilo está abierto y el error persiste, Instagram ha cambiado su marcado; abre una incidencia con tu navegador y versión.

### Faltan mensajes antiguos en la exportación

**Causa.** Instagram descarga mensajes de la página conforme te desplazas, así que no están en el DOM para leerse.
**Solución.** Deja que el escaneo termine. Recorre el hilo hacia atrás a propósito. Las conversaciones largas llevan tiempo.

### Falta material, o el ZIP tiene menos archivos de los esperados

**Causa.** El medio se cargó antes de instalar los hooks, o su URL caducó antes de la descarga.
**Solución.** Recarga la página, pega primero el script y solo entonces escanea. No navegues por el hilo a mano antes de empezar.

### El navegador se niega a aceptar el script pegado

**Causa.** Una medida de seguridad del navegador contra la ingeniería social basada en pegar código.
**Solución.** Escribe `allow pasting` una vez en la consola y pega.

### La pestaña se congela o se queda sin memoria

**Causa.** Un hilo muy largo con mucho material retenido en memoria para el ZIP.
**Solución.** Exporta como TXT o JSON, o exporta por partes usando la selección de mensajes.

### Recoger un registro para informar de un fallo

Copia la salida de la consola. **Antes de publicarla, quita todo lo que te identifique a ti o a la otra persona:** nombres de usuario, texto de los mensajes, cookies de sesión y cualquier URL con un token. Una incidencia es pública y permanente.

---

## ❓ Preguntas frecuentes

**¿Sale algo de mi máquina?**
Solo las peticiones que Instagram haría igualmente. No hay ningún servidor de este proyecto ni analíticas.

**¿Puede leer conversaciones en las que no participo?**
No. Solo puede ver lo que tu propia sesión iniciada ya es capaz de mostrar.

**¿Por qué sigue estando el archivo v1?**
Porque 342 líneas se leen de una sentada y se verifican a ojo. Hay quien prefiere auditar un script pequeño antes que confiar en uno grande.

**¿Funciona en la versión móvil?**
No. La conversación se renderiza de otra forma y los selectores no aplican.

---

## 📕 Glosario

| Término | Significado |
|---|---|
| Hook | Un envoltorio sobre `fetch` o `XHR` que permite a la herramienta ver las peticiones de la página |
| PerformanceObserver | API del navegador que informa de los recursos cargados, usada para atrapar medios que los hooks no ven |
| URL blob | URL temporal en memoria, usada por Instagram para parte del material |
| Scroll virtual | Quitar de la página los elementos fuera de pantalla para ahorrar memoria, motivo por el que el escaneo recorre el hilo |
| Dirección | Si un mensaje lo enviaste tú o lo recibiste |

---

<div align="center">
<img src="./assets/divider.svg" width="100%" height="3" alt="">
<br/>
<sub>Creado por <b><a href="https://github.com/Miabeyefendi">Miabeyefendi</a></b> · <a href="./README_ES.md">Volver al README</a></sub>
</div>
