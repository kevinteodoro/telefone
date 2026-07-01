# telefone.wiki.br — Telefones Operadoras Brasil

Site estático (HTML/CSS/JS vanilla) com os canais de atendimento (telefone, SAC, ouvidoria, chat, app) das principais empresas e órgãos do Brasil. Publicado via GitHub Pages no domínio **telefone.wiki.br** (arquivo `CNAME`).

## Estrutura

- **21 páginas de conteúdo** — uma por entidade real:
  - Telecom/Internet/TV: `telefone-claro`, `telefone-tim`, `telefone-oi`, `telefone-vivo`, `telefone-net`, `telefone-sky`
  - Streaming: `telefone-netflix`
  - Bancos: `telefone-nubank`, `telefone-bradesco`, `telefone-santander`, `telefone-itau`, `telefone-caixa-economica-federal-sac`, `banco-inter-telefone-sac`
  - Compras/Entregas: `telefone-amazon-contato`, `mercado-livre-sac`, `sac-magazine-luiza`, `telefone-jadlog`, `telefone-total-express-sac`, `telefone-correios`
  - Governo: `telefone-inss`, `telefone-receita-federal`
- **Institucionais**: `sobre/`, `contato/`, `politica-de-privacidade/`, `termos-de-uso/`
- **Home**: `index.html` — **Total no `sitemap.xml`: 26 URLs**
- **21 stubs de redirect** — slugs antigos consolidados (ex.: `ouvidoria-claro/`, `telefone-tim-sac/`) que redirecionam para a página-mãe. Ficam **fora** do sitemap (`noindex`).
- Infra: `ads.txt`, `robots.txt`, `sitemap.xml`, `404.html`, `assets/`.

## Monetização (Google AdSense)

- Publisher ID: `ca-pub-7989576624887637` (snippet em toda página de conteúdo, após o GTM).
- `ads.txt`: `google.com, pub-7989576624887637, DIRECT, f08c47fec0942fa0`.
- GTM: `GTM-NLMC2HLF`.

## Regras editoriais (ver `AI_CONTEXT.md`)

- **Uma página por entidade** — não duplicar variantes da mesma marca (evita *scaled content abuse*).
- **Páginas legais obrigatórias** linkadas no footer de todas as páginas.
- **E-E-A-T honesto**: sem processos de verificação inventados, sem métricas fabricadas; cada número com disclaimer + link à fonte oficial.
- **ANATEL** só para telecom; demais → `consumidor.gov.br`, Procon, Reclame Aqui; bancos → Banco Central; órgãos públicos → Fala.BR.
- Sem links internos quebrados.

## Auditoria / validação

Agentes usados no fluxo de qualidade:
- `seo-auditor` / `aeo-auditor` — checa canonical, GTM+AdSense, H1 único, sitemap, órfãs, ano ≥ 2026, FAQ em `<details>`.
- `algoritmo-google` — avalia se o conteúdo é rankeável (alvo: sair de IRRELEVANTE, nota ≥ 80).

Checagens rápidas de integridade (rodar na raiz do projeto):

```bash
# páginas com GTM + AdSense + 1 H1 + canonical; sitemap sem URL morta; stubs válidos
python3 - <<'PY'
import re,glob,os
for f in glob.glob('*/index.html')+['index.html']:
    h=open(f,encoding='utf-8').read()
    assert 'GTM-NLMC2HLF' in h and 'rel="canonical"' in h, f
print('OK')
PY
```

## Deploy

GitHub Pages a partir da raiz de `telefone/` (domínio custom via `CNAME`). Não há build — arquivos estáticos servidos diretamente.
