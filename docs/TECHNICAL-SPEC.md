# Arquitetura técnica e desempenho

## 1. Stack recomendada

### Base

- **Astro:** gera HTML estático, envia pouco JavaScript e permite componentes isolados quando necessários.
- **Tailwind CSS:** sistema de estilos utilitário com tokens definidos no projeto.
- **TypeScript:** configuração e scripts pequenos com contratos claros.
- **Cloudflare Pages:** previews por branch, CDN global, HTTPS e deploy estático.

Uma SPA em React/Next não é necessária para a V1. Se um componente interativo exigir framework, usar ilha isolada; para FAQ, menu, CTA e animações simples, HTML/CSS/JavaScript nativo é suficiente.

## 2. Estrutura planejada

```text
/
├─ public/
│  ├─ fonts/
│  ├─ images/
│  └─ _headers
├─ src/
│  ├─ assets/
│  ├─ components/
│  │  ├─ sections/
│  │  └─ ui/
│  ├─ content/
│  ├─ layouts/
│  ├─ pages/
│  ├─ scripts/
│  └─ styles/
├─ docs/
├─ astro.config.mjs
├─ package.json
└─ tsconfig.json
```

Conteúdo repetido, como módulos, FAQ e depoimentos, deve vir de dados tipados em vez de markup duplicado.

## 3. Renderização e comportamento

- HTML estático no edge/CDN;
- zero JavaScript para conteúdo essencial e links de compra;
- hidratação apenas sob interação ou visibilidade, se realmente necessária;
- animações com CSS, `IntersectionObserver` pequeno e respeito a `prefers-reduced-motion`;
- FAQ com elementos semânticos `details/summary` ou controle acessível equivalente;
- links de checkout com fallback normal, sem depender do analytics.

## 4. Design system

Tokens obrigatórios:

- cores semânticas: background, surface, text, muted, brand, accent, success, warning;
- escala tipográfica fluida com `clamp()`;
- escala de espaçamento consistente;
- raios, sombras, largura de container e breakpoints;
- estados hover, focus, active e disabled;
- z-index nomeados e limitados.

Componentes iniciais: `Container`, `Section`, `ButtonLink`, `Eyebrow`, `SectionHeading`, `MediaFrame`, `TestimonialCard`, `ModuleCard`, `OfferCard`, `Guarantee`, `FaqList` e `LegalNotice`.

## 5. Imagens e vídeo

- manter originais fora da cadeia de derivados de baixa qualidade;
- gerar AVIF e WebP com fallback quando necessário;
- declarar `width` e `height` para evitar layout shift;
- usar `srcset`/`sizes` por contexto;
- hero otimizado e potencialmente preloaded apenas se for o LCP;
- imagens abaixo da dobra com lazy loading;
- não carregar imagem desktop no mobile quando crops diferentes forem necessários;
- evitar GIF e vídeo autoplay pesado;
- poster responsivo e carregamento sob interação para vídeo.

## 6. Fontes

- preferir fonte variável ou no máximo dois pesos por família;
- hospedar localmente em WOFF2, se a licença permitir;
- subset latino quando adequado;
- preload apenas da fonte crítica;
- fallback com métricas compatíveis;
- `font-display: swap` ou `optional`, conforme teste visual.

## 7. Budgets de performance

Alvos de campo no percentil 75, mobile:

- LCP ≤ 2,5 s;
- INP ≤ 200 ms;
- CLS ≤ 0,10.

Budgets iniciais para a rota principal em compressão de rede:

- JavaScript inicial próprio ≤ 50 KB gzip;
- CSS inicial ≤ 40 KB gzip;
- fontes iniciais ≤ 100 KB;
- imagem LCP ≤ 180 KB no perfil mobile;
- peso inicial antes de lazy assets ≤ 700 KB;
- nenhum script de terceiro sem proprietário e justificativa.

Lighthouse em ambiente de produção é diagnóstico, não substitui dados reais. Meta de CI: Performance ≥ 90 e Accessibility/Best Practices/SEO ≥ 95, com variação controlada.

## 8. Acessibilidade

Alvo: WCAG 2.2 AA.

- landmarks e hierarquia de headings corretos;
- foco visível e ordem de tabulação lógica;
- contraste AA inclusive em CTA e texto pequeno;
- alvos de toque com tamanho e espaçamento adequados;
- alt text editorial, não redundante;
- depoimentos em texto, não apenas screenshots;
- controles com nomes acessíveis;
- nenhuma informação dependente apenas de cor;
- zoom e reflow até 400%;
- motion reduzido e ausência de flashes;
- skip link para conteúdo principal.

## 9. SEO e compartilhamento

- `lang="pt-BR"`, title e description exclusivos;
- canonical no domínio final;
- Open Graph e Twitter cards;
- favicon e web app icons;
- sitemap e robots coerentes com ambiente;
- previews/branches com `noindex`;
- JSON-LD apenas para entidades e propriedades verificáveis;
- evitar marcação de avaliação, produto ou FAQ que não cumpra diretrizes do buscador.

## 10. Analytics, privacidade e terceiros

- carregar tags conforme consentimento e base legal aplicável;
- não enviar texto sensível, diagnósticos, e-mail ou telefone em eventos/URLs;
- preferir um único gerenciador de tags;
- atrasar scripts não essenciais sem perder atribuição autorizada;
- documentar finalidade, fornecedor, cookie e retenção;
- permitir revogação de consentimento;
- mascarar dados sensíveis em ferramentas de replay, se usadas.

## 11. Checkout e atribuição

Todos os CTAs usam a variável `PUBLIC_CHECKOUT_URL` como configuração central do destino. Parâmetros permitidos de campanha devem ser preservados por allowlist, evitando repassar dados arbitrários ou sensíveis.

Requisitos:

- abrir na mesma aba por padrão;
- evento `cta_click` disparado sem bloquear navegação;
- `cta_id` e `section_id` estáveis;
- validação automatizada da URL e teste manual de compra;
- preço da página conferido contra o checkout antes do deploy.

## 12. Cloudflare Pages

- build command previsto: `npm run build`;
- diretório de saída previsto: `dist`;
- versão do Node fixada no projeto;
- preview para pull requests/branches;
- variáveis separadas por preview e produção;
- headers de segurança em `public/_headers`;
- redirects em arquivo dedicado quando necessário;
- domínio canônico e redirecionamento HTTPS/www definidos no lançamento.

Headers a avaliar e testar: CSP, `Referrer-Policy`, `X-Content-Type-Options`, `Permissions-Policy` e proteção contra framing compatível com integrações.

## 13. Compatibilidade

Suportar as duas versões principais atuais de Chrome, Safari, Firefox e Edge, além de Safari iOS e Chrome Android. A experiência deve degradar de forma segura em navegadores mais antigos.
