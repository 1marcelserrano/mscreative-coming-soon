# Story Cards — MSCREATIVE.SYSTEMS™ (DS V3.0)

Spec reutilizável para transformar um artigo/relatório em um deck de **stories verticais 9:16** (social cards) no design system da MSCREATIVE.SYSTEMS™. Seguir isto reproduz o look-and-feel do deck `bcg-ai-at-work-2026-stories.html`.

---

## 1. Formato & estrutura

- **Dimensão:** 1080×1920 px (9:16). Cada slide é uma `<section class="story">`.
- **Quantidade:** 7–9 slides. Arco narrativo padrão:
  1. **Capa / gancho** — headline editorial (sand) + ênfase em Libre Caslon itálico laranja. Ex.: "A IA já chegou. *A gestão, não.*"
  2. **Contexto / o estudo** — fonte, amostra, credibilidade (linhas de dados `.rows`).
  3–N. **Slides de dado** — 1 número-herói por slide (`.figure`) OU listas `.rows`.
  - **Comparação** — dois cards `.vs` (lead-card com borda-topo laranja vs. card neutro).
  - **Pull quote** — citação em Libre Caslon itálico (`.quote`), com palavra-chave em laranja.
  N. **CTA / pra levar** — lista numerada `ol.q` (3 perguntas/ações) + tagline da marca.
- **Tom:** editorial, confiante, PT-BR. Ênfase é cara — usar laranja + itálico serif com parcimônia (1 ponto focal por slide).

## 2. Design System V3.0 (tokens — idênticos ao `index.html`)

```css
--ds-bg:#0A0C10; --ds-bg-secondary:#12141A; --ds-surface:#1A1D26;
--ds-text:#B2A898;                 /* warm oxidized sand (texto primário) */
--ds-text-body:rgba(178,168,152,0.85); --ds-text-muted:rgba(178,168,152,0.5);
--ds-text-strong:#FFFFFF;
--ds-border-subtle:rgba(255,255,255,0.06); --ds-grid:rgba(255,255,255,0.025);
--ds-headline:#6A6A6A; --ds-emphasis:#A85A30;  /* electric orange */ --ds-emphasis-2:#6A3818;
--p-rule:linear-gradient(90deg,#A85A30 0%,#6A3818 50%,transparent 100%); /* régua-assinatura */
--radius:2px;
```

**Tipografia (Google Fonts):**
- `IBM Plex Sans` peso **300** → headlines, números, corpo.
- `Libre Caslon Text` **itálico** → ênfases/citações (cor laranja).
- `Space Mono` → labels, eyebrows, rodapés, numeração (uppercase, `letter-spacing:.18em`).

**Texturas de fundo:** grid editorial sutil (`--ds-grid`, `background-size:120px`) + vinheta quente no topo-direito (`radial-gradient(...rgba(168,90,48,.10)...)`).

## 3. Componentes (classes canônicas)

- `.head` → topbar: `.brand` `MSCREATIVE.SYSTEMS™` (esq.) + `.eyebrow` (seção, dir.).
- `.kicker` (Space Mono, laranja ou `.muted`) → eyebrow do conteúdo.
- `h1` / `h2` (IBM Plex 300, sand) com `.accent` / `<em>` em Libre Caslon itálico laranja.
- `.rule` → divisor em gradiente (assinatura visual).
- `.figure` (300px) com `.u` no sufixo (% / unidade) em laranja; `.fig-label`, `.fig-sub`.
- `.rows` › `.row` (`.n` número + `.t` texto) — dados em lista com bordas finas.
- `.vs` › `.card` (`.lead-card` = destaque com `border-top` laranja); `.big`, `.cap`.
- `.quote` (Libre Caslon itálico) + `.byline` (Space Mono).
- `ol.q` → lista numerada (numeração `decimal-leading-zero` em laranja).
- `.foot` → `.src` (fonte, Space Mono muted) + `.pageno` (NN / NN) + **monograma**.

## 4. Marca

- **Wordmark** `MSCREATIVE.SYSTEMS™` no `.head` de TODO slide (com `<sup>™</sup>`).
- **Monograma oficial MS** como `<symbol id="ms-mono">` reutilizável, `fill="currentColor"` (herda cor/opacidade discretas). Usar `.mono` (rodapé, 54px, opacity .65) e `.mono.lg` (capa/CTA, 66px, opacity .8). **Não** reinventar o monograma — usar o path oficial:

