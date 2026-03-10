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

*Salidas elegantes para situaciones imposibles — powered by Claude AI*

---

![Status](https://img.shields.io/badge/estado-operativo-brightgreen?style=for-the-badge&logo=checkmarx)
![Claude](https://img.shields.io/badge/motor-Claude_Sonnet_4-blueviolet?style=for-the-badge&logo=anthropic)
![Stack](https://img.shields.io/badge/stack-HTML_·_CSS_·_JS-orange?style=for-the-badge)
![Responsabilidad](https://img.shields.io/badge/responsabilidad-ninguna-red?style=for-the-badge)

</div>

---

## ¿Qué es V.I.D.A.?

> **V.I.D.A.** es un generador de excusas con inteligencia artificial para las situaciones sociales más incómodas de la vida moderna.  
> Selecciona tu situación, el nivel de urgencia, añade contexto opcional — y en segundos tendrás una excusa creíble, lista para copiar y pegar.

No más bloqueos mentales. No más "es que..." sin terminar la frase. Solo excusas de precisión quirúrgica.

---

## 🎭 Categorías disponibles

| Emoji | Situación | Descripción |
|-------|-----------|-------------|
| 👻 | **No quiero quedar** | Para cuando no tienes ganas pero tampoco quieres quedar mal |
| 📵 | **Cancelar plan a último momento** | Emergencias de última hora con cobertura narrativa sólida |
| 🛌 | **No ir al trabajo / colegio** | Bajas de emergencia con justificación médico-social |

---

## ⚡ Niveles de urgencia

```
🌿  SIN PRISA    →  Tienes tiempo de construir la excusa con calma
⚡  URGENTE      →  Necesitas algo creíble en los próximos minutos  
🔥  ¡CRÍTICO!    →  La situación explota ahora mismo
```

---

## 🚀 Cómo usarlo

### 1 — Consigue tu API Key

Ve a [console.anthropic.com](https://console.anthropic.com/) y genera una API key.

### 2 — Configura el proyecto

Abre `app.js` y reemplaza la primera variable:

```js
const API_KEY = "TU_API_KEY_AQUI";  // ← pon aquí tu clave
```

> ⚠️ **Importante:** No subas tu API key a GitHub ni la compartas. Cualquier persona que la tenga puede usarla y gastar tus créditos de Anthropic.

### 3 — Abre en el navegador

```bash
# Opción A: directamente
Abre index.html en tu navegador

# Opción B: con Live Server (recomendado)
Click derecho en index.html → Open with Live Server
```

> 💡 Se recomienda Live Server porque algunos navegadores bloquean llamadas a APIs externas desde `file://`

---

## 📁 Estructura del proyecto

```
VIDA/
├── 📄 index.html   →  Estructura y layout
├── 🎨 style.css    →  Estilos, tema y animaciones
├── ⚙️  app.js       →  Lógica + integración con la API
└── 📖 README.md    →  Este archivo
```

---

## 🔧 Personalización

¿Quieres tunear V.I.D.A. a tu gusto?

| Qué cambiar | Dónde |
|-------------|-------|
| Colores y tema visual | Variables `:root` en `style.css` |
| Añadir nuevas situaciones | Array `SITUATIONS` en `app.js` |
| Tono de las excusas | Función `buildPrompt()` en `app.js` |
| Modelo de IA | Variable `model` en `callClaude()` |

---

## ⚖️ Aviso legal

```
V.I.D.A. no se hace responsable de:
  → Relaciones deterioradas por excusas mal ejecutadas
  → Jefes que no se creen lo de "la tubería"
  → Amigos que ya no te invitan a nada
  → Consecuencias kármicas a largo plazo

El uso responsable (o irresponsable) es tuyo.
```

---

<div align="center">

*Hecho con amor + poca vergüenza*

</div>