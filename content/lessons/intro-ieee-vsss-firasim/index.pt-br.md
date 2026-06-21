---
title: "Introdução ao IEEE VSSS com FIRASim"
translationKey: "intro-ieee-vsss-firasim"
date: 2023-03-01
tipo: "Aula"
quando: "2023"
onde: "Project Neon — UFABC"
---

Aula introdutória ministrada para a equipe de robótica [Project Neon](https://github.com/project-neon) da Universidade Federal do ABC, cobrindo a modalidade IEEE VSSS, o simulador FIRASim e os primeiros passos para criar um cliente Python capaz de se comunicar com o ambiente simulado.

---

## Introdução à Modalidade

A modalidade **IEEE VSSS** (IEEE Very Small Size Soccer) é a modalidade de entrada em competições de robótica universitárias para um desafio robótico de sistema multi-robótico, usando regras que emulam um futebol de robôs.

A modalidade consiste em dois times de 3 robôs cada, separados em dois lados do campo que tem como objetivo carregar a bola até a área do gol, posicionada do lado do campo do time adversário.

Regras como tamanho do campo e tamanho dos robôs tornam a modalidade padronizada num sistema robótico de robôs móveis diferenciais.

Os principais desafios da modalidade envolvem o desenvolvimento do robô, visão computacional, comunicação em rede, sistemas de controle e algoritmos de tomada de decisão.

## História

A modalidade IEEE VSSS nasceu de uma necessidade da modalidade **LARC** (Latin American Robotics Competition) de ter uma modalidade intermediária entre as modalidades de robótica júnior e a modalidade **Robocup Small Size League (F180)**. Suas regras são baseadas na modalidade **MIROSOT**, que por muitos anos aconteceu na competição **FIRA** (Federation of International Sports Association), com primeira versão na UNICAMP.

A modalidade veio ao Brasil através da LARC, sendo uma das competições organizadas pela IEEE RAS, junto às demais modalidades IEEE OPEN e IEEE SEK. Atualmente é competida em sua versão 3v3, com ocasionais desafios técnicos propondo equipes a 5v5 e simulada (3v3 e 5v5 através do FIRASim).

## Regras

As principais regras são publicadas pela própria organização da LARC através do seu chair de modalidade. As regras são atualizadas anualmente — todo ano um novo documento é emitido e regras novas podem ser adicionadas ou mudadas.

## Competições

As principais competições que incluem a modalidade:

- **Iron Cup** (4 - 6 equipes)
- **RCX Experience** (Primeira edição em 2023)
- **RSM International** (4 - 5 equipes)
- **LARC** (14 - 18 equipes)

As competições LARC e RSM têm alcance internacional.

## Documentação e Projetos

Além das regras, a modalidade conta com um histórico de **TDPs** (Technical Description Papers) — produzidos pelas equipes em suas participações anteriores na LARC. O TDP é obrigatório para participação e deve conter descrição do projeto com devidas descrições mecânicas, eletrônicas e de software.

Alguns projetos open source de referência:

- [NeonFC](https://github.com/project-neon/NeonFC) — Sistema de tomada de Decisão da Project Neon
- [robocin/vss-vision](https://github.com/robocin/vss-vision) — Sistema de Visão Computacional da Robocin
- [Red-Dragons-UFSCar/LARC-2021-Python](https://github.com/Red-Dragons-UFSCar/LARC-2021-Python) — Sistema de tomada de Decisão da Red Dragons

---

## Ambiente Simulado: FIRASim

O **FIRASim** é um software de simulação de um ambiente robótico semelhante a uma competição de simurosot. Como suas dimensões são as mesmas da modalidade IEEE VSSS, tornou-se comum equipes usá-lo como etapa de validação de seus algoritmos antes de testá-los no ambiente real.

O software é escrito em C++ e conta com uma interface gráfica com configurações e uma visualização do ambiente simulado — câmera, campo, robôs e bola. É possível mover os robôs e a bola via *drag-and-drop*.

O FIRASim também funciona como **servidor UDP**: recebe comandos e envia dados de estado usando o protocolo UDP, com mensagens encapsuladas via **Google Protobuf**.

### Instalação

Seguir o guia oficial disponível em:
[github.com/VSSSLeague/FIRASim/blob/master/INSTALL.md](https://github.com/VSSSLeague/FIRASim/blob/master/INSTALL.md)

Após o build, executar com:

```bash
./bin/FIRASim
```

### Interface do FIRASim

A interface possui três áreas principais:

![Interface completa do FIRASim — painel de configuração à esquerda e visualização 3D do campo](/images/vsss-firasim/img-000.png)

**1. View Gráfica** — Ambiente simulado com 3 robôs azuis contra 3 robôs amarelos. Use scroll para zoom, click esquerdo + movimento para ângulo da câmera e `C` para alternar câmeras pré-definidas.

![View Gráfica — campo 3D com time azul e time amarelo](/images/vsss-firasim/img-001.png)

**2. Variáveis de Configuração** — As configurações mais importantes:

| Parâmetro | Descrição |
|---|---|
| `Geometry.Game` | Define a divisão e quantidade de robôs em campo |
| `Communication.Vision multicast Address` | Endereço UDP Multicast para envio dos dados do ambiente |
| `Communication.Vision multicast Port` | Porta do UDP Multicast |
| `Communication.Vision listen Port` | Porta onde o FIRASim escuta comandos (localhost em ambiente local) |

![Painel de variáveis de configuração — seção Communication](/images/vsss-firasim/img-002.png)

**3. Seleção de Robô Atual** — Permite selecionar o robô desejado, desligá-lo (turn-off) ou definir sua posição pelas coordenadas e ângulo diretamente.

![Painel Current Robot — seleção de time e índice](/images/vsss-firasim/img-003.png)

---

## Mão na Massa: Cliente Python

### Conexão UDP & Google Protobuf

Para criar um cliente Python, precisamos entender dois conceitos:

**UDP Multicast** — Protocolo de transferência muito usado quando um servidor precisa enviar dados de forma muito rápida e constante, com pouca preocupação de garantia de chegada. É o protocolo usado entre nosso cliente e o FIRASim.

**Google Protobuf** — Biblioteca criada pelo Google para serializar dados de forma agnóstica a qualquer linguagem. Você cria um objeto em uma linguagem, compacta em bytes, e lê em outra linguagem com tipagens compatíveis. O FIRASim usa arquivos `.proto` para definir a estrutura dos pacotes de comunicação.

### Recebendo Dados do FIRASim

`código: p1_firasim_client.py`

Criamos uma conexão socket configurada para UDP Multicast. O resultado é um loop infinito recebendo dados do FIRASim em formato binário serializado — ilegível diretamente, pois está em estrutura Protobuf.

### Desserializando com Protobuf

`código: p2_firasim_client.py`

O resultado sem deserialização é ilegível — bytes Protobuf em formato bruto:

![Terminal com saída bruta dos bytes Protobuf recebidos via UDP](/images/vsss-firasim/img-004.png)

Os arquivos `.proto` do FIRASim estão em `FIRASim/msg`. As "compilações" para Python ficam na pasta `protocols` do projeto. Ao importar e deserializar, os dados ficam totalmente legíveis — posições de robôs, bola, dimensões do campo:

```python
# Estrutura principal (Frame)
{
  'ball': {'x': -0.097, 'y': -0.320, 'z': 0.021},
  'robotsYellow': [{'robotId': 0, 'x': 0.443, 'y': 0.442, 'orientation': 0.006}, ...],
  'robotsBlue': [{'robotId': 0, 'x': 0.375, 'y': 0.369, 'orientation': -0.007}, ...],
  'field': {'width': 1.3, 'length': 1.5, 'goalWidth': 0.4, 'goalDepth': 0.1}
}
```

![Terminal com saída deserializada — dados legíveis de bola, robôs e campo](/images/vsss-firasim/img-005.png)

A estrutura `.proto` do `common.proto` define os tipos `Ball`, `Robot`, `Field` e `Frame`. Note que quando os valores `x`, `y` ou `orientation` são zero, a chave não aparece na conversão para JSON — comportamento próprio do FIRASim.

![Estrutura do common.proto — mensagens Ball, Robot, Field e Frame](/images/vsss-firasim/img-006.png)

### Movimentando os Robôs

`código: p3_firasim_client.py`

Com as posições conhecidas, podemos enviar comandos de movimento. A estrutura `Commands` é uma lista de `Command`, onde cada um recebe:

- `yellowteam` [bool]: se o robô é do time amarelo
- `wheel_right` [float]: velocidade da roda direita (cm/s)
- `wheel_left` [float]: velocidade da roda esquerda (cm/s)
- `id` [int]: identificador numérico do robô

### Noções de Robô Diferencial

`código: p4_firasim_client.py`

Controlar o robô por velocidades de roda tem uma limitação: a informação é local — não sabemos se "mover a roda para frente" leva o robô à bola ou ao nosso gol.

A solução é um sistema que recebe velocidade em eixos cartesianos e converte para velocidades de roda, usando um algoritmo de controle que torna o robô referenciado globalmente ao campo. Independente de onde ele comece, ele se orienta para 45° e começa a se mover em relação ao campo.

A matemática por trás está no Coursera (Robot Control, Professor Magnus Egerstedt — aula 7.4 "A Clever Trick"). Os slides traduzidos estão nos slides desta aula.

### Campo Potencial para Locomoção

Uma das estratégias clássicas para movimentação autônoma de robôs — o conteúdo desta seção foi continuado na sequência do treinamento.

---

## Referências

- [Documentação Protobuf](https://protobuf.dev/) — Documentação oficial
- [Instalação FIRASim](https://github.com/VSSSLeague/FIRASim/blob/master/INSTALL.md)
- [NeonFC](https://github.com/project-neon/NeonFC) — Código da equipe
- Coursera: Robot Control — Professor Magnus Egerstedt (Georgia Tech)
- UFABC: Robótica Móvel — Professora Elvira Rafikova
