---
version: 1
slug: "layouts-index-html"
primary_target: "layouts/index.html"
related_targets: []
---

# Surface brief: alexsandro.dev (redesenho completo)

Escopo: todo o site (home, portfólio, posts, palestras, HEA, projetos), modo Experience nas vitrines (home, portfólio, projetos) e Read na leitura (post, palestra, HEA). Código primeiro, sem comp de imagem. Hugo mantido, layouts próprios sobre o tema Risotto, URLs e conteúdo preservados, pt-br e en.

## Direction contract

THESIS: Um painel técnico feito à mão: uma máquina técnica e tensa por fora, didática e acolhedora por dentro. Recusa o blog de dev genérico (cabeçalho, lista, rodapé em tema monocromático) e o cosplay de Matrix/neon.

OWN-WORLD: Base preto-azulada #0A0F12, superfície #121A1F, linha #26343C, texto #ECE6D8, âmbar de fósforo #FFB000 dominante, ciano #46D9E8 de apoio, vermelho #FF5A4D só para alerta. Shippori Mincho 800 no nome e nos títulos grandes, Chakra Petch nas etiquetas, JetBrains Mono no texto. Grade em ch; três molduras apenas: borda simples, canto cortado (diagonal desenhada em 1px), linha dupla. Textura neutra: scanlines finas e pontos âmbar só nas vitrines.

STORY: O visitante entende em segundos quem é Alex (Tech Lead de Dados, professor por vocação), onde estão posts, palestras, HEA e projetos, e lê sem esforço. Ação: abrir um conteúdo ou conhecer o portfólio.

FIRST VIEWPORT: Home em três zonas no desktop: à esquerda perfil e atalhos; no centro um painel de pontos âmbar com o nome em Mincho grande e a frase de apresentação, abaixo as últimas palestras e posts; à direita os últimos HEA. No celular, uma coluna com o hero primeiro. A ação principal (ver portfólio) fica sob a frase do hero.

FORM: Painéis de terminal sobre grade de caracteres. Posição na lista: direção pinada pelo usuário. seed: none (pinned). Pin: "Como se a pessoa tivesse em um terminal de computador numa realidade cyberpunk, referencias deve ser terminais de maquinas de Evangelion e Cyberpunk 2077, mas ao mesmo tempo com uma aura retro de monitor ASCII" e moodboard aprovado com "ok".

FINISH: unreviewed and undocumented is unfinished; this build ends with the finish review, the verdict, DESIGN.md, and every shipping raster carrying its provenance

## Decisões
- Leitura sem efeito algum: coluna de ~70ch, fundo liso. Efeitos (pontos, scanlines, glitch) só nas vitrines, em CSS, com prefers-reduced-motion.
- Sem kicker nem numeração decorativa. Sem atalhos de teclado, WebGL, kanji, tela de entrada.
- Imagens do moodboard e diagrama C4 arquivados no Cloud Storage; índice e links em `docs/design-assets.md`.
