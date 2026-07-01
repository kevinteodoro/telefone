# AI_CONTEXT — Projeto SEO HTML/CSS/JS Puros

## Objetivo
- Ranquear no Google (SEO) para termos definidos pelo projeto.
- **Somente** HTML + CSS + JavaScript vanilla. Sem frameworks, sem bundlers, sem SSR.
- Páginas **mobile-first**, rápidas, acessíveis e sem dependências externas desnecessárias.

## Regras Gerais (obrigatórias)
1. **Tecnologia**: apenas HTML, CSS e JS puros. Nada de frameworks, bibliotecas externas, nem imports de CDNs (salvo fontes/svgs estritamente necessárias).
2. **Performance**: 
   - Lighthouse alvo: Performance ≥ 90, SEO ≥ 95, Acessibilidade ≥ 90.
   - TTFB baixo (usar HTML estático), **CSS crítico inline** (até ~8–12KB) e CSS restante em arquivo único minificado.
   - JS sempre **defer** (ou no fim do `body`), evitar bloqueio de render.
   - Imagens responsivas (`<img srcset>`), formatos modernos quando possível (webp/avif), `width/height` definidos.
3. **SEO On-Page**:
   - Uma **palavra-chave foco** por página (definir no topo do arquivo ao criar).
   - **Title** único (≤ 60 caracteres) e **meta description** (120–160).
   - **URL** curta, descritiva, com hífens: `minha-pagina-exemplo.html`.
   - **Heading único H1** contendo a palavra-chave foco; hierarquia correta de H2/H3.
   - **Conteúdo original** e útil; inserir sinônimos e LSI naturalmente.
   - **Links internos** contextuais e breadcrumbs.
   - **Canonical** sempre presente.
   - **Dados estruturados JSON-LD** apropriados (ex: `WebPage`, `Article`, `FAQPage`, `BreadcrumbList`).
   - **Open Graph/Twitter** para compartilhamento.
4. **Mobile-first & UX**:
   - `meta viewport` correto.
   - Layout fluido; tipografia legível; touch targets adequados (mín. 44x44px).
   - Evitar modais intrusivos; respeitar **CLS** (evitar layout shift).
5. **Acessibilidade**:
   - Semântica correta; `alt` em imagens; contrastes AA; foco visível; navegação por teclado.
   - `aria-` somente quando necessário (não substitui semântica).
6. **Privacidade/Tracking**:
   - Adiar qualquer script de analytics (se usado) com `defer` e eventuais consentimentos.
   - Não carregar tags que não sejam essenciais.
7. **Conteúdo e Tom**:
   - Clareza, utilidade e profundidade; responda intenção de busca (informacional/transacional/navegacional).
   - Use FAQs quando fizer sentido para *featured snippets*.
8. **Google Tag Manager (OBRIGATÓRIO)**:
   - **SEMPRE** incluir o snippet do GTM em TODAS as páginas criadas.
   - **Código no `<head>`**: antes do `</head>`, logo após as meta tags.
   - **Código após `<body>`**: logo após a abertura da tag `<body>`.
   - **ID do container**: usar `GTM-NLMC2HLF` (será rotacionado por segurança).
   - **Posicionamento**: GTM deve ser o primeiro script no head e o primeiro elemento no body.
   - **Fallback**: incluir sempre o código noscript para usuários sem JavaScript.

## Checklist para **nova página**
- [ ] Definir **palavra-chave foco** e intenção de busca.
- [ ] Redigir **Title** e **meta description**.
- [ ] Esqueleto HTML semântico, **H1 único** com a keyword.
- [ ] Conteúdo original e escaneável (sumário, H2/H3, listas, imagens com `alt`).
- [ ] Links internos (incluir 2–4 para páginas relevantes).
- [ ] JSON-LD adequado (WebPage/Article + BreadcrumbList; FAQ se houver).
- [ ] CSS crítico inline + restante minificado; fontes otimizadas.
- [ ] JS `defer`; sem bloqueio; sem libs externas.
- [ ] **GOOGLE TAG MANAGER** incluído no head e body (OBRIGATÓRIO).
- [ ] Teste mobile (quebra de layout, tipografia, CLS).
- [ ] Verificar Lighthouse (Perf/SEO/A11y).
- [ ] Adicionar à `sitemap.xml` (e link no `robots.txt`).
- [ ] Revisar ortografia e consistência de tom.

