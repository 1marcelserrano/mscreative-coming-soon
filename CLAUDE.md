# CLAUDE.md — mscreative-coming-soon

Landing page temporária da MSCREATIVE.SYSTEMS™ + assets de conteúdo (notas Obsidian e story cards).

## Design System (fonte da verdade)

O DS V3.0 vive em `index.html` (`:root` tokens). Paleta: fundo chumbo `#0A0C10`, texto sand `#B2A898`, ênfase electric orange `#A85A30`. Tipografia: IBM Plex Sans (300) + Libre Caslon Text (itálico, ênfases) + Space Mono (labels). Régua-assinatura em gradiente laranja→transparente. Radius 2px.

## Story cards (social, 9:16)

Quando o pedido for **"transformar X em stories / cards"**, seguir **`stories/STORYCARDS_SPEC.md`** — é a receita canônica. Resumo do que NÃO pode faltar:

- Slides 1080×1920 (`<section class="story">`), 7–9 no total, arco: capa/gancho → contexto → dados → comparação/quote → CTA.
- DS V3.0 (mesmos tokens do `index.html`) — editorial, NÃO neon. Ênfase com parcimônia (laranja + Libre Caslon itálico).
- Wordmark `MSCREATIVE.SYSTEMS™` no topo de cada slide.
- **Monograma oficial MS** (`<symbol id="ms-mono">`, `currentColor`) discreto no rodapé — usar o path oficial do spec, nunca reinventar.
- Export: Playwright/Chromium → `stories/export/story-NN.png` (1080×1920, dpr 1, esperar `document.fonts.ready`).
- Fonte de conteúdo: se o egress bloquear o domínio, pedir o texto colado; nunca inventar números. Sempre creditar a fonte.

Entregáveis: `stories/<slug>-stories.html` + PNGs em `stories/export/` (+ nota Obsidian em `notes/` quando fizer sentido).

## Git

Trabalhar na branch indicada; commit + push; abrir PR draft. Deploy automático via Vercel a cada push.
