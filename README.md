# mscreative-coming-soon

Landing page temporária — MSCREATIVE.SYSTEMS™.

Single-file HTML, zero build, zero dependência. Vive até o site oficial subir.

---

## Stack

- HTML/CSS/JS estático (single-file)
- Hospedagem: Vercel (auto-deploy via GitHub)
- Domínio: `mscreative.systems` (DNS no GoDaddy)
- Captura de email: ConvertKit (Kit)
- Fonts: Inter + Space Mono (Google Fonts CDN)

---

## Setup — passo a passo

### 1. GitHub

```bash
cd mscreative-coming-soon
git init
git add .
git commit -m "init: LP temporária"
git branch -M main
# criar repo vazio em github.com/seu-user/mscreative-coming-soon (sem README)
git remote add origin git@github.com:SEU-USER/mscreative-coming-soon.git
git push -u origin main
```

### 2. Vercel

1. Acessar [vercel.com/new](https://vercel.com/new)
2. **Import Git Repository** → selecionar `mscreative-coming-soon`
3. Framework Preset: `Other` (Vercel detecta HTML estático automaticamente)
4. Root directory: `./` (default)
5. Clicar **Deploy**

A primeira URL sai em ~30s no formato `mscreative-coming-soon-xxx.vercel.app`. Testa antes de apontar o domínio.

### 3. Domínio custom (mscreative.systems)

**No Vercel:**

1. Project → **Settings** → **Domains**
2. Add `mscreative.systems` e `www.mscreative.systems`
3. Vercel mostra os DNS records necessários (geralmente um A record e um CNAME)

**No GoDaddy:**

1. Domínios → `mscreative.systems` → **DNS**
2. Editar/adicionar conforme o Vercel pediu. Padrão atual:
   - `A` record: Host `@`, Value `76.76.21.21`
   - `CNAME` record: Host `www`, Value `cname.vercel-dns.com`
3. TTL: 600s (ou default)
4. Salvar

Propagação DNS: 5min a 24h (geralmente <1h). SSL provisionado automaticamente pelo Vercel.

### 4. ConvertKit (Kit) — form de captura

1. [app.kit.com](https://app.kit.com) → **Grow** → **Landing Pages & Forms** → **+ Create new**
2. Escolher **Form** → **Inline**
3. Configurar (campo email só, opt-in opcional, sem double opt-in se quiser conversão direta)
4. Save → **Embed** → aba **HTML**
5. Localizar a linha `<form action="https://app.kit.com/forms/XXXXXX/subscriptions" ...>`
6. Copiar o número `XXXXXX` (FORM_ID)
7. Abrir `index.html` neste repo, localizar `REPLACE_WITH_FORM_ID` (linha ~190 aproximadamente, dentro do `<form action=...>`)
8. Substituir pelo FORM_ID. Commit e push — Vercel re-deploya em ~20s.

**Verificação:** abre a LP no navegador, submete um email teste, confirma que aparece em **Subscribers** no Kit.

---

## Microcopy do bloco do form

O `index.html` tem 1 microcopy default ativa. As outras 2 opções estão comentadas no final deste README. Para trocar, edita a linha marcada `<!-- MICROCOPY: ... -->` em `index.html`.

### Opção 1 (ativa) — Direta/promessa

```
O site oficial chega em breve. Quem entra na lista recebe primeiro:
ensaios, demonstrações e o processo público da infraestrutura sendo montada.
```
Micro: `Sem spam. Só quando vale seu tempo.`

### Opção 2 — Filtragem por afinidade

```
A lista é pra quem prefere acompanhar o sistema sendo construído
em vez de receber o produto pronto. Bastidor, ensaios, prova de conceito.
```
Micro: `Sem newsletter genérica. Sem promessa de virar guru.`

### Opção 3 — Marcel-pessoa

```
Enquanto o site oficial não está pronto, o trabalho continua à vista.
Quem entra recebe o que estou construindo enquanto construo.
```
Micro: `Sem spam. Sem performance. Só o que vale a leitura.`

---

## Estrutura

```
mscreative-coming-soon/
├── index.html       ← página completa (HTML + CSS + form)
├── vercel.json      ← config de headers e cache
├── .gitignore
└── README.md        ← este arquivo
```

---

## Deploy de uma alteração

Qualquer push pra `main` re-deploya automaticamente:

```bash
git add .
git commit -m "fix: troca microcopy"
git push
```

Vercel constrói e publica em ~20s.

---

## Quando o site oficial ficar pronto

Duas opções:

1. **Trocar o deploy do mesmo domínio:** No Vercel, mover o domínio `mscreative.systems` do project `mscreative-coming-soon` pro project do site oficial.
2. **Arquivar este repo:** GitHub → Settings → Archive. Mantém histórico, impede commits.

---

## Notas técnicas

- Fonts servidos via Google Fonts CDN — sem self-hosting (LP temporária, otimização não compensa).
- Sem analytics (Marcel decide depois — Plausible/Umami se quiser, ou Vercel Analytics nativo).
- Sem CSP estrita por enquanto (form ConvertKit precisa de domínio externo). Adicionar quando o site oficial subir.
- Form posta direto pro Kit via action HTML padrão — não exige JS. Se Kit retornar erro, o usuário vê página padrão do Kit; se quiser tela custom de confirmação, configurar no próprio Kit (Settings → Incentive/Thank-you page).
