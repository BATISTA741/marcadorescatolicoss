# 150 Marcadores Católicos — Landing page (Portugal)

Site estático: `index.html` + pasta `images/`. Não precisa de build.

## 1. Configuração (fim do `index.html`, bloco `CONFIGURAÇÃO`)

```js
UTMIFY_PIXEL_ID: '6af5faa1da03acc1ff584cf1', // Pixel da UTMify (já preenchido)
UTMIFY_UTMS: true,                            // script de UTMs da UTMify (repasse para o checkout)
PIXEL_ID: 'SEU_PIXEL_ID',                     // deixe assim se o Pixel da Meta é gerido pela UTMify
FIM_OFERTA: '2026-11-30T23:59:59Z'            // fim REAL do preço de lançamento
```

## 2. GitHub → Vercel
1. Crie um repositório no GitHub e envie esta pasta (index.html, images/, README.md).
2. Na Vercel: **Add New → Project → Import** o repositório.
3. Framework Preset: **Other**. Sem build command, sem output directory. Deploy.
4. (Opcional) Ligue o seu domínio em **Settings → Domains**.

## 3. O que já está na página
- **Aviso de cookies (RGPD):** os scripts da UTMify e o Pixel só carregam depois de "Aceitar". Link "Preferências de cookies" no rodapé.
- **UTMify:** script oficial `cdn.utmify.com.br/scripts/pixel/pixel.js` com o seu `pixelId`.
- **UTMs → Hotmart:** feito pelo script de UTMs da UTMify (`utms/latest.js`, com `data-utmify-prevent-subids`). Se puser `UTMIFY_UTMS: false`, a página usa o repasse próprio (UTMs + `sck` para o relatório de Origem de Vendas da Hotmart).
- **Pixel da Meta direto (opcional):** PageView, ViewContent e InitiateCheckout. Só ativa se preencher `PIXEL_ID`. Não use em simultâneo com o mesmo pixel na UTMify, para não duplicar eventos.

## 4. Falta fazer fora da página
- **UTMify:** ligar a Hotmart (webhook de vendas) e o Pixel/API de Conversões da Meta no painel.
- **Meta Ads → Parâmetros de URL** do anúncio: use os parâmetros que a UTMify indicar, ou
  `utm_source=FB&utm_campaign={{campaign.name}}|{{campaign.id}}&utm_medium={{adset.name}}|{{adset.id}}&utm_content={{ad.name}}|{{ad.id}}&utm_term={{placement}}`
- **Teste:** abra o site com `?utm_source=teste`, aceite os cookies, passe o rato sobre um botão de compra e confirme que o link tem `utm_source=teste`. Na UTMify, confirme que a visita aparece.