## Convenções de Arquivos
- Páginas em `/pages/` com nomes descritivos: `termo-principal.html`.
- Assets em `/assets/` (`/assets/img`, `/assets/css`, `/assets/js`).
- Um CSS global (`/assets/css/styles.min.css`) + CSS crítico inline por página.
- JS global mínimo (`/assets/js/main.js`) + JS específico por página se necessário.

## Template HTML Base (SEO + Mobile + GTM)
```html
<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />

  <!-- Google Tag Manager -->
  <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
  new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
  j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
  'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
  })(window,document,'script','dataLayer','GTM-NLMC2HLF');</script>
  <!-- End Google Tag Manager -->

  <title><!-- 55–60c: Título com keyword foco --></title>
  <meta name="description" content="<!-- 120–160c: descrição atraente com keyword -->" />

  <link rel="canonical" href="https://www.exemplo.com.br/slug-da-pagina/" />

  <!-- Open Graph -->
  <meta property="og:type" content="website" />
  <meta property="og:title" content="<!-- mesmo do title ou variante -->" />
  <meta property="og:description" content="<!-- igual/variante da description -->" />
  <meta property="og:url" content="https://www.exemplo.com.br/slug-da-pagina/" />
  <meta property="og:image" content="https://www.exemplo.com.br/assets/img/og.jpg" />

  <!-- Twitter -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="<!-- título -->" />
  <meta name="twitter:description" content="<!-- descrição -->" />
  <meta name="twitter:image" content="https://www.exemplo.com.br/assets/img/og.jpg" />

  <!-- CSS crítico inline (até ~12KB) -->
  <style>
    :root { line-height: 1.5; }
    * { box-sizing: border-box; }
    body { margin:0; font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif; color:#111; background:#fff; }
    img { max-width:100%; height:auto; }
    a { color:inherit; text-decoration: underline; }
    header, main, footer { width: min(92ch, 92%); margin-inline: auto; }
    .container { padding: 16px 0; }
    .btn { display:inline-block; padding:12px 16px; border-radius:8px; border:1px solid #ddd; text-decoration:none; }
    /* Evitar CLS para imagens/iframes */
    img, iframe { display:block; }
  </style>

  <!-- JSON-LD (ajuste conforme o tipo de página) -->
  <script type="application/ld+json">
  {
    "@context":"https://schema.org",
    "@type":"WebPage",
    "name":"<!-- título -->",
    "url":"https://www.exemplo.com.br/slug-da-pagina/",
    "description":"<!-- description -->",
    "breadcrumb":{
      "@type":"BreadcrumbList",
      "itemListElement":[
        {"@type":"ListItem","position":1,"name":"Início","item":"https://www.exemplo.com.br/"},
        {"@type":"ListItem","position":2,"name":"<!-- Seção -->","item":"https://www.exemplo.com.br/secao/"},
        {"@type":"ListItem","position":3,"name":"<!-- Página -->","item":"https://www.exemplo.com.br/slug-da-pagina/"}
      ]
    }
  }
  </script>

  <!-- CSS adicional minificado -->
  <link rel="preload" href="/assets/css/styles.min.css" as="style" />
  <link rel="stylesheet" href="/assets/css/styles.min.css" />
</head>
<body>
  <!-- Google Tag Manager (noscript) -->
  <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-NLMC2HLF"
  height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
  <!-- End Google Tag Manager (noscript) -->

  <header class="container" role="banner" aria-label="Topo do site">
    <nav aria-label="Breadcrumb">
      <ol>
        <li><a href="/">Início</a></li>
        <li><a href="/secao/">Seção</a></li>
        <li aria-current="page">Página</li>
      </ol>
    </nav>
    <h1><!-- H1 único com keyword foco --></h1>
  </header>

  <main class="container" role="main">
    <p><!-- Intro que responde a intenção de busca em 1–2 frases. --></p>

    <h2><!-- Subtópico 1 --></h2>
    <p><!-- Conteúdo útil, exemplos, listas --></p>

    <h2><!-- Subtópico 2 --></h2>
    <p><!-- Mais conteúdo relevante --></p>

    <!-- FAQ opcional (ótimo para snippets) -->
    <section aria-labelledby="faq-title">
      <h2 id="faq-title">Perguntas frequentes</h2>
      <dl>
        <dt><!-- Pergunta 1 --></dt>
        <dd><!-- Resposta 1 objetiva e clara --></dd>
        <dt><!-- Pergunta 2 --></dt>
        <dd><!-- Resposta 2 --></dd>
      </dl>
      <script type="application/ld+json">
      {
        "@context":"https://schema.org",
        "@type":"FAQPage",
        "mainEntity":[
          {"@type":"Question","name":"Pergunta 1","acceptedAnswer":{"@type":"Answer","text":"Resposta 1."}},
          {"@type":"Question","name":"Pergunta 2","acceptedAnswer":{"@type":"Answer","text":"Resposta 2."}}
        ]
      }
      </script>
    </section>

    <!-- Imagem exemplo com dimensões para evitar CLS -->
    <figure>
      <img src="/assets/img/exemplo.webp" width="1200" height="675" alt="Descrição objetiva da imagem" />
      <figcaption>Legenda descritiva opcional.</figcaption>
    </figure>
  </main>

  <footer class="container" role="contentinfo">
    <nav aria-label="Links de rodapé">
      <a class="btn" href="/contato.html">Contato</a>
      <a class="btn" href="/sobre.html">Sobre</a>
    </nav>
    <p>&copy; <span id="year"></span> Exemplo Ltda.</p>
  </footer>

  <script defer>
    // UX mínima e sem bloqueio
    document.getElementById('year').textContent = new Date().getFullYear();
  </script>
</body>
</html>
```

