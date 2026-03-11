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
> **Este proyecto NO está listo para uso.** Hay bugs conocidos pendientes de resolver y la funcionalidad principal no funciona aún.
> No se recomienda compartir ni usar en producción hasta que se resuelvan los problemas listados en la sección [Bugs pendientes](#-bugs-pendientes).

---

## ¿Por qué existe V.I.D.A.?

Porque todos hemos estado ahí. El chat abierto, el cursor parpadeando, y el cerebro en blanco intentando inventarse algo creíble para no ir al trabajo, cancelar ese plan o evitar quedar con alguien sin que parezca mala excusa.

**V.I.D.A. lo hace por ti.** En segundos. Con IA.

> ⚠️ **Nota:** La generación de excusas no funciona aún. Ver [Bugs pendientes](#-bugs-pendientes).

---

## ✨ Lo que podrá hacer *(cuando esté listo)*

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

---

### ❌ Error 400 al llamar a la API — la excusa no se genera

**Estado:** 🔴 Pendiente — **revisar mañana**  
**Prioridad:** Crítica — bloquea la funcionalidad principal

**Descripción:**  
Al intentar generar una excusa, la consola muestra:

```
Failed to load resource: the server responded with a status of 400
openrouter.ai/api/v1/chat/completions
```

La app cae al `catch` y muestra siempre el mismo texto de emergencia (`"Me quedé sin batería"`), ocultando el error real.

**Causa probable:**  
El nombre del modelo en el código puede no ser válido en OpenRouter, o la API key no tiene crédito.

**Pasos para investigar mañana:**

1. Abrir la app en el navegador con la consola abierta (F12)
2. Hacer clic en el enlace `openrouter.ai/api/v1/chat/completions:1` que aparece en rojo — muestra el mensaje exacto de error de la API
3. O ejecutar esto directamente en la consola y leer la respuesta:
```js
fetch("https://openrouter.ai/api/v1/chat/completions", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": "Bearer " + API_KEY
  },
  body: JSON.stringify({
    model: MODEL,
    max_tokens: 10,
    messages: [{role: "user", content: "hola"}]
  })
}).then(r => r.json()).then(d => console.log(JSON.stringify(d)))
```
4. Con el mensaje exacto, determinar si el problema es:
   - El nombre del modelo — probar con `anthropic/claude-3-5-sonnet` o consultar la lista en [openrouter.ai/models](https://openrouter.ai/models)
   - La API key sin crédito o inválida — revisar en [openrouter.ai/keys](https://openrouter.ai/keys)
   - Otro parámetro del body rechazado por OpenRouter

---

### ⚠️ `Uncaught SyntaxError: Unexpected token 'export'`

**Estado:** 🟡 Pendiente — aparentemente externo, no bloquea  
**Prioridad:** Baja

**Descripción:**  
La consola muestra este error al cargar, pero viene de una extensión de Chrome, no del código propio:

```
Uncaught SyntaxError: Unexpected token 'export'   chrome-extension://...
```

**Hasta que se investigue:** No parece bloquear la app. Abrir en incógnito para confirmar que desaparece.

---

## 📁 Estructura

```
VIDA/
├── 📄 index.html   →  Estructura, estilos y lógica (todo embebido aquí)
├── 🎨 style.css    →  Estilos externos (pendiente de conectar)
├── ⚙️  app.js       →  Versión externa de la lógica (pendiente de conectar)
└── 📖 README.md    →  Este archivo
```

> ⚠️ **Nota de estructura:** `app.js` y `style.css` existen como archivos separados pero `index.html` los tiene todo embebido. Pendiente de unificar cuando la app funcione.

---

## 🤝 Contribuir

El proyecto está en desarrollo activo. Si encuentras bugs o tienes ideas, abre un issue.

---

<div align="center">

*Hecho con poca vergüenza · Úsala bien (o mal, tú decides)*

**⚠️ EN DESARROLLO — NO APTO PARA USO GENERAL AÚN ⚠️**

</div>