# Limpeza Descomplicada — página de vendas

Páginas que estavam no GreatPages, agora como um site próprio publicado na
**Cloudflare** (Workers com arquivos estáticos). Tudo o que vai ao ar fica na
pasta `public/`. Cada arquivo `.html` vira um endereço com o mesmo nome:

| Página                     | Arquivo                             | Endereço                                              |
|----------------------------|-------------------------------------|-------------------------------------------------------|
| Limpeza Descomplicada      | `public/limpeza-descomplicada.html` | `lp.brunatreinamentos.com.br/limpeza-descomplicada`   |
| Combo Niver da Prof        | `public/niver.html`                 | `lp.brunatreinamentos.com.br/niver`                   |

```
public/
  *.html                       → as páginas
  assets/img/                  → imagens em WebP (as da página Niver ficam em assets/img/niver/)
  _redirects                   → quem entra em "/" vai para /limpeza-descomplicada
  _headers                     → cache das imagens (7 dias)
  404.html                     → página de "não encontrada"
```

### Rastreamento por página

- **Limpeza Descomplicada:** Google Tag Manager `GTM-TS7QPR2Z`, Pixel do Facebook
  e o script próprio que repassa UTMs para o checkout (detalhes abaixo).
- **Combo Niver:** Pixel do Facebook (`ViewContent`) e **Utmify**, que repassa as
  UTMs (`xcod`/`sck`) para o checkout `payfast.greenn.com.br/redirect/282119` e
  marca o link do WhatsApp. Botão flutuante do WhatsApp: `5547991719826`.

## Limpeza Descomplicada: o que já vem configurado

- **Checkout Greenn:** `https://payfast.greenn.com.br/redirect/179526` (4 botões).
  Os outros 3 botões rolam a página até o bloco de preço.
- **Google Tag Manager:** `GTM-TS7QPR2Z` (dispara GA4, TikTok etc., como antes).
- **Pixel do Facebook:** `394447143723680` (evento `ViewContent`, como no GreatPages).
- **UTMs no checkout:** o mesmo script do GreatPages. Guarda `utm_*`, `fbclid`,
  `gclid`, `ttclid`, `src`, `sck` etc. por 7 dias e repassa para o checkout.
  As UTMs também são mantidas nos redirecionamentos (`/` e `/limpeza-descomplicada/`).

## Publicação na Cloudflare (Workers conectado ao GitHub)

O projeto `limpeza-descomplicada` na Cloudflare está ligado a este repositório.
Toda alteração enviada para a branch de produção é publicada sozinha.

- `wrangler.jsonc` (na raiz) diz à Cloudflare para publicar a pasta `public/`.
  O `name` dele precisa ser igual ao nome do projeto no painel.
- Configuração no painel: comando da build **vazio**, comando de implantação
  `npx wrangler deploy`, diretório raiz `/`.

### Ligar o domínio

No projeto: **Configurações → Domínios e rotas → Adicionar → Domínio
personalizado** → `lp.brunatreinamentos.com.br`. Como o domínio já está na
Cloudflare, o DNS é criado sozinho.

Endereço final: `https://lp.brunatreinamentos.com.br/limpeza-descomplicada`

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

Abra o `.html` da página e use "Localizar" (Ctrl+F). Exemplos da Limpeza Descomplicada:

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
npx wrangler dev
```

Abre em `http://localhost:8787/limpeza-descomplicada`, com o mesmo comportamento
da Cloudflare.
