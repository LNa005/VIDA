// ============================================================
//  V.I.D.A. — app.js
//  Verificador de Inconsistencias Discretamente Aceptables
// ============================================================

const API_KEY = "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";
const OR_URL  = "https://openrouter.ai/api/v1/chat/completions";
const MODEL   = "anthropic/claude-sonnet-4-5";

// ------------------------------------------------------------
// Data
// ------------------------------------------------------------
const SITUATIONS = [
  { id: "noshow", emoji: "👻", label: "No quiero quedar",              color: "#FF4D6D" },
  { id: "cancel", emoji: "📵", label: "Cancelar plan a último momento", color: "#FF9F1C" },
  { id: "work",   emoji: "🛌", label: "No ir al trabajo / colegio",    color: "#9B5DE5" },
];

const URGENCY = [
  { id: "low",  emoji: "🌿", label: "Sin prisa" },
  { id: "mid",  emoji: "⚡", label: "Urgente"   },
  { id: "high", emoji: "🔥", label: "¡Crítico!" },
];

// ------------------------------------------------------------
// State
// ------------------------------------------------------------
let selectedSituation = null;
let selectedUrgency   = null;
let uploadedImageB64  = null;
let uploadedMimeType  = "image/jpeg";
let detectTimer       = null;
let rawExcuse         = "";

// ------------------------------------------------------------
// DOM refs
// ------------------------------------------------------------
const situationsGrid  = document.getElementById("situations");
const urgencyRow      = document.getElementById("urgency");
const contextInput    = document.getElementById("context");
const generateBtn     = document.getElementById("generate-btn");
const loadingEl       = document.getElementById("loading");
const resultEl        = document.getElementById("result");
const resultBody      = document.getElementById("result-body");
const resultLabel     = document.getElementById("result-label");
const copyBtn         = document.getElementById("copy-btn");
const retryBtn        = document.getElementById("retry-btn");
const titleEl         = document.getElementById("title");
const subtitleTop     = document.querySelector(".subtitle-top");
const uploadZone      = document.getElementById("upload-zone");
const uploadInner     = document.getElementById("upload-inner");
const screenshotInput = document.getElementById("screenshot-input");
const uploadPreview   = document.getElementById("upload-preview");
const previewImg      = document.getElementById("preview-img");
const removeImgBtn    = document.getElementById("remove-img");
const analyzingBadge  = document.getElementById("analyzing-badge");
const detectedBadge   = document.getElementById("detected-badge");
const autoDetectBar   = document.getElementById("auto-detect-bar");
const detectText      = document.getElementById("detect-text");

// ------------------------------------------------------------
// Render buttons
// ------------------------------------------------------------
SITUATIONS.forEach(sit => {
  const btn = document.createElement("button");
  btn.className = "situation-btn";
  btn.innerHTML = `<span class="sit-emoji">${sit.emoji}</span><span>${sit.label}</span>`;
  btn.addEventListener("click", () => selectSituation(sit));
  btn.dataset.id = sit.id;
  situationsGrid.appendChild(btn);
});

URGENCY.forEach(urg => {
  const btn = document.createElement("button");
  btn.className = "urgency-btn";
  btn.innerHTML = `<div class="urg-emoji">${urg.emoji}</div><div class="urg-label">${urg.label}</div>`;
  btn.addEventListener("click", () => selectUrgency(urg));
  btn.dataset.id = urg.id;
  urgencyRow.appendChild(btn);
});

// ------------------------------------------------------------
// Selection
// ------------------------------------------------------------
function selectSituation(sit, auto = false) {
  selectedSituation = sit;
  document.querySelectorAll(".situation-btn").forEach(btn => {
    const active = btn.dataset.id === sit.id;
    btn.classList.toggle("active", active);
    btn.style.background  = active ? sit.color : "";
    btn.style.borderColor = active ? sit.color : "";
    btn.style.color       = active ? "#fff" : "";
  });
  setAccent(sit.color);
  if (auto) {
    const activeBtn = document.querySelector(`.situation-btn[data-id="${sit.id}"]`);
    activeBtn?.classList.add("auto-flash");
    setTimeout(() => activeBtn?.classList.remove("auto-flash"), 700);
  }
  checkReady();
}