## Arquitetura atual e requisitos do Google AdSense (revisão de jun/2026)

Após 2 reprovações no AdSense, o site foi reestruturado. Regras que passam a valer:

### 1. Uma página por entidade real (evitar *scaled content abuse*)
- **Não criar** múltiplas páginas quase idênticas variando só o nome/subserviço da mesma marca (ex.: `telefone-claro`, `telefone-claro-fibra`, `telefone-claro-sac`, `ouvidoria-claro`...). Isso é conteúdo em massa e reprova no AdSense.
- Cada marca/entidade tem **uma única página abrangente** cobrindo todos os canais (SAC, ouvidoria, fibra, residencial, móvel, empresas) em seções internas.
- Slugs aposentados viram **stub de redirect** (não entram no `sitemap.xml`): `<link rel="canonical">` para a página nova + `<meta http-equiv="refresh" content="0; url=/pagina-nova/">` + `<meta name="robots" content="noindex, follow">` + redirect JS. Sem GTM/AdSense nos stubs.

### 2. Páginas obrigatórias (exigidas pelo AdSense)
- `/politica-de-privacidade/` — **obrigatória**; divulga cookies do Google AdSense/DoubleClick, GTM e terceiros, com links de opt-out.
- `/contato/` — canal real de contato do site.
- `/termos-de-uso/` — disclaimer de site independente, sem afiliação, dados sujeitos a alteração.
- Todas devem estar linkadas no footer `.site-map-nav` de **todas** as páginas.

### 3. AdSense e footer (obrigatórios em toda página de conteúdo)
- Snippet do AdSense `ca-pub-7989576624887637` logo após o GTM no `<head>`.
- Footer global `.site-map-nav` idêntico em todas as páginas + disclaimer honesto antes dele.
- `ads.txt` na raiz: `google.com, pub-7989576624887637, DIRECT, f08c47fec0942fa0`.

### 4. Confiabilidade / E-E-A-T honesto (não inventar autoridade)
- **Nunca** afirmar processo de verificação que não existe (ex.: "conferimos mensalmente", "verificado na base X") nem inserir data de verificação falsa.
- **Não** fabricar métricas (estrelas de "eficácia", "tempo médio: imediato"). Usar só prazos qualitativos plausíveis ou nada.
- Cada número deve ter disclaimer "sujeito a alteração — confira na fonte oficial" e link para o canal oficial da empresa.
- **ANATEL** só é canal de consumo para **telecomunicações** (Claro/TIM/Oi/Vivo/NET/SKY). Para os demais: `consumidor.gov.br` (Senacon) + Procon + Reclame Aqui; **bancos** → Banco Central (bcb.gov.br/meubc); **órgãos públicos** → Ouvidoria + Fala.BR (falabr.cgu.gov.br).

### 5. Links internos
- Nenhum link para slug inexistente. "Páginas Relacionadas" deve apontar só para páginas reais existentes.

### Estrutura de páginas (após consolidação)
- **21 páginas de conteúdo** (entidades distintas): Claro, TIM, Oi, Vivo, NET, SKY, Netflix; Nubank, Bradesco, Santander, Itaú, Caixa, Banco Inter; Amazon, Mercado Livre, Magazine Luiza, Jadlog, Total Express, Correios; INSS, Receita Federal.
- **+ home + 4 institucionais** (sobre, contato, política de privacidade, termos de uso) = 26 URLs no `sitemap.xml`.
- **+ 21 stubs de redirect** (fora do sitemap).