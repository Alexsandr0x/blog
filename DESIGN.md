---
name: alexsandro.dev
description: Terminal de garagem — painéis âmbar e ciano sobre preto azulado, texto claro e didático.
colors:
  base: "#0a0f12"
  surface: "#121a1f"
  surface-deep: "#0d1519"
  line: "#26343c"
  text: "#ece6d8"
  muted: "#8a979c"
  amber: "#ffb000"
  amber-ink: "#1a1000"
  cyan: "#46d9e8"
  alert-red: "#ff5a4d"
typography:
  display:
    fontFamily: "Shippori Mincho, Iowan Old Style, Georgia, serif"
    fontSize: "6rem"
    fontWeight: 800
    lineHeight: 0.95
    letterSpacing: "-0.03em"
  headline:
    fontFamily: "Chakra Petch, Rajdhani, system-ui, sans-serif"
    fontSize: "1.75rem"
    fontWeight: 700
    lineHeight: 1.2
    letterSpacing: "0em"
  title:
    fontFamily: "Chakra Petch, Rajdhani, system-ui, sans-serif"
    fontSize: "1.3125rem"
    fontWeight: 700
    lineHeight: 1.3
    letterSpacing: "0em"
  body:
    fontFamily: "JetBrains Mono, ui-monospace, SF Mono, Menlo, monospace"
    fontSize: "1.0625rem"
    fontWeight: 400
    lineHeight: 1.7
    letterSpacing: "0em"
  label:
    fontFamily: "Chakra Petch, Rajdhani, system-ui, sans-serif"
    fontSize: "0.8125rem"
    fontWeight: 700
    lineHeight: 1
    letterSpacing: "0.14em"
rounded:
  none: "0px"
  chamfer: "14px"
spacing:
  xs: "0.5rem"
  sm: "0.75rem"
  md: "1.25rem"
  lg: "1.5rem"
  xl: "3rem"
components:
  button-primary:
    backgroundColor: "{colors.amber}"
    textColor: "{colors.amber-ink}"
    typography: "{typography.label}"
    rounded: "{rounded.none}"
    padding: "0.7rem 1.25rem"
  button-ghost:
    backgroundColor: "transparent"
    textColor: "{colors.amber}"
    typography: "{typography.label}"
    rounded: "{rounded.none}"
    padding: "0.7rem 1.25rem"
  panel:
    backgroundColor: "{colors.surface}"
    textColor: "{colors.text}"
    rounded: "{rounded.chamfer}"
    padding: "1.25rem 1.375rem"
  tag:
    backgroundColor: "transparent"
    textColor: "{colors.cyan}"
    typography: "{typography.label}"
    rounded: "{rounded.none}"
    padding: "0.05rem 0.55rem"
---

# Design System: alexsandro.dev

## Overview

**Creative North Star: "O Terminal de Garagem"**

Uma máquina técnica e tensa por fora, didática e acolhedora por dentro. O site se comporta como um painel de controle feito à mão por alguém que quer ensinar: preto azulado, âmbar de fósforo como voz dominante, ciano como apoio, linhas finas de 1px e painéis de canto cortado sobre uma grade de caracteres. O visual vem de terminais de máquinas de ficção científica (NERV, HUD de Cyberpunk 2077) e de monitores ASCII, mas o texto continua simples.

A densidade é média: vitrines (home, portfólio, projetos) carregam o efeito; páginas de leitura (posts, palestras, HEA) são calmas, com fundo liso, coluna de 70 caracteres e contraste alto. O mundo é só escuro, pensado para uma tela à noite.

**Key Characteristics:**
- Preto azulado nunca puro; um acento dominante e um de apoio.
- Três vozes tipográficas com função fixa.
- Três molduras: borda simples, canto cortado (diagonal de 1px desenhada), linha dupla (reservada).
- Efeitos (pontos, scanlines, glitch curto) só nas vitrines, em CSS, e param com `prefers-reduced-motion`.

## Colors

Paleta de fósforo: um preto frio, um quente de texto, um amarelo-âmbar e um ciano.