function selectUrgency(urg) {
  selectedUrgency = urg;
  document.querySelectorAll(".urgency-btn").forEach(btn => {
    const active = btn.dataset.id === urg.id;
    btn.classList.toggle("active", active);
    btn.style.borderColor = active ? getComputedStyle(document.documentElement).getPropertyValue("--accent") : "";
    btn.style.color       = active ? getComputedStyle(document.documentElement).getPropertyValue("--accent") : "";
  });
  checkReady();
}

function setAccent(color) {
  document.documentElement.style.setProperty("--accent", color);
  subtitleTop.style.color = color;
}

function checkReady() {
  generateBtn.disabled = !(selectedSituation && selectedUrgency);
}

// ------------------------------------------------------------
// Auto-detect from text
// ------------------------------------------------------------
contextInput.addEventListener("input", () => {
  const text = contextInput.value.trim();
  if (text.length < 15) {
    autoDetectBar.classList.add("hidden");
    return;
  }
  autoDetectBar.classList.remove("hidden");
  autoDetectBar.style.color = "";
  detectText.textContent = "Detectando situación...";
  clearTimeout(detectTimer);
  detectTimer = setTimeout(() => autoDetectSituation(text), 700);
});

async function autoDetectSituation(text) {
  try {
    const result = await callOR([{
      role: "user",
      content: `Analiza este contexto y clasifícalo en una de estas 3 categorías:
- noshow: no querer quedar con alguien, evitar un plan que aún no está confirmado
- cancel: cancelar un plan ya acordado a último momento
- work: no querer ir al trabajo o al colegio/instituto

Contexto: "${text}"

Responde ÚNICAMENTE con una de estas palabras: noshow, cancel, work`
    }]);
    const detected = result.trim().toLowerCase().replace(/[^a-z]/g, "");
    const sit = SITUATIONS.find(s => s.id === detected);
    if (sit) {
      selectSituation(sit, true);
      detectText.textContent = `✓ ${sit.emoji} ${sit.label}`;
      autoDetectBar.style.color = sit.color;
    } else {
      autoDetectBar.classList.add("hidden");
    }
  } catch {
    autoDetectBar.classList.add("hidden");
  }
}

// ------------------------------------------------------------
// Screenshot upload
// ------------------------------------------------------------
uploadZone.addEventListener("click", (e) => {
  if (e.target === removeImgBtn) return;
  if (!uploadedImageB64) screenshotInput.click();
});

uploadZone.addEventListener("dragover", (e) => {
  e.preventDefault();
  uploadZone.classList.add("drag-over");
});

uploadZone.addEventListener("dragleave", () => uploadZone.classList.remove("drag-over"));

uploadZone.addEventListener("drop", (e) => {
  e.preventDefault();
  uploadZone.classList.remove("drag-over");
  const file = e.dataTransfer.files[0];
  if (file && file.type.startsWith("image/")) handleImageFile(file);
});

screenshotInput.addEventListener("change", () => {
  const file = screenshotInput.files[0];
  if (file) handleImageFile(file);
});

removeImgBtn.addEventListener("click", (e) => {
  e.stopPropagation();
  clearImage();
});

function handleImageFile(file) {
  uploadedMimeType = file.type || "image/jpeg";
  const reader = new FileReader();
  reader.onload = async (e) => {
    const dataUrl = e.target.result;
    uploadedImageB64 = dataUrl.split(",")[1];
    previewImg.src = dataUrl;
    uploadInner.classList.add("hidden");
    uploadPreview.classList.remove("hidden");
    analyzingBadge.classList.remove("hidden");
    detectedBadge.classList.add("hidden");
    await analyzeScreenshot(uploadedImageB64, uploadedMimeType);
  };
  reader.readAsDataURL(file);
}

