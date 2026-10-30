# Limpeza Descomplicada — página de vendas

Cópia da página de vendas que estava no GreatPages, agora como um site próprio
publicado no **Cloudflare Pages**. Tudo o que vai ao ar fica na pasta `public/`:

```
public/
  limpeza-descomplicada.html   → a página (abre em /limpeza-descomplicada)
  assets/img/                  → imagens (WebP, ~0,7 MB no total)
  _redirects                   → quem entra em "/" vai para /limpeza-descomplicada
  _headers                     → cache das imagens (7 dias)
  404.html                     → página de "não encontrada"
```

## O que já vem configurado

- **Checkout Greenn:** `https://payfast.greenn.com.br/redirect/179526` (4 botões).
  Os outros 3 botões rolam a página até o bloco de preço.
- **Google Tag Manager:** `GTM-TS7QPR2Z` (dispara GA4, TikTok etc., como antes).
- **Pixel do Facebook:** `394447143723680` (evento `ViewContent`, como no GreatPages).
- **UTMs no checkout:** o mesmo script do GreatPages. Guarda `utm_*`, `fbclid`,
  `gclid`, `ttclid`, `src`, `sck` etc. por 7 dias e repassa para o checkout.
  As UTMs também são mantidas nos redirecionamentos (`/` e `/limpeza-descomplicada/`).

## Publicar no Cloudflare Pages (fazer uma vez)

1. No painel da Cloudflare: **Workers & Pages → Create application → Pages →
   Connect to Git**.
2. Escolha **GitHub**, autorize e selecione o repositório
   `limpeza-descomplicada` → **Begin setup**.
3. Preencha:
   - **Project name:** `brunatreinamentos` (ou outro nome; vira o endereço
     `nome.pages.dev`)
   - **Production branch:** a branch onde está a página
   - **Framework preset:** `None`
   - **Build command:** deixe vazio
   - **Build output directory:** `public` ← importante
4. **Save and Deploy**. Em ~1 minuto a página abre em
   `https://<nome-do-projeto>.pages.dev/limpeza-descomplicada`.
   Teste ali antes de ligar o domínio (inclusive clicar no botão de compra).
5. No projeto: **Custom domains → Set up a custom domain** →
   digite `lp.brunatreinamentos.com.br` → **Continue → Activate domain**.
   Como o domínio já está na Cloudflare, o DNS é criado sozinho.

Endereço final: `https://lp.brunatreinamentos.com.br/limpeza-descomplicada`

Depois disso, toda alteração enviada para a branch de produção no GitHub é
publicada automaticamente.

### Por que um subdomínio (`lp.`) e não o `www`?

O `www.brunatreinamentos.com.br` aponta para o GreatPages e serve ~23 páginas
(obrigado, links, comunidade, black…). Trocar o `www` derruba todas de uma vez.
Com o `lp.` o caminho continua igual (`/limpeza-descomplicada`); quando todas as
páginas tiverem saído do GreatPages, dá para apontar o `www` para este projeto
sem mudar mais nada.

**Não altere o registro DNS `www`** enquanto houver páginas no GreatPages.

Se escolher outro subdomínio, troque `lp.brunatreinamentos.com.br` nas linhas
`og:url`, `og:image` e `canonical` no topo de `public/limpeza-descomplicada.html`
(são usadas na prévia do link no WhatsApp/Facebook).

## Como editar o básico

Abra `public/limpeza-descomplicada.html` e use "Localizar" (Ctrl+F):

| Quero mudar…              | Procure por                                   |
|---------------------------|-----------------------------------------------|
| Link do checkout          | `payfast.greenn.com.br/redirect/179526`       |
| Preço parcelado           | `20,25*`                                      |
| Preço à vista             | `R$197,00 à vista`                            |
| Preço "De:"               | `R$897,00`                                    |
| Vídeo do topo (Vimeo)     | `player.vimeo.com/video/1177483040`           |
| Vídeos de depoimento      | `youtube.com/embed/`                          |

## Testar localmente

```bash
npx wrangler pages dev public
```

Abre em `http://localhost:8788/limpeza-descomplicada`, com o mesmo comportamento
da Cloudflare.
