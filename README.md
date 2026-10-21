# JTech Climatização, Lavadoras e Refrigeração

Landing page de captação de orçamentos. HTML, CSS e JavaScript puros, sem build e sem
dependências. Para ver localmente, basta abrir o `index.html` no navegador.

```
index.html     conteúdo, SEO e dados estruturados (LocalBusiness)
styles.css     sistema visual completo
script.js      CONFIG do contato, mensagens, seletor de equipamento, menu, galeria
img/           fotos em WebP e imagem de compartilhamento (og.jpg)
favicon.svg    ícone da aba
```

---

## 1. Ligar o WhatsApp (o mais importante)

O número fica em **um único lugar**, no topo do `script.js`:

```js
const CONFIG = {
  whatsapp: '',   // ex.: '5551987654321'  (55 + DDD + número, só dígitos)
  ...
};
```

- **Vazio (hoje):** todos os 14 botões abrem o Direct do Instagram
  (`ig.me/m/jtechclimatizacaoelavadoras`) e os textos dizem "Instagram".
  Nenhum número inventado vai ao ar.
- **Preenchido:** todos viram links `wa.me` com mensagem pronta para cada contexto
  (geral, cada equipamento, seletor, região, dúvida), os textos passam a dizer
  "WhatsApp" e o número aparece formatado no rodapé.
- Número em formato errado: o site continua no Instagram e avisa no console.

As mensagens estão em `MESSAGES`, logo abaixo do `CONFIG`.

Depois de confirmar o número, adicione também `"telephone": "+55 51 ..."` ao JSON-LD no
`<head>` do `index.html` (o Google lê esse bloco, não o JavaScript).

## 2. Antes de publicar

| # | O que | Onde |
|---|---|---|
| 1 | Número de WhatsApp | `script.js`, `CONFIG.whatsapp` |
| 2 | Domínio | `index.html`: `canonical`, `og:url`, `og:image`, `twitter:image`, JSON-LD (marcados `TROCAR`). Hoje: `https://jtechclimatizacao.com.br/` |
| 3 | Fotos reais | ver seção 3 |

## 3. Trocar as fotos

Todas as fotos atuais são de banco (Pexels e Unsplash). A galeria avisa "Imagens
ilustrativas" e o rodapé cita a origem. **Esses avisos só saem quando todas as fotos
forem da JTech.** Use as fotos do Instagram, principalmente o antes e depois.

| Arquivo | Proporção exibida | Onde |
|---|---|---|
| `hero-1400.webp` + `hero-800.webp` | 4:5 | hero |
| `card-ar.webp`, `card-lavadora.webp`, `card-geladeira.webp`, `card-microondas.webp` | 16:10 | cards de serviço |
| `porque.webp` | 4:5 | "Assistência técnica sem complicação" |
| `gal-*.webp` + `gal-*-lg.webp` | 3:4 (a `-lg` abre ampliada) | galeria |
| `og.jpg` | 1200x630 | prévia ao compartilhar o link |

Tudo é recortado com `object-fit: cover`, então outra proporção também funciona.
Ao trocar uma foto, atualize `alt`, `width` e `height` da `<img>` e, na galeria, o
`data-caption` (tire o "(imagem ilustrativa)").

Converter com ffmpeg: `ffmpeg -i foto.jpg -vf scale=800:-2 -c:v libwebp -quality 78 gal-x.webp`

## 4. Decisões do projeto

- **O azul domina:** hero, seletor, CTA e rodapé em azul-marinho; superfícies
  secundárias em azul-claro. Raios: 10px em botões e controles, 18px em cards e fotos.
- **Ícones:** Tabler (traço linear), embutidos como sprite SVG no topo do `index.html`.
- **Nada inventado:** sem garantias, anos de experiência, avaliações, preços, marcas
  autorizadas ou 24 horas. O FAQ manda confirmar quando depende do equipamento,
  defeito ou localização.
- **Seletor de equipamento** usa rádios de verdade (teclado e leitor de tela
  funcionam); o botão só aparece depois da escolha.
- **Sem listener de scroll**: tudo por `IntersectionObserver`. Movimento reduzido é
  respeitado. Sem JavaScript, o conteúdo aparece e os links levam ao Instagram.
- **Celular:** barra fixa "Solicitar orçamento" depois dos botões do hero, some no CTA
  final; o `body` reserva o espaço dela. A galeria vira uma faixa que se arrasta.