async function analyzeScreenshot(b64, mimeType) {
  try {
    const result = await callORWithImage(b64, mimeType,
      `Analiza esta captura de pantalla de una conversación (WhatsApp, Instagram, iMessage, etc.).
Extrae:
1. El contexto: ¿qué le están pidiendo al usuario? ¿qué situación social hay?
2. La categoría: noshow (no querer quedar), cancel (cancelar plan acordado), work (no ir a trabajo/colegio)

Responde SOLO con JSON sin markdown:
{"situacion":"noshow|cancel|work","resumen":"una frase corta del contexto"}`
    );
    let parsed;
    try {
      parsed = JSON.parse(result.replace(/```json|```/g, "").trim());
    } catch {
      showDetectedBadge("⚠️ No se pudo leer el chat", "#666");
      return;
    }
    const sit = SITUATIONS.find(s => s.id === parsed.situacion);
    if (sit) {
      selectSituation(sit, true);
      if (parsed.resumen) contextInput.value = parsed.resumen;
      showDetectedBadge(`${sit.emoji} ${sit.label} detectado`, sit.color);
    } else {
      showDetectedBadge("⚠️ Situación no reconocida", "#666");
    }
  } catch {
    showDetectedBadge("⚠️ Error al analizar", "#666");
  } finally {
    analyzingBadge.classList.add("hidden");
  }
}

function showDetectedBadge(text, color) {
  detectedBadge.textContent = text;
  detectedBadge.style.color = color;
  detectedBadge.style.borderColor = color;
  detectedBadge.classList.remove("hidden");
}

function clearImage() {
  uploadedImageB64 = null;
  previewImg.src = "";
  uploadPreview.classList.add("hidden");
  uploadInner.classList.remove("hidden");
  analyzingBadge.classList.add("hidden");
  detectedBadge.classList.add("hidden");
  screenshotInput.value = "";
}

// ------------------------------------------------------------
// Generate
// ------------------------------------------------------------
generateBtn.addEventListener("click", generate);
retryBtn.addEventListener("click", generate);

async function generate() {
  if (!selectedSituation || !selectedUrgency) return;

  resultEl.classList.add("hidden");
  loadingEl.classList.remove("hidden");
  generateBtn.disabled = true;

  titleEl.classList.add("glitch");
  setTimeout(() => titleEl.classList.remove("glitch"), 500);

  document.querySelectorAll(".loading-line").forEach(el => {
    el.style.animation = "none";
    void el.offsetWidth;
    el.style.animation = "";
  });

  try {
    let excuse;
    if (uploadedImageB64) {
      excuse = await generateFromImage();
    } else {
      excuse = await callOR([{ role: "user", content: buildPrompt() }]);
    }
    displayResult(excuse);
  } catch (err) {
    displayResult(`⚠️ Error: ${err.message}\n\nRevisa la consola (F12) para más detalles.`);
  }

  loadingEl.classList.add("hidden");
  generateBtn.disabled = false;
}

async function generateFromImage() {
  const ctx = contextInput.value.trim();
  const prompt = `Eres un experto mundial en excusas sociales. Analiza esta captura de conversación y genera UNA excusa perfecta y creíble.

Situación: ${selectedSituation.label}
Urgencia: ${selectedUrgency.label}
${ctx ? `Contexto adicional: ${ctx}` : ""}

Responde SOLO con este formato:

🎭 EXCUSA:
[La excusa lista para usar, 2-4 frases, tono natural y coloquial, en español, adaptada a lo que ves en el chat]

💡 CONSEJO PRO:
[Un tip corto de cómo usarla teniendo en cuenta la conversación]

⚠️ NIVEL DE RIESGO: [Bajo / Medio / Alto] — [razón en 5 palabras]`;

  return callORWithImage(uploadedImageB64, uploadedMimeType, prompt);
}

