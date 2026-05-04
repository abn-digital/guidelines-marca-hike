# Hike Design System

> Referencia de diseño para todos los proyectos de Hike. Copiá de acá para mantener consistencia visual entre apps, decks y materiales.

---

## Tabla de contenidos

1. [Filosofía](#filosofía)
2. [Tipografía](#tipografía)
3. [Paleta de colores](#paleta-de-colores)
4. [Variables CSS](#variables-css)
5. [Espaciado y layout](#espaciado-y-layout)
6. [Componentes: patrones recurrentes](#componentes-patrones-recurrentes)
7. [Animaciones](#animaciones)
8. [Assets](#assets)
9. [Setup mínimo](#setup-mínimo)

---

## Filosofía

El estilo de Hike se puede resumir en tres palabras: **limpio, denso, premium**.

- **Limpio**: mucho espacio en blanco, jerarquía clara, sin ruido visual.
- **Denso**: la información tiene peso. No decoramos por decorar.
- **Premium**: cada detalle importa — tipografía fina, colores curados, micro-animaciones sutiles.

El resultado visual tiene que transmitir que Hike opera en el mundo enterprise, no en el mundo startup-colorido.

---

## Tipografía

**Fuente principal**: [Inter](https://fonts.google.com/specimen/Inter) — Google Fonts.

```html
<!-- En el <head> -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
```

```css
/* CSS */
font-family: 'Inter', system-ui, sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
```

### Escala tipográfica

| Uso | Tamaño | Peso | Extras |
|---|---|---|---|
| Hero H1 | `4xl–7xl` (fluid) | `font-light` (300) | `tracking-tight`, `leading-[1.1]` |
| Section H2 | `3xl–6xl` | `font-light` (300) | `tracking-tight` |
| Card H3 | `base–lg` | `font-semibold` (600) | `tracking-tight`, `leading-snug` |
| Body principal | `base` | `font-light` (300) | `leading-relaxed` |
| Body secundario | `sm` | `font-light` (300) | `leading-relaxed` |
| Labels/eyebrow | `[10px]–[11px]` | `font-bold` (700) | `tracking-[0.2em]–[0.25em]` `uppercase` |
| Monospace/fuentes | `xs` | `font-mono` | `tracking-widest` `uppercase` |

### Patrones de headline

```jsx
// Headline principal (hero) — siempre font-light con span semibold italic
<h1 className="text-4xl md:text-6xl xl:text-7xl font-light tracking-tight text-[#1A1420] leading-tight">
  La IA ya llegó a tu empresa.{" "}
  <span className="font-semibold text-[#2D1B4E] italic">Ahora hay que hacerla funcionar.</span>
</h1>

// Headline en fondo oscuro — con acento amarillo
<h2 className="text-4xl md:text-6xl font-light tracking-tight text-white leading-[1.1]">
  Identificá dónde está{" "}
  <span className="italic text-[#F4EB33]">el mayor impacto.</span>
</h2>

// Eyebrow label — siempre en mayúsculas, letra chica, peso bold
<p className="text-[10px] font-bold tracking-[0.25em] uppercase text-[#9E97A5]">
  La pregunta que pocos se hacen
</p>
```

---

## Paleta de colores

### Colores base

| Token | Hex | Uso |
|---|---|---|
| `--bg` | `#FCF9F7` | Background general — warm off-white |
| `--surface` | `#FFFFFF` | Cards, modales, superficies elevadas |
| `--surface-2` | `#F7F4F1` | Cards levemente más cálidas |
| `--dark` | `#1A0A2E` | CTA sections, footer, slides oscuros |

### Colores de acento (morado)

| Token | Hex | Uso |
|---|---|---|
| `--accent` | `#7E6E94` | Borders, labels, separadores suaves |
| `--accent-dark` | `#2D1B4E` | Headlines, botones, elementos focales |
| `--accent-deep` | `#5E5070` | Hover entre `--accent` y `--accent-dark` |
| `--accent-light` | `rgba(126,110,148,0.08)` | Backgrounds de hover muy sutil |
| `--accent-border` | `rgba(126,110,148,0.18)` | Borders suaves sobre fondo claro |

### Amarillo (sólo en fondo oscuro)

| Token | Hex | Regla |
|---|---|---|
| `--yellow` | `#F4EB33` | ⚠️ Usar SOLO sobre `#1A0A2E` o `#1A0F30`. Nunca sobre blanco. |

```jsx
// ✅ Correcto — amarillo sobre fondo oscuro
<div className="bg-[#1A0A2E]">
  <span className="text-[#F4EB33]">El mayor impacto.</span>
</div>

// ❌ Incorrecto — amarillo sobre blanco
<div className="bg-white">
  <span className="text-[#F4EB33]">...</span>
</div>
```

### Texto

| Token | Hex | Uso |
|---|---|---|
| `--text` | `#1A1420` | Texto principal — near-black con warmth |
| `--text-2` | `#6B6272` | Texto secundario, subtítulos |
| `--text-3` | `#9E97A5` | Texto terciario, labels, placeholders |

### Borders

| Token | Valor | Uso |
|---|---|---|
| `--border` | `rgba(26,20,32,0.07)` | Borde muy sutil (default) |
| `--border-md` | `rgba(26,20,32,0.13)` | Borde visible en hover |

---

## Variables CSS

Copiar exactamente en `globals.css` de cada proyecto:

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&display=swap');

:root {
  /* Brand palette */
  --bg:           #FCF9F7;   /* Hike warm off-white */
  --surface:      #FFFFFF;
  --surface-2:    #F7F4F1;   /* slightly warmer card bg */
  --dark:         #1A0A2E;   /* dark navy for CTA/footer */
  --accent:       #7E6E94;   /* Hike mauve — labels, borders, soft accents */
  --accent-dark:  #2D1B4E;   /* deep mauve — headlines, buttons, focal points */
  --accent-deep:  #5E5070;   /* hover between the two */
  --accent-light: rgba(126,110,148,0.08);
  --accent-border: rgba(126,110,148,0.18);
  --yellow:       #F4EB33;   /* accent only on dark bg */

  /* Text */
  --text:         #1A1420;   /* near-black with warmth */
  --text-2:       #6B6272;   /* warm gray, secondary */
  --text-3:       #9E97A5;   /* tertiary / labels */

  /* Borders */
  --border:       rgba(26,20,32,0.07);
  --border-md:    rgba(26,20,32,0.13);
}

* { box-sizing: border-box; }

html {
  scroll-behavior: smooth;
  scrollbar-width: thin;
  scrollbar-color: rgba(126,110,148,0.2) transparent;
}

::-webkit-scrollbar { width: 4px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb {
  background: rgba(126,110,148,0.25);
  border-radius: 2px;
}

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'Inter', system-ui, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  line-height: 1.6;
}

::selection {
  background: rgba(126,110,148,0.15);
  color: var(--accent-deep);
}
```

---

## Espaciado y layout

### Contenedor máximo

```jsx
// Siempre max-w-5xl o max-w-6xl, centrado, con padding lateral
<div className="max-w-5xl mx-auto px-6">
  ...
</div>
```

### Padding de secciones

| Sección | Padding vertical |
|---|---|
| Secciones estándar | `py-20` – `py-28` |
| CTA / footer hero | `py-24` |
| Navbar | `py-4` (scrolled: `py-3`) |

### Grid de cards

```jsx
// 3 columnas en desktop, 1 en mobile
<div className="grid grid-cols-1 md:grid-cols-3 gap-4">
  ...
</div>

// 2 columnas en desktop
<div className="flex flex-col lg:flex-row items-start gap-12 lg:gap-24">
  ...
</div>
```

---

## Componentes: patrones recurrentes

### Eyebrow label (pill con punto)

```jsx
// Sobre fondo claro
<div className="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-white border border-black/8 mb-10">
  <div className="w-1.5 h-1.5 rounded-full bg-[#2D1B4E]" />
  <span className="text-[#6B6272] text-[11px] font-semibold tracking-widest uppercase">El Desafío</span>
</div>

// Sobre fondo oscuro (con guiones y amarillo)
<div className="inline-flex items-center gap-3 mb-10">
  <div className="h-px w-10 bg-[#F4EB33]/40" />
  <span className="text-[#F4EB33] text-[10px] font-bold tracking-[0.25em] uppercase">Próximo paso</span>
  <div className="h-px w-10 bg-[#F4EB33]/40" />
</div>
```

### Cards sobre fondo claro

```jsx
// Card estándar
<div className="border rounded-2xl p-7 bg-white border-black/6 hover:border-black/12 hover:shadow-md transition-all duration-300">
  <div className="text-[10px] font-bold tracking-widest uppercase text-[#9E97A5]">01</div>
  <h3 className="text-base font-semibold tracking-tight leading-snug text-[#1A1420]">Título</h3>
  <p className="text-sm font-light leading-relaxed text-[#6B6272]">Body text aquí.</p>
  <p className="text-sm font-semibold mt-auto pt-3 border-t border-black/6 text-[#2D1B4E]">Bold closing statement.</p>
</div>

// Card destacada (inverted — dark bg)
<div className="border rounded-2xl p-7 bg-[#2D1B4E] border-[#2D1B4E]">
  <div className="text-[10px] font-bold tracking-widest uppercase text-white/30">03</div>
  <h3 className="text-base font-semibold tracking-tight leading-snug text-white">Título</h3>
  <p className="text-sm font-light leading-relaxed text-white/60">Body text aquí.</p>
  <p className="text-sm font-semibold mt-auto pt-3 border-t border-white/10 text-[#F4EB33]">Bold closing statement.</p>
</div>
```

### Separador decorativo (divider con texto)

```jsx
<div className="flex items-center gap-4">
  <div className="h-px flex-1 bg-white/10" />
  <span className="text-[10px] font-bold tracking-[0.2em] uppercase text-white/20">
    Texto del separador
  </span>
  <div className="h-px flex-1 bg-white/10" />
</div>
```

### CTA Button — primario (sobre fondo oscuro)

```jsx
<a
  href="https://..."
  className="inline-flex items-center gap-2 px-10 py-5 rounded-full bg-[#F4EB33] text-[#1A0A2E] text-base font-bold hover:brightness-105 transition-all shadow-xl"
>
  Agendar diagnóstico ↗
</a>
```

### CTA Button — outline (Navbar)

```jsx
// Versión scrolled (sobre fondo blanco)
<button className="text-[10px] uppercase tracking-[0.2em] font-bold px-6 py-2 rounded-full border border-black/10 text-black hover:bg-black hover:text-white transition-all duration-500">
  Hablemos
</button>

// Versión hero (sobre fondo oscuro)
<button className="text-[10px] uppercase tracking-[0.2em] font-bold px-6 py-2 rounded-full border border-white/10 text-white hover:bg-white hover:text-black transition-all duration-500">
  Hablemos
</button>
```

### Navbar link

```jsx
// Texto de nav — siempre tiny, uppercase, muy espaciado
<button className="text-[10px] uppercase tracking-[0.2em] font-medium transition-all duration-500 text-black/60 hover:text-black">
  Sección
</button>
```

### Sección oscura (dark section)

```jsx
<section className="relative bg-[#1A0A2E] py-20 px-6">
  {/* Accent top line — siempre en footer/CTA */}
  <div className="h-[3px] w-full bg-[#F4EB33]" />

  {/* Blur accents de fondo */}
  <div className="absolute inset-0 pointer-events-none">
    <div className="absolute -bottom-32 -right-32 w-96 h-96 rounded-full bg-[#F4EB33]/[0.04] blur-3xl" />
    <div className="absolute -top-32 -left-32 w-96 h-96 rounded-full bg-white/[0.02] blur-3xl" />
  </div>

  {/* Content */}
  <div className="relative ...">
    ...
  </div>
</section>
```

### Variante oscura más densa (slides / PreAI)

```jsx
// Para secciones más azuladas/violáceas (no puro navy)
<section className="bg-[#1A0F30]">
  <div className="absolute top-0 right-0 w-[40%] h-full bg-gradient-to-l from-white/[0.02] to-transparent" />
  <div className="absolute bottom-0 left-0 w-64 h-64 rounded-full bg-[#F4EB33]/[0.03] blur-3xl" />
</section>
```

---

## Animaciones

Usamos **Framer Motion**. Los patrones estándar:

### Fade in al entrar en viewport

```jsx
import { motion } from "framer-motion";

<motion.div
  initial={{ opacity: 0, y: 16 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true }}
  transition={{ duration: 0.6 }}
>
  ...
</motion.div>
```

### Stagger de cards (múltiples elementos)

```jsx
{items.map((item, i) => (
  <motion.div
    key={i}
    initial={{ opacity: 0, y: 16 }}
    whileInView={{ opacity: 1, y: 0 }}
    viewport={{ once: true }}
    transition={{ delay: i * 0.1, duration: 0.6 }}
  >
    ...
  </motion.div>
))}
```

### Entry de elementos en slides (sin scroll trigger)

```jsx
<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.7 }}
>
  ...
</motion.div>
```

### Navbar entry

```jsx
<motion.nav
  initial={{ y: -100, opacity: 0 }}
  animate={{ y: 0, opacity: 1 }}
  transition={{ duration: 0.8, ease: [0.16, 1, 0.3, 1] }}
>
  ...
</motion.nav>
```

### Transición entre slides (slide lateral)

```jsx
const variants = {
  enter: (d: number) => ({ opacity: 0, x: d > 0 ? 80 : -80 }),
  center: { opacity: 1, x: 0 },
  exit:  (d: number) => ({ opacity: 0, x: d > 0 ? -80 : 80 }),
};

// transition={{ duration: 0.4, ease: [0.25, 1, 0.5, 1] }}
```

### Easing curves de Hike

```js
// Entry rápido (spring-like)
ease: [0.16, 1, 0.3, 1]

// Slide lateral
ease: [0.25, 1, 0.5, 1]

// Duración estándar de elementos
duration: 0.6 – 0.7

// Duración de navbars / UI chrome
duration: 0.4 – 0.5
```

---

## Assets

### Logos oficiales

| Variante | URL | Cuándo usarla |
|---|---|---|
| **Mauve** (violeta) | `https://storage.googleapis.com/abn-assets/hike_logo_violeta_1080x1080.png` | Sobre fondos claros (`#FCF9F7`, `#FFFFFF`) |
| **Blanco** | `https://storage.googleapis.com/abn-assets/hike_logo_blanco_1080x1080.png` | Sobre fondos oscuros (`#1A0A2E`, `#1A0F30`, `#0D0815`) |

> **Regla simple**: fondo claro → logo mauve. Fondo oscuro → logo blanco. Nunca usar CSS `brightness-0 invert` como sustituto — usar el archivo correcto.

```jsx
// ✅ Logo sobre fondo claro
<div className="w-10 h-10 relative">
  <Image
    src="https://storage.googleapis.com/abn-assets/hike_logo_violeta_1080x1080.png"
    alt="Hike"
    fill
    className="object-contain"
  />
</div>

// ✅ Logo sobre fondo oscuro
<div className="w-10 h-10 relative">
  <Image
    src="https://storage.googleapis.com/abn-assets/hike_logo_blanco_1080x1080.png"
    alt="Hike"
    fill
    className="object-contain"
  />
</div>
```

---

## Setup mínimo

Para un proyecto nuevo que use el sistema de Hike:

### 1. Dependencias

```bash
npm install framer-motion lucide-react
```

### 2. globals.css

Copiar las [Variables CSS](#variables-css) de arriba.

### 3. Estructura recomendada de sección

```tsx
// Plantilla de sección estándar
export default function MiSeccion() {
  return (
    <section className="relative z-20 py-24 px-6 bg-[var(--bg)]">
      <div className="max-w-5xl mx-auto">
        {/* Eyebrow */}
        <div className="text-center mb-16">
          <div className="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-white border border-black/8 mb-10">
            <div className="w-1.5 h-1.5 rounded-full bg-[#2D1B4E]" />
            <span className="text-[#6B6272] text-[11px] font-semibold tracking-widest uppercase">Eyebrow Label</span>
          </div>
          <h2 className="text-4xl md:text-5xl font-light tracking-tight text-[#1A1420] leading-tight">
            Título principal con{" "}
            <span className="font-semibold text-[#2D1B4E]">acento.</span>
          </h2>
          <p className="mt-5 text-[#6B6272] font-light text-base max-w-xl mx-auto leading-relaxed">
            Descripción secundaria.
          </p>
        </div>

        {/* Cards u otros elementos */}
        <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
          ...
        </div>
      </div>
    </section>
  );
}
```

---

*Última actualización: Mayo 2026 — sincronizado con el Deck en `/Deck/src/app/globals.css`*
