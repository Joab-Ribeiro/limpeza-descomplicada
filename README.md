# Limpeza Descomplicada — página de vendas

Cópia da página de vendas que estava no GreatPages, agora como um site próprio
(um arquivo `index.html` + imagens em `assets/img/`). Não depende de nenhuma
ferramenta paga para funcionar.

## O que já vem configurado

- **Checkout Greenn:** `https://payfast.greenn.com.br/redirect/179526` (4 botões).
  Os outros 3 botões rolam a página até o bloco de preço.
- **Google Tag Manager:** `GTM-TS7QPR2Z` (dispara GA4, TikTok etc., como antes).
- **Pixel do Facebook:** `394447143723680` (evento `ViewContent`, como no GreatPages).
- **UTMs no checkout:** o mesmo script que você usava no GreatPages. Ele guarda
  `utm_*`, `fbclid`, `gclid`, `ttclid`, `src`, `sck` etc. por 7 dias e repassa
  esses dados para o link do checkout.
- **Vídeos:** Vimeo no topo e 5 depoimentos do YouTube (carregam só quando a
  pessoa chega na seção).
- **Imagens otimizadas em WebP:** ~0,7 MB no total (no GreatPages eram ~35 MB).

## Como editar o básico

Abra o `index.html` em qualquer editor de texto e use "Localizar" (Ctrl+F):

| Quero mudar…              | Procure por                                   |
|---------------------------|-----------------------------------------------|
| Link do checkout          | `payfast.greenn.com.br/redirect/179526`       |
| Preço parcelado           | `20,25*`                                      |
| Preço à vista             | `R$197,00 à vista`                            |
| Preço "De:"               | `R$897,00`                                    |
| Vídeo do topo (Vimeo)     | `player.vimeo.com/video/1177483040`           |
| Vídeos de depoimento      | `youtube.com/embed/`                          |

## Como publicar (opções gratuitas)

Qualquer hospedagem de site estático funciona. Basta enviar a pasta inteira
(`index.html` + `assets/`):

- **Netlify** (netlify.com) — arraste a pasta na tela "Deploy manually".
- **Vercel** ou **Cloudflare Pages** — conecte este repositório do GitHub.
- **GitHub Pages** — em *Settings → Pages* deste repositório, escolha a branch.
- **Hospedagem que você já tenha** (Hostinger, HostGator…) — envie os arquivos
  para uma pasta `limpeza-descomplicada` dentro de `public_html`.

### Atenção ao domínio

Hoje o endereço é `www.brunatreinamentos.com.br/limpeza-descomplicada`, servido
pelo GreatPages. Se outras páginas suas também estão no GreatPages com esse
domínio, mudar o DNS do `www` tira todas elas do ar ao mesmo tempo. Nesse caso,
o mais seguro é publicar esta página num subdomínio novo (ex.:
`curso.brunatreinamentos.com.br`) e trocar o link nos anúncios.

Se o endereço final for diferente do atual, atualize as linhas `og:url` e
`og:image` no topo do `index.html` (são usadas na prévia do link no WhatsApp e
no Facebook).