### Primary
- **Âmbar de Fósforo** (#ffb000): links, títulos de seção (h2), botão principal, item de menu ativo, marcador de lista. Contraste 10,5:1 sobre a base.

### Secondary
- **Ciano de Apoio** (#46d9e8): prompt do terminal, tags, anel de foco de teclado, hover de link. Contraste 11,3:1.

### Tertiary
- **Vermelho de Alerta** (#ff5a4d): só estado (aviso de rascunho, erro). Contraste 6,3:1.

### Neutral
- **Preto de Tela** (#0a0f12): fundo de toda página.
- **Superfície de Painel** (#121a1f): painéis e linha de lista em hover.
- **Vidro Fundo** (#0d1519): blocos de código e monitor CRT.
- **Linha de Grade** (#26343c): bordas e divisórias de 1px.
- **Branco Quente** (#ece6d8): texto corrido (15,5:1).
- **Cinza de Metadado** (#8a979c): datas e legendas (6,4:1).

### Named Rules
**The Two Signals Rule.** Âmbar guia, ciano liga, vermelho avisa. Nenhuma outra cor de acento entra: verde, roxo e magenta estão fora.

**The Alert Is State Rule.** O vermelho nunca decora; só sinaliza estado.

## Typography

**Display Font:** Shippori Mincho 800 (com Iowan Old Style, Georgia)
**Body Font:** JetBrains Mono (com ui-monospace, Menlo)
**Label Font:** Chakra Petch (com Rajdhani, system-ui)

**Character:** Uma serifa pesada de título contra monoespaçada de texto e etiquetas angulares: livro técnico, terminal e painel de controle na mesma página. Fontes hospedadas no próprio site (subconjunto latino, OFL).

### Hierarchy
- **Display** (800, clamp até 6rem, 0.95): nome do site no hero; h1 de página em escala menor (2,25 a 3,5rem).
- **Headline** (Chakra 700, 1.75rem, 1.2): h2 de leitura, em âmbar.
- **Title** (Chakra 700, 1.3125rem, 1.3): h3, títulos de linha de lista.
- **Body** (400, 1.0625rem, 1.7): texto corrido, coluna de 70ch.
- **Label** (Chakra 700, 0.8125rem, 0.14em, caixa alta): títulos de painel, menu, botões, metadados.

### Named Rules
**The Three Voices Rule.** Mincho só em nome e títulos de página; Chakra Petch só em estrutura (menu, rótulos, h2/h3); mono em tudo que se lê.

**The No Kicker Rule.** Nenhum rótulo pequeno acima de um título e nenhuma numeração decorativa: o título carrega o próprio peso.

## Layout

Página de 76rem com gutter fluido (1 a 2,5rem). Vitrine em três zonas (perfil e atalhos, destaque, novidades) com `minmax(0, 15rem) 1fr minmax(0, 17rem)`; abaixo de 68rem vira duas colunas e abaixo de 52rem uma coluna, com o hero primeiro. Leitura em coluna única de 70ch. Listas em linhas com data de 7,5rem à esquerda. Ritmo de espaçamento em rem: mais espaço acima de um título (2,5 a 2,75rem) que abaixo (0,6 a 0,75rem).

## Elevation & Depth

Plano por tonalidade: sem sombras. Profundidade vem de camadas de superfície (base, painel, vidro fundo) e de linhas de 1px. O único brilho é o de fósforo em texto de destaque (`text-shadow` com deslocamento e desfoque) e no hero.

## Shapes

Ângulos retos, sem arredondamento. A assinatura é o **canto cortado**: um chanfro de 14px no canto superior direito (`clip-path`), com a diagonal desenhada à parte em 1px para não perder a borda. Botões e tags são retangulares. O hero usa um painel de pontos (grade de 12px) com máscara que corre devagar.

## Components

### Buttons
- **Shape:** retângulo, sem raio (0px).
- **Primary:** fundo âmbar (#ffb000), texto #1a1000, Chakra Petch 700 em caixa alta com 0.12em; padding 0.7rem 1.25rem.
- **Hover / Focus:** fundo vira branco quente; foco com anel ciano de 2px com offset de 3px.
- **Ghost:** borda de 1px âmbar, texto âmbar, hover com 12% de âmbar.

### Panel
Superfície #121a1f, borda de 1px (#26343c), canto cortado de 14px. Título em label âmbar. Variante quente: borda âmbar.

### Tag
Retângulo com borda de 1px, texto ciano, label de 0.75rem.

### Navigation
Menu em label caixa alta; item ativo em âmbar com sublinhado de 2px; seletor pt/en à direita. Em telas estreitas quebra em linhas.

### Monitor CRT (assinatura)
Bloco "ls palestras/" sobre #070b0d com texto real em âmbar com brilho suave, scanlines finas, vinheta e uma faixa luminosa que sobe devagar. O texto continua selecionável; os efeitos somem com `prefers-reduced-motion`.

## Do's and Don'ts

### Do:
- **Do** manter leitura sem efeito: fundo liso, 70ch, contraste mínimo de 4,5:1.
- **Do** usar âmbar para guiar e ciano para ligar; vermelho só para estado.
- **Do** desenhar o canto cortado com a diagonal de 1px, não só com `clip-path`.
- **Do** respeitar `prefers-reduced-motion` em todo efeito.

### Don't:
- **Don't** usar kanji, listras de perigo, papel amassado ou outro ornamento do Evangelion.
- **Don't** usar verde, roxo, magenta ou neon com vidro líquido.
- **Don't** exigir clique para mostrar conteúdo, nem WebGL, bibliotecas externas ou voz sintetizada.
- **Don't** empilhar mais de três tipos de moldura numa página.
