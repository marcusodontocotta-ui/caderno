# 📓 Caderno de Estudos

Aplicativo web de caderno para estudantes, em **arquivo único** (`index.html`) + dados bíblicos
locais. Funciona totalmente **sem backend** e pode ser publicado como site estático gratuito.

## Recursos

- **Layout 50/50 ou tela cheia** — o painel de consulta (anexos ou Bíblia) pode ser dividido
  50/50 com o editor ou expandido para a tela toda (botão `⛶ Tela cheia` / `⊞ 50/50`).
- **Abas no painel de consulta**: `📎 Anexos` e `📖 Bíblia`.
- **Editor de texto rico** — negrito, itálico, sublinhado, tamanho da fonte.
- **Anexos PDF e fotos** — upload ou **captura da câmera**, com **desenho/anotação livre** por cima
  (cor e espessura ajustáveis) e limpar desenho.
- **Bíblia consultável embutida (offline)** — dados locais incluídos no site:
  - **Português** — Almeida (Bíblia Livre, domínio público)
  - **Inglês** — King James (KJV), World English (WEB), American Standard (ASV)
  - **Hebraico original** — Westminster Leningrad Codex (com pontos vocálicos), séries só AT
  - Navegação por livro/capítulo, fonte ajustável, e botão copiar.
- **Páginas e múltiplos cadernos** — navegue e exporte o texto da página como `.txt`.
- **Persistência local** — tudo salvo no navegador (`localStorage`).

## Rodar localmente

Abra direto pelo arquivo (funciona Anexos/Bíblia), ou sirva com HTTP para habilitar a câmera:

```
# opção A: servidor simples
npx serve .
# ou já está rodando em http://localhost:3000

# opção B: basta abrir o arquivo
start index.html
```

> **Importante**: o modo `file://` (abrir o arquivo) funciona para anexos e Bíblia, mas a
> **captura de câmera** exige `https://` ou `localhost`. Os dados da Bíblia são carregados por
> `fetch`, então **servir via HTTP** (`npx serve` / `localhost:3000`) é o caminho recomendado.

## Dados da Bíblia (licenças)

Os textos são de **domínio público / distribuição livre**, baixados do projeto
[`midvash/bible-data`](https://github.com/midvash/bible-data) (esquema OSIS, livro por livro):
- `pt/almeida-livre` — Almeida 1819 / "Bíblia Livre" (domínio público)
- `en/kjv` — King James Version 1769 (domínio público)
- `en/web` — World English Bible (domínio público)
- `en/asv` — American Standard Version 1901 (domínio público)
- `he/wlc` — Westminster Leningrad Codex (AT hebraico, com nikkud)
- `he/aleppo` — Aleppo Codex (AT hebraico)

O app carrega **um livro por vez** sob demanda (fetch), mantendo o site leve.

## Deploy no GitHub

```bash
git init
git add .
git commit -m "Caderno de Estudos - v1"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/caderno-estudos.git
git push -u origin main
```

## Deploy no Render (Free Static Site)

O site é 100% estático — **não precisa de build**:

1. Acesse https://render.com → **New** → **Static Site**.
2. Conecte o repositório GitHub do projeto.
3. Configuração:
   - **Build Command**: `#` (vazio — nada a compilar)
   - **Publish Directory**: `.` (raiz)
4. **Create Static Site**. O Render gera a URL pública (ex.: `https://caderno-estudos.onrender.com`).

> O Render entrega via **HTTPS**, então a câmera e tudo mais funcionam no celular/dispositivos.

## Estrutura

```
caderno-estudos/
  index.html            # App completo (HTML + Tailwind CDN + JS)
  README.md
  data/
    biblia/
      pt/almeida-livre/books/*.json
      en/{kjv,web,asv}/books/*.json
      he/{wlc,aleppo}/books/*.json
```

Tecnologia: HTML5 · Tailwind CSS (CDN) · JavaScript puro · PDF.js (CDN) · dados bíblicos locais.