function buildPrompt() {
  const ctx = contextInput.value.trim();
  const styles = [
    "médica o física (dolor, malestar, enfermedad)",
    "familiar o personal (problema en casa, familiar que necesita ayuda)",
    "técnica o logística (avería, incidencia, problema de transporte)",
    "emocional o psicológica (agotamiento, estrés, necesidad de descanso)",
    "imprevisto externo (algo inesperado que surgió de repente)",
  ];
  const randomStyle = styles[Math.floor(Math.random() * styles.length)];
  const seed = Math.floor(Math.random() * 99999);

  return `Eres un experto mundial en excusas sociales. Tu misión: generar UNA excusa perfecta, creíble y lista para copiar y pegar.

Situación: ${selectedSituation.label}
Urgencia: ${selectedUrgency.label}
Contexto adicional: ${ctx || "ninguno"}
Estilo de excusa: ${randomStyle}
Semilla de variedad: ${seed}

IMPORTANTE: Cada excusa debe ser completamente diferente a las anteriores. Varía el tipo de problema, los detalles concretos y el enfoque narrativo. Sé creativo e impredecible.

Responde SOLO con esto, sin comentarios ni explicaciones extra:

🎭 EXCUSA:
[La excusa lista para usar, en 2-4 frases máximo, en español, tono natural y coloquial]

💡 CONSEJO PRO:
[Un tip corto de cómo usarla bien]

⚠️ NIVEL DE RIESGO: [Bajo / Medio / Alto] — [razón en 5 palabras]`;
}

// ------------------------------------------------------------
// API — OpenRouter
// ------------------------------------------------------------
async function callOR(messages) {
  const res = await fetch(OR_URL, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "Authorization": `Bearer ${API_KEY}`,
    },
    body: JSON.stringify({ model: MODEL, max_tokens: 1000, messages }),
  });
  if (!res.ok) {
    const err = await res.json().catch(() => ({}));
    throw new Error(err.error?.message || `HTTP ${res.status}`);
  }
  const data = await res.json();
  return data.choices?.[0]?.message?.content || "Sin respuesta.";
}

async function callORWithImage(b64, mimeType, textPrompt) {
  const res = await fetch(OR_URL, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "Authorization": `Bearer ${API_KEY}`,
    },
    body: JSON.stringify({
      model: MODEL,
      max_tokens: 1000,
      messages: [{
        role: "user",
        content: [
          { type: "image_url", image_url: { url: `data:${mimeType};base64,${b64}` } },
          { type: "text", text: textPrompt }
        ]
      }],
    }),
  });
  if (!res.ok) {
    const err = await res.json().catch(() => ({}));
    throw new Error(err.error?.message || `HTTP ${res.status}`);
  }
  const data = await res.json();
  return data.choices?.[0]?.message?.content || "Sin respuesta.";
}

// ------------------------------------------------------------
// Display result
// ------------------------------------------------------------
function displayResult(text) {
  rawExcuse = text;
  resultBody.innerHTML = "";
  text.split("\n").forEach(line => {
    const div = document.createElement("div");
    div.className = /^(🎭|💡|⚠️)/.test(line) ? "line-header" : "line-content";
    div.textContent = line;
    resultBody.appendChild(div);
  });
  resultLabel.style.color = selectedSituation?.color || "var(--accent)";
  resultEl.classList.remove("hidden");
  resultEl.scrollIntoView({ behavior: "smooth", block: "start" });
}

// ------------------------------------------------------------
// Copy
// ------------------------------------------------------------
copyBtn.addEventListener("click", () => {
  const match = rawExcuse.match(/🎭 EXCUSA:\n([\s\S]*?)(?=\n💡|\n⚠️|$)/);
  const toCopy = match ? match[1].trim() : rawExcuse;
  navigator.clipboard.writeText(toCopy).then(() => {
    copyBtn.textContent = "✓ Copiado";
    copyBtn.classList.add("copied");
    setTimeout(() => {
      copyBtn.textContent = "Copiar";
      copyBtn.classList.remove("copied");
    }, 2000);
  });
});