```html
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <symbol id="ms-mono" viewBox="0 0 67.19667 51.75458">
    <path fill="currentColor" d="M8.15479,17.66986c-.10727,4.76875.03115,9.5285.41527,14.27922.25365,3.1651,1.03955,6.29608,1.74645,9.47888C12.17932,49.84272-.28837,51.03399.0051,42.2846c.35921-10.7694,2.02753-21.07894,5.00492-30.92856.43105-1.41773,1.65413-3.47677,3.2464-2.21435.53746.42306.92911.9969,1.17496,1.72154l5.78538,16.91602c.23584.68769.41046.67353.52387-.04254,1.02383-6.35386,2.74577-12.56867,5.16579-18.64433,2.42341-6.08573,7.57839-4.14271,9.40284.91599,2.77922,7.71993,3.71882,15.26481,4.54493,24.0988.01976.18583.11541.20673.28695.06271,5.16382-4.20649,10.48613-8.20113,15.96693-11.98388.2477-.17071.22158-.25977-.07835-.26709-3.61598-.09368-7.23981-.18066-10.87148-.26095-7.39821-.16475-4.36055-6.1619-1.09576-9.14847,3.1263-2.86316,6.25148-5.72857,9.37556-8.59623,1.40786-1.29146,2.61261-3.41267,5.0914-3.82386,5.89972-.9766,7.89921,6.29685,3.23346,9.68677-3.83797,2.79228-7.80539,5.39743-11.90226,7.81541-.15464.09367-.14189.15021.03827.16962,3.88277.43335,7.73249.3423,11.54916-.27318,2.22015-.35804,3.71273-2.03541,5.76647-2.29809,3.64903-.46082,6.04224,3.15361,4.51287,6.37544-.40245.85424-1.13742,1.76487-2.20492,2.73191-9.11467,8.26941-20.20634,14.6041-28.33323,22.56665-1.08504,1.06379-2.30373,3.42673-3.57933,4.09058-4.6234,2.39615-8.52986-.9142-8.76183-5.62878-.18359-3.7576-1.48526-26.94142-1.86815-26.88513-.09989.01549-.20829.14727-.27434.33352-1.46726,4.3048-2.51335,8.71175-3.13827,13.2209-.12499.90632-.43616,1.72773-.9335,2.46426-1.56103,2.29841-3.54903-.8048-4.06681-2.08179-2.07112-5.11908-3.79413-9.98508-5.16903-14.59797-.02544-.08589-.07445-.14821-.12558-.15976l-.05874-.0085c-.02576-.00602-.05156.01476-.05761.04636-.00077.00405-.00119.00814-.00126.01226Z"/>
  </symbol>
</svg>
```
> Fonte do vetor: Google Drive → `MS CREATIVE SYSTEMS/_MS BRAND/logo/monogram.svg`.

## 5. Pipeline de export (PNG)

Renderizar cada `.story` como PNG 1080×1920 com Playwright/Chromium:
- `viewport: { width:1080, height:1920 }`, `deviceScaleFactor:1`
- `goto(file://…, { waitUntil:'networkidle' })` → `await page.evaluate(() => document.fonts.ready)` → pequeno `waitForTimeout`
- `for (const s of await page.$$('.story')) await s.screenshot({ path: 'stories/export/story-NN.png' })`
- Saída: `stories/export/story-01.png … story-NN.png`.
- Fontes vêm do Google Fonts via `<link>` — exigem rede no momento do render.

## 6. Conteúdo / fontes

- Web egress pode bloquear o domínio da fonte (403 "Host not in allowlist"). Quando isso ocorrer, pedir ao usuário o **texto integral colado** e extrair os dados dali — não inventar números.
- Sempre creditar a fonte original no `.foot .src` e (se aplicável) na nota Obsidian companheira.

## 7. Entregáveis padrão

1. `stories/<slug>-stories.html` — deck editável (HTML único, self-contained).
2. `stories/export/story-01..NN.png` — imagens prontas pra postar.
3. (opcional) nota Obsidian em `notes/` com o conteúdo-fonte.
