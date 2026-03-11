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

![Status](https://img.shields.io/badge/estado-operativo-brightgreen?style=for-the-badge&logo=checkmarx)
![Claude](https://img.shields.io/badge/motor-Claude_Sonnet-blueviolet?style=for-the-badge&logo=anthropic)
![Stack](https://img.shields.io/badge/stack-HTML_·_CSS_·_JS-orange?style=for-the-badge)
![Responsabilidad](https://img.shields.io/badge/responsabilidad-ninguna-red?style=for-the-badge)

</div>

---

## ¿Por qué existe V.I.D.A.?

Porque todos hemos estado ahí. El chat abierto, el cursor parpadeando, y el cerebro en blanco intentando inventarse algo creíble para no ir al trabajo, cancelar ese plan o evitar quedar con alguien sin que parezca mala excusa.

**V.I.D.A. lo hace por ti.** En segundos. Con IA.

---

## ✨ Lo que puede hacer

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

## 🚀 Cómo usarlo

### 1 — Consigue tu API Key de OpenRouter

Ve a **[openrouter.ai](https://openrouter.ai)** → crea cuenta → **Keys** → **Create Key**

> OpenRouter es gratuito para empezar y te da acceso a Claude sin necesidad de cuenta de Anthropic.

### 2 — Pon tu key en app.js

Abre `app.js` y sustituye la línea de la key:

```js
const API_KEY = "sk-or-v1-AQUI_TU_KEY";
```

### 3 — Abre en el navegador

```
Opción A → abre index.html directamente en tu navegador
Opción B → usa Live Server en VSCode (recomendado)
```

> 💡 Si ves errores de extensiones de Chrome en la consola, ábrelo en modo incógnito — no afectan al funcionamiento.

---

## 📁 Estructura

```
VIDA/
├── 📄 index.html   →  Estructura y layout
├── 🎨 style.css    →  Estilos, tema y animaciones
├── ⚙️  app.js       →  Lógica + integración con OpenRouter
└── 📖 README.md    →  Este archivo
```

---

## 🔧 Personalización

| Qué cambiar | Dónde |
|-------------|-------|
| API key | Variable `API_KEY` en `app.js` |
| Colores y tema | Variables `:root` en `style.css` |
| Añadir situaciones | Array `SITUATIONS` en `app.js` |
| Tono de las excusas | Función `buildPrompt()` en `app.js` |
| Modelo de IA | Variable `MODEL` en `app.js` |

---

## 🤝 Úsala, compártela, mejórala

Si V.I.D.A. te ha salvado de una situación incómoda, **comparte el proyecto**. ¿Tienes ideas para nuevas categorías o has encontrado un bug? Abre un issue o manda un PR.

---

<div align="center">

*Hecho con poca vergüenza · Úsala bien (o mal, tú decides)*

</div>