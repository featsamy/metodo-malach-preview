# Método Malach — página de vendas

Repositório da nova página de vendas do Método Malach, planejada para Cloudflare Pages com abordagem mobile-first, alta velocidade e foco em conversão responsável.

## Estado atual

V2 implementada para a oferta do kit físico Método Malach e validada em build de produção. A página usa Astro, Tailwind CSS e saída estática pronta para Cloudflare Pages.

## Desenvolvimento

```bash
npm install
npm run dev
```

Build de produção:

```bash
npm run build
```

A Cloudflare Pages deve usar `npm run build` como comando e `dist` como diretório de saída.

Configure `PUBLIC_CHECKOUT_URL` no ambiente da Cloudflare Pages com a URL do checkout principal. Sem essa variável, os botões permanecem na seção de oferta para evitar encaminhar o visitante a um destino incorreto.

## Documentação

- [Guia mestre do projeto](docs/PROJECT-GUIDE.md)
- [Inventário de conteúdo e copy](docs/CONTENT-INVENTORY.md)
- [Arquitetura técnica e desempenho](docs/TECHNICAL-SPEC.md)
- [Medição, QA e lançamento](docs/MEASUREMENT-QA.md)

## Decisões pendentes antes da implementação

1. Aprovar a direção visual e o tom de voz.
2. Validar a copy e as alegações de saúde/compliance.
3. Confirmar preço, parcelamento, garantia e URL final do checkout.
4. Confirmar direitos de uso de fotos, depoimentos e demais assets.
5. Definir analytics, pixel de mídia e ferramenta de consentimento.
