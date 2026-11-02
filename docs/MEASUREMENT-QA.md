# Medição, QA e lançamento

## 1. Plano de eventos

| Evento | Quando | Parâmetros permitidos |
|---|---|---|
| `page_view` | visualização válida da página | page, referrer_group, campaign |
| `section_view` | seção relevante atinge limiar de visibilidade | section_id |
| `cta_view` | CTA de compra torna-se visível | cta_id, section_id |
| `cta_click` | clique em CTA de compra | cta_id, section_id, destination |
| `faq_open` | abertura de pergunta | faq_id |
| `testimonial_view` | prova social torna-se visível | testimonial_id |
| `scroll_depth` | 25%, 50%, 75% e 90% | threshold |
| `outbound_click` | clique externo não-CTA | link_group |
| `web_vital` | métrica de campo coletada | metric, value, rating |

Não coletar texto livre, informações de saúde, PII ou conteúdo de parâmetros não aprovados. Eventos devem ser deduplicados e versionados.

## 2. Atribuição

- preservar somente UTMs e identificadores expressamente aprovados;
- definir janela e fonte de verdade da conversão;
- documentar discrepâncias esperadas entre navegador, plataforma de anúncio e checkout;
- testar navegação com e sem consentimento;
- validar campanha em mobile real, incluindo navegadores internos de redes sociais.

## 3. Plano de QA funcional

- todos os CTAs apontam para a oferta correta;
- UTMs aprovadas chegam ao destino;
- FAQ funciona por mouse, toque e teclado;
- CTA fixo não cobre conteúdo nem avisos;
- links legais e de suporte funcionam;
- voltar do checkout preserva uma experiência válida;
- sem JavaScript, conteúdo e compra continuam acessíveis;
- eventos não duplicam e não atrasam navegação;
- banners/consentimento respeitam a escolha;
- preço, parcelas, bônus e garantia coincidem com o checkout.

## 4. Matriz de viewport

Testes prioritários:

- 320 × 568: largura mínima suportada;
- 360 × 800: Android compacto;
- 390 × 844: iPhone moderno;
- 412 × 915: Android moderno;
- 768 × 1024: tablet retrato;
- 1024 × 768: tablet paisagem;
- 1366 × 768: notebook comum;
- 1440 × 900 e 1920 × 1080: desktop.

Verificar também zoom 200%/400%, orientação, safe areas e teclado virtual.

## 5. QA visual e de conteúdo

- nenhum overflow horizontal;
- nenhuma linha órfã crítica em títulos/CTA;
- imagens sem distorção e crops aprovados;
- layout estável durante carregamento;
- contraste e foco visível;
- ortografia pt-BR e pontuação revisadas;
- depoimentos legíveis e dados pessoais tratados;
- disclaimers presentes nos pontos adequados;
- consistência de nomes de módulos e bônus;
- nenhuma informação comercial desatualizada.

## 6. QA de performance

- medir build limpo e preview de produção;
- testar perfil mobile com rede/CPU limitadas;
- confirmar elemento LCP e sua prioridade;
- auditar terceiros individualmente;
- verificar cache, compressão e formatos de imagem;
- validar que lazy loading não afeta conteúdo acima da dobra;
- coletar Web Vitals reais após lançamento;
- criar alerta para regressão dos budgets documentados.

## 7. QA de acessibilidade

- axe/Lighthouse sem violações sérias, seguido de teste manual;
- navegação completa somente por teclado;
- leitura com NVDA + Chrome/Firefox e VoiceOver + Safari;
- ordem de headings e landmarks;
- nomes, estados e descrições de controles;
- reflow, zoom, contraste e motion reduzido;
- conteúdo equivalente para screenshots e mídia.

## 8. Checklist pré-lançamento

### Comercial e conteúdo

- [ ] Copy final aprovada.
- [ ] Compliance aprovado por responsável identificado.
- [ ] Direitos de todos os assets confirmados.
- [ ] Oferta e checkout conferidos.
- [ ] Suporte, empresa e políticas publicados.

### Engenharia

- [ ] Build reprodutível e dependências auditadas.
- [ ] Preview aprovado em dispositivos reais.
- [ ] Headers, redirects, canonical, sitemap e robots validados.
- [ ] Analytics e consentimento testados.
- [ ] Monitoramento e rollback definidos.

### Qualidade

- [ ] Testes funcionais aprovados.
- [ ] Acessibilidade aprovada.
- [ ] Budgets de performance aprovados.
- [ ] Links e eventos validados em produção.
- [ ] Teste do caminho completo até a compra realizado.

## 9. Pós-lançamento

Primeiras 24 horas:

- monitorar disponibilidade, erros, cliques e discrepâncias de checkout;
- validar eventos com tráfego real;
- conferir Core Web Vitals e comportamento por dispositivo;
- checar campanhas e UTMs.

Primeiros 7–14 dias:

- estabelecer baseline por origem e dispositivo;
- identificar seções com abandono e CTAs com baixa interação;
- coletar objeções de suporte/reembolso;
- priorizar uma hipótese de melhoria por vez.

## 10. Backlog inicial de experimentos

Somente após baseline e volume suficiente:

1. clareza da promessa no hero;
2. CTA fixo no mobile;
3. ordem entre mecanismo e prova social;
4. formato da apresentação dos módulos;
5. prova social em texto versus cards visuais;
6. enquadramento da garantia;
7. resumo da oferta próximo ao primeiro CTA.

Cada teste deve ter hipótese, métrica primária, guardrails, duração mínima e critério de decisão definidos antes do início.
