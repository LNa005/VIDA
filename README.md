<div align="center">

```
 ██╗   ██╗██╗██████╗  █████╗ 
 ██║   ██║██║██╔══██╗██╔══██╗
 ██║   ██║██║██║  ██║███████║
 ╚██╗ ██╔╝██║██║  ██║██╔══██║
  ╚████╔╝ ██║██████╔╝██║  ██║
   ╚═══╝  ╚═╝╚═════╝ ╚═╝  ╚═╝
```

### **V**erificador de **I**nconsistencias **D**iscretamente **A**ceptables

*Salidas elegantes para situaciones imposibles*

---

![Status](https://img.shields.io/badge/estado-EN%20DESARROLLO-orange?style=for-the-badge)
![WIP](https://img.shields.io/badge/⚠️_NO_LISTO_PARA_USO-red?style=for-the-badge)
![Claude](https://img.shields.io/badge/motor-Claude_Sonnet-blueviolet?style=for-the-badge&logo=anthropic)
![Stack](https://img.shields.io/badge/stack-HTML_·_CSS_·_JS-orange?style=for-the-badge)

</div>

---

> ## ⚠️ AVISO IMPORTANTE — TRABAJO EN PROGRESO
>
> **Este proyecto NO está listo para uso.** Hay bugs conocidos pendientes de resolver y la funcionalidad principal puede no funcionar correctamente dependiendo del entorno.
> No se recomienda compartir ni usar en producción hasta que se resuelvan los problemas listados en la sección [Bugs pendientes](#-bugs-pendientes).

---

## ¿Por qué existe V.I.D.A.?

Porque todos hemos estado ahí. El chat abierto, el cursor parpadeando, y el cerebro en blanco intentando inventarse algo creíble para no ir al trabajo, cancelar ese plan o evitar quedar con alguien sin que parezca mala excusa.

**V.I.D.A. lo hace por ti.** En segundos. Con IA.

> ⚠️ **Nota:** La generación de excusas aún no funciona de forma estable en todos los entornos. Ver [Bugs pendientes](#-bugs-pendientes).

---

## ✨ Lo que puede hacer *(cuando funcione)*

> **Estado actual:** Funcionalidades en desarrollo. Algunas pueden no responder como se espera.

**🔍 Detección automática** — escribe el contexto y V.I.D.A. detecta sola qué tipo de excusa necesitas, sin que tengas que seleccionar nada.

**📸 Análisis de capturas** — sube una foto del chat y la IA lee la conversación, entiende la situación y genera la excusa perfecta para ese contexto concreto.

**🎭 Excusas a medida** — no son plantillas genéricas. Cada excusa se genera en tiempo real adaptada a tu situación, urgencia y contexto.

---

## 🎭 Categorías

| Emoji | Situación | Cuándo usarla |
|-------|-----------|---------------|
| 👻 | **No quiero quedar** | Cuando el plan aún no está confirmado y quieres esquivarlo |
| 📵 | **Cancelar a último momento** | Cuando ya dijiste que sí pero ya no puedes más |
| 🛌 | **No ir al trabajo / colegio** | Bajas de emergencia con narrativa sólida |

---

## ⚡ Niveles de urgencia

```
🌿  SIN PRISA    →  Tienes margen para construir la coartada con calma
⚡  URGENTE      →  Necesitas algo creíble en los próximos minutos
🔥  ¡CRÍTICO!    →  La situación explota ahora mismo, no hay tiempo
```

---

## 🐛 Bugs pendientes

> Esta sección recoge los problemas conocidos que hay que resolver antes de que el proyecto esté listo.

### ❌ `Uncaught SyntaxError: Unexpected token 'export'`

**Estado:** Pendiente de investigación  
**Prioridad:** Alta — bloquea la funcionalidad principal en algunos entornos

**Descripción:**  
Al cargar la aplicación en ciertas configuraciones, la consola del navegador lanza el siguiente error:

```
Uncaught SyntaxError: Unexpected token 'export'   chrome-extension://...
```

**Causa probable:**  
El error parece originarse desde una extensión de Chrome que inyecta scripts con sintaxis de módulos ES (`export`) en un contexto donde no está permitido. No está claro aún si es un conflicto externo o un problema propio del código.

**Pasos para reproducir:**  
1. Abrir `index.html` con una o más extensiones de Chrome activas
2. Abrir la consola del navegador (F12)
3. El error aparece antes de que la app termine de cargar

**Lo que hay que revisar:**
- Comprobar si el error desaparece en ventana de incógnito (sin extensiones)
- Identificar si algún script propio usa `export` fuera de un contexto de módulo
- Si el error viene de una extensión externa, valorar añadir un aviso en el README para el usuario final

**Hasta que esté resuelto:** Abrir la app en modo incógnito como medida provisional.

---

## 🚀 Instalación *(en desarrollo — puede no funcionar)*

> ⚠️ Los pasos de abajo son la intención del proyecto, pero la configuración puede fallar hasta que se resuelvan los bugs pendientes.

### 1 — Consigue tu API Key de OpenRouter

Ve a **[openrouter.ai](https://openrouter.ai)** → crea cuenta → **Keys** → **Create Key**

> OpenRouter es gratuito para empezar y te da acceso a Claude sin necesidad de cuenta de Anthropic.

### 2 — Configura el proyecto

Abre `index.html`, localiza la variable `API_KEY` dentro del bloque `<script>` y sustitúyela:

```js
const API_KEY = "sk-or-v1-AQUI_TU_KEY";
```

> ⚠️ El archivo `app.js` existe pero actualmente **no se usa** — todo el código JS está embebido directamente en `index.html`. Pon la key ahí, no en `app.js`.

### 3 — Abre en el navegador

```
Opción A → abre index.html directamente en tu navegador
Opción B → usa Live Server en VSCode (recomendado)
```

> 💡 Si tienes problemas, prueba primero en ventana de incógnito para descartar conflictos con extensiones. Ver bug conocido arriba.

---

## 📁 Estructura

```
VIDA/
├── 📄 index.html   →  Estructura, estilos y lógica (todo embebido aquí)
├── 🎨 style.css    →  Estilos externos (actualmente no se carga)
├── ⚙️  app.js       →  Versión externa de la lógica (actualmente no se usa)
└── 📖 README.md    →  Este archivo
```

> ⚠️ **Nota de estructura:** El proyecto tiene `app.js` y `style.css` como archivos separados, pero `index.html` los tiene todos embebidos internamente. Pendiente de unificar.

---

## 🔧 Personalización

| Qué cambiar | Dónde |
|-------------|-------|
| Colores y tema | Variables `:root` en el `<style>` de `index.html` |
| Añadir situaciones | Array `SITUATIONS` en el `<script>` de `index.html` |
| Tono de las excusas | Función `buildPrompt()` en el `<script>` de `index.html` |
| Modelo de IA | Variable `MODEL` en el `<script>` de `index.html` |

---

## 🤝 Contribuir

El proyecto está en desarrollo activo. Si encuentras bugs o tienes ideas, abre un issue. Cualquier ayuda para resolver los [bugs pendientes](#-bugs-pendientes) es bienvenida.

---

<div align="center">

*Hecho con 🤖 + poca vergüenza · Úsala bien (o mal, tú decides)*

**⚠️ EN DESARROLLO — NO APTO PARA USO GENERAL AÚN ⚠️**

</div>