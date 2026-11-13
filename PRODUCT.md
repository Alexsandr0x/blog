# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Stack
Site estático publicado em alexsandro.dev (GitHub Pages, deploy via GitHub Actions, sem orçamento de hospedagem). Decisão confirmada: **manter o Hugo** (layouts e CSS próprios sobrescrevem o tema Risotto, sem editar o submódulo do tema) e o deploy atual via GitHub Actions.

## Users
Alex (Alexsandro), Tech Lead e Coordenador de Dados na ImpulsoGov, professor por vocação. Visitantes: leitores técnicos de língua portuguesa (principal) e inglesa (secundário, via traduções); alunos e colegas de dados; pessoas avaliando o perfil profissional de Alex.

## Product Purpose
Site pessoal multi-uso. Apesar de se chamar "blog", reúne quatro frentes e uma que falta:
1. Blog: posts médios e longos.
2. Repositório de palestras e aulas (menu "Palestras").
3. Microblog TIL/HEA ("Hoje Eu Aprendi"): anotações curtas do dia a dia.
4. Páginas de projeto (ex.: flappy-bem-te-vi, com jogo GBA embutido).
5. **Nova:** portfólio, página própria (separada de "Sobre"), que apresenta Alex com um "quase currículo". O rascunho é escrito a partir do que já se sabe e será revisado por Alex.

## Capabilities and Constraints
- Conteúdo existente e URLs são preservados no redesenho; pt-br é o idioma padrão, com versões en.
- Menu: Sobre, Portfólio, Posts, Palestras, Projetos, HEA (pt-br); About, Portfolio, Posts, Talks, Projects, HEA (en). As URLs não mudam (`/lessons/` continua).
- O HEA vive em repositório próprio (submódulo `content/hea`) e aparece como **lista única**, por data.
- O texto do site deve ser simples e didático (a estética não vale como desculpa para texto obscuro).
- Camada de deploy automático obrigatória.

## Brand Commitments
Restrição visual binding declarada pelo dono: o site deve parecer um terminal de computador em uma realidade cyberpunk (referências: terminais de máquinas de Evangelion e Cyberpunk 2077), com aura retro de monitor ASCII e vibe DIY/hacker. Vale só para o visual; o texto permanece simples.

## Evidence on Hand
Posts em `content/posts`, talks em `content/lessons` (3 talks), projeto em `content/projects`, HEA em `content/hea`, página Sobre em `content/about`. Não há currículo estruturado no repositório: o conteúdo do "quase currículo" precisa vir de Alex e não deve ser inventado.

## Product Principles
- Um site, várias frentes: cada tipo de conteúdo tem forma própria, sem parecer cinco sites colados.
- Visual extremo, texto claro: o mundo cyberpunk não pode custar legibilidade.
- Conteúdo e URLs sobrevivem ao redesenho.
- DIY: simples de manter e publicar por quem o escreve.
