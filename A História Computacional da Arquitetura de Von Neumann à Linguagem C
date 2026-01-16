# A História Computacional da Arquitetura de Von Neumann à Linguagem C

## Uma Análise Técnica, Eletrônica e Conceitual Aprofundada

---

# PARTE I: A ARQUITETURA DE VON NEUMANN E OS PRIMEIROS COMPUTADORES

## Capítulo 1: O Contexto Histórico e as Origens

### 1.1 O Cenário Pré-Von Neumann

Antes de compreender a arquitetura de Von Neumann, é essencial entender o contexto tecnológico da década de 1940. Os computadores existentes eram máquinas de propósito específico, programadas através de conexões físicas — cabos, plugues e chaves. O ENIAC (Electronic Numerical Integrator and Computer), completado em 1945, exemplifica essa era.

#### 1.1.1 O ENIAC: Contexto Técnico

O ENIAC foi projetado por J. Presper Eckert e John Mauchly na Moore School of Electrical Engineering da Universidade da Pensilvânia, com o objetivo principal de calcular tabelas balísticas para o Exército dos EUA.

**Especificações Técnicas do ENIAC:**

- **Válvulas:** 18.000 válvulas termiônicas (vacuum tubes)
- **Diodos de cristal:** 7.200
- **Relés:** 6.000
- **Resistores:** 70.000
- **Capacitores:** 10.000
- **Junções soldadas:** Aproximadamente 5.000.000
- **Peso:** Mais de 30 toneladas
- **Dimensões:** Aproximadamente 30m de comprimento, 3m de altura, 1m de profundidade
- **Consumo:** 150 kW de eletricidade
- **Área ocupada:** 300 m²

#### 1.1.2 O Sistema Numérico do ENIAC

O ENIAC era uma **máquina decimal**, não binária. Este é um ponto crucial para entender a evolução para computadores orientados a word.

**Funcionamento dos Acumuladores:**

O ENIAC utilizava **ring counters de 10 posições** para armazenar dígitos. Cada dígito decimal requeria 36 válvulas:
- 10 válvulas formavam os flip-flops do ring counter (dual triodes)
- As demais válvulas controlavam carry, entrada e saída

A aritmética era realizada por "contagem" de pulsos:

```
Estrutura do Ring Counter (para um dígito):

    ┌────────────────────────────────────────┐
    │  FF0 ─ FF1 ─ FF2 ─ FF3 ─ FF4 ─ FF5 ─   │
    │   │                                 │  │
    │  FF9 ─ FF8 ─ FF7 ─ FF6 ─────────────┘  │
    │                                        │
    │  Pulsos de entrada ──▶ Incrementam     │
    │  Carry gerado quando FF9 → FF0         │
    └────────────────────────────────────────┘
```

Cada ring counter podia representar um valor de 0 a 9. Quando pulsos chegavam, o estado "ativo" circulava pelo anel. Se ultrapassasse 9 (voltando a 0), um pulso de carry era gerado para o próximo dígito.

**Implicação Importante:** O ENIAC emulava eletronicamente uma calculadora mecânica de rodas dentadas. Esta decisão de design foi pragmática — os engenheiros entendiam bem aritmética decimal e podiam verificar resultados manualmente.

#### 1.1.3 A Programação do ENIAC

O ENIAC **não era orientado a word** no sentido moderno. Sua "programação" consistia em:

1. **Conexão física de cabos** entre unidades funcionais
2. **Configuração de chaves** para definir operações
3. **Configuração das function tables** (memória somente-leitura)

A "memória" do ENIAC era distribuída:
- **Acumuladores:** 20 unidades, cada uma com 10 dígitos decimais com sinal (complemento de 10)
- **Function tables:** Memória somente-leitura para constantes
- **Sem memória de programa:** O programa existia fisicamente nos cabos

**Reprogramação:** Mudar o programa podia levar dias, pois requeria reconexão física de centenas de cabos.

### 1.2 John von Neumann e o Projeto Manhattan

John von Neumann (1903-1957) era um matemático húngaro-americano de extraordinária capacidade intelectual. Trabalhava no Projeto Manhattan em Los Alamos, onde os cálculos para a bomba atômica (e posteriormente a bomba de hidrogênio) exigiam poder computacional massivo.

#### 1.2.1 O Encontro com o ENIAC

No verão de 1944, Von Neumann tomou conhecimento do projeto ENIAC. Herman Goldstine, oficial do Exército e administrador do projeto, encontrou Von Neumann casualmente em uma estação de trem. Reconhecendo-o, Goldstine mencionou o ENIAC, e Von Neumann ficou imediatamente interessado.

Von Neumann começou a atuar como consultor no projeto, trazendo sua formação em lógica matemática para as discussões sobre o design do próximo computador — o EDVAC.

#### 1.2.2 Influências Intelectuais sobre Von Neumann

Von Neumann foi influenciado por várias fontes:

1. **Alan Turing e a Máquina Universal de Turing (1936):**
   - A máquina hipotética de Turing tinha uma "fita" infinita contendo tanto dados quanto instruções
   - A máquina podia ler, escrever e se mover na fita
   - Este conceito de programa armazenado como dados foi fundamental

2. **Warren McCulloch e Walter Pitts (1943):**
   - Paper "A Logical Calculus of Ideas Immanent in Nervous Activity"
   - Modelaram neurônios como elementos lógicos binários
   - Influenciaram a notação e terminologia de Von Neumann

3. **A experiência prática com o ENIAC:**
   - Mostrou que a programação por cabos era impraticável
   - A necessidade de flexibilidade era clara

---

## Capítulo 2: O "First Draft of a Report on the EDVAC"

### 2.1 Contexto da Criação

Entre fevereiro e junho de 1945, Von Neumann escreveu o documento que se tornaria o mais influente da história da computação. O "First Draft of a Report on the EDVAC" foi circulado em 30 de junho de 1945 por Herman Goldstine para 24 pessoas conectadas ao projeto EDVAC.

**Controvérsia sobre autoria:** O documento listava apenas Von Neumann como autor, o que causou ressentimento em Eckert e Mauchly, que alegavam ter desenvolvido muitas das ideias em discussões anteriores. Esta controvérsia persiste historicamente, mas é inegável que Von Neumann foi quem formalizou e articulou os conceitos de maneira clara e sistemática.

### 2.2 A Estrutura da Arquitetura Proposta

Von Neumann descreveu uma máquina composta de "órgãos", usando terminologia biológica deliberada:

```
ARQUITETURA VON NEUMANN (conforme First Draft)

┌──────────────────────────────────────────────────────────┐
│                                                          │
│    ┌─────────┐                        ┌─────────────┐    │
│    │    I    │                        │      R      │    │
│    │  Input  │                        │   Outside   │    │
│    │  Organ  │                        │  Recording  │    │
│    └────┬────┘                        │   Medium    │    │
│         │                             └─────────────┘    │
│         │                                    ▲           │
│         ▼                                    │           │
│    ┌───────────────────────────┐             │           │
│    │              M            │             │           │
│    │     High-Speed Memory     │             │           │
│    │  (Data AND Instructions)  │             │           │
│    └───────┬────────────┬──────┘             │           │
│           │             │                    │           │
│         ┌─┴────────┐  ┌─┴──────┐             │           │
│         │          │  │        │             │           │
│         ▼          │  │        ▼             │           │
│    ┌────────────┐  │  │   ┌─────────────┐    │           │
│    │     CA     │◄─┘  └──►│     CC      │    │           │
│    │  Central   │         │   Central   │    │           │
│    │ Arithmetic │         │   Control   │    │           │
│    │    Unit    │         │    Unit     │    │           │
│    └────────────┘         └──────┬──────┘    │           │
│                                    │         │           │
│                                    ▼         │           │
│                            ┌──────────────┐  │           │
│                            │      O       │──┘           │
│                            │   Output     │              │
│                            │    Organ     │              │
│                            └──────────────┘              │
│                                                          │
└──────────────────────────────────────────────────────────┘
```

#### 2.2.1 Os Cinco Componentes Fundamentais

**1. Central Arithmetic Unit (CA) - Unidade Aritmética Central:**
- Realiza operações aritméticas (adição, subtração, multiplicação)
- Von Neumann especificou aritmética binária, bit a bit (serial)
- Estimou que uma adição de dois dígitos binários levaria 1 microssegundo
- Uma multiplicação de 30 bits levaria aproximadamente 30² = 900 µs ≈ 1 milissegundo

**2. Central Control (CC) - Controle Central:**
- Busca instruções da memória
- Decodifica instruções
- Coordena a execução sequencial
- Controla o fluxo do programa

**3. Memory (M) - Memória:**
- **Conceito revolucionário:** Armazena TANTO dados QUANTO instruções no mesmo espaço
- Von Neumann argumentou: "É tentador tratar toda a memória como um único órgão, e ter suas partes tão intercambiáveis quanto possível"
- A memória é organizada como um array linear de "words"

**4. Input (I) - Entrada:**
- Recebe dados e programas do mundo externo

**5. Output (O) - Saída:**
- Transmite resultados para o mundo externo ou para o meio de gravação (R)

### 2.3 O Conceito de Memória Unificada: A Revolução

A ideia central — armazenar instruções e dados na mesma memória — tinha implicações profundas:

1. **O programa pode modificar a si mesmo:**
   - Instruções são apenas dados
   - O programa pode computar novos endereços de instruções
   - Possibilita loops com contadores de iteração modificáveis

2. **Flexibilidade de reprogramação:**
   - Mudar o programa significa apenas mudar o conteúdo da memória
   - Não requer reconexão física

3. **Uniformidade de tratamento:**
   - O mesmo mecanismo que lê dados pode ler instruções
   - Simplifica o hardware

### 2.4 Os "E Elements" de Von Neumann

Von Neumann descreveu a construção do computador usando "E elements" (elementos), baseados em neurônios biológicos mas implementados com válvulas. O E element mais simples era:

```
E ELEMENT BÁSICO (AND com entrada de inibição)

     Entrada A ───────────┐
                          ├────► Saída
     Entrada B (inibição) ┘

     Saída = A AND (NOT B)

     Implementação com válvulas:
     
     ┌─────────────────────────────────────┐
     │   +V                                │
     │    │                                │
     │    │                                │
     │    R (resistor de carga)            │
     │    │                                │
     │    ├───────────────► Saída          │
     │    │                                │
     │  ┌─┴─┐                              │
     │  │   │ Triodo 1 (entrada A)         │
     │  └─┬─┘                              │
     │    │                                │
     │  ┌─┴─┐                              │
     │  │   │ Triodo 2 (entrada B-inibição)│
     │  └─┬─┘                              │
     │    │                                │
     │   GND                               │
     └─────────────────────────────────────┘
```

E elements mais complexos tinham um **threshold** (limiar): produziam saída quando o número de entradas positivas igualava ou excedia o limiar, desde que a linha de inibição não estivesse ativa.

### 2.5 O Formato das Instruções

Na seção 14.1 do First Draft, Von Neumann propôs o formato das "orders" (instruções):

**Tipos de instruções incluídos:**
- Operações aritméticas básicas (add, subtract, multiply)
- Movimentação de "minor cycles" entre CA e M (load e store)
- Instrução de seleção condicional baseada no sinal do resultado anterior
- Entrada e saída
- Transferência de controle (jump)

**Estrutura de uma word:**
- Von Neumann calculou quantos bits seriam necessários para cada campo
- Sugeriu instruções "imediatas" onde a word seguinte é o operando
- Discutiu a possibilidade de deixar bits sobressalentes para expansão futura

### 2.6 Por Que Binário? Por Que Orientado a Word?

Von Neumann justificou a escolha do sistema binário:

1. **Simplicidade eletrônica:**
   - Dispositivos de dois estados são mais confiáveis
   - Válvulas funcionam bem como chaves ON/OFF
   - Menos estados = menos chance de erro

2. **Eficiência lógica:**
   - Aritmética binária é mais simples de implementar
   - Cada bit requer apenas um flip-flop
   - Operações podem ser decompostas em passos bit-a-bit

**A orientação a word surgiu de considerações práticas:**

1. **A memória de delay line era serial:**
   - Bits circulavam sequencialmente
   - Natural organizar em grupos (words) para acesso

2. **O processamento era serial:**
   - Para economizar hardware, aritmética era feita bit-a-bit
   - A word representava a unidade mínima de dados significativa

3. **Endereçamento:**
   - Endereçar cada bit individual seria desperdiçador
   - Words são a unidade natural de processamento

---

## Capítulo 3: A Tecnologia de Memória Mercury Delay Line

### 3.1 O Problema da Memória

O maior desafio técnico para implementar a arquitetura Von Neumann era a memória. Eram necessários:
- Velocidade suficiente para acompanhar a CPU
- Capacidade para armazenar programas e dados
- Custo e tamanho razoáveis

Flip-flops de válvula eram rápidos mas caros (36 válvulas por dígito decimal no ENIAC).

### 3.2 A Invenção da Delay Line

A solução veio de uma tecnologia desenvolvida durante a Segunda Guerra Mundial para radar. J. Presper Eckert trabalhou em tubos preenchidos com mercúrio para reduzir "clutter" em telas de radar.

**Princípio de funcionamento:**

```
MERCURY DELAY LINE MEMORY

┌──────────────────────────────────────────────────────┐
│                                                      │
│  Transdutor       Tubo de Mercúrio       Transdutor  │
│  Transmissor       (≈1.5 metros)          Receptor   │
│                                                      │
│    ┌────┐     ════════════════════════     ┌────┐    │
│    │    │ ──▶ Ondas sonoras propagando ──▶ │    │    │
│    │ TX │       através do mercúrio        │ RX │    │
│    │    │     (velocidade ≈ 1450 m/s)      │    │    │
│    └─┬──┘                                  └──┬─┘    │
│      │                                        │      │
│      │        ┌──────────────────────┐        │      │
│      │        │    Circuito de       │        │      │
│      └────────│    Realimentação     │────────┘      │
│               │    (Regenerador)     │               │
│               └──────────────────────┘               │
│                                                      │
└ ─────────────────────────────────────────────────────┘

Sequência temporal:
t=0:    [1][0][1][1][0][0][1][0] ──▶ entrando no tubo
t=Δt:   Bits propagam através do mercúrio
t=τ:    [1][0][1][1][0][0][1][0] ──▶ saindo do tubo
        └── Realimentado para entrada, criando loop perpétuo
```

**Detalhes técnicos:**

1. **Transdutores piezoelétricos:**
   - Cristais de quartzo nas extremidades do tubo
   - Convertem sinais elétricos em ondas ultrassônicas
   - Convertem ondas sonoras de volta em sinais elétricos

2. **Velocidade do som no mercúrio:** ≈ 1450 m/s

3. **Frequência típica:** 5-10 MHz para os pulsos

4. **Tempo de delay:** Para um tubo de 1.5m: τ ≈ 1.5/1450 ≈ 1 milissegundo

5. **Capacidade:** O número de bits armazenados depende do comprimento do tubo e da frequência dos pulsos

**Problemas práticos:**

1. **Temperatura:**
   - A velocidade do som no mercúrio varia com a temperatura
   - Variações de temperatura desalinham o timing
   - Necessário controle de temperatura preciso

2. **Acesso serial:**
   - Só se pode acessar um bit por vez, conforme passa pelo ponto de leitura
   - Para ler uma word específica, deve-se esperar ela "passar"

3. **Peso e toxicidade:**
   - Mercúrio é pesado (cada tubo podia pesar centenas de quilos)
   - Mercúrio é altamente tóxico

### 3.3 Implicações para a Orientação a Word

A natureza serial da memória delay line teve profundas consequências:

1. **Aritmética serial bit-a-bit:**
   - Como bits chegam um de cada vez, é natural processar um bit por vez
   - Economiza hardware (um único somador completo em vez de N)
   
2. **Words como unidades de acesso:**
   - Organizar a memória em words permitia sincronização
   - O fim de uma word marcava um ponto de sincronização conhecido
   - Múltiplas words podiam residir em um único delay line

3. **Endereçamento por word:**
   - Endereçar bits individuais seria ineficiente
   - Words são a menor unidade endereçável

```
Organização típica de um delay line (EDSAC):

│◄─────────────── Um delay line ───────────────►│

┌────┬────┬────┬────┬────┬────┬────┬────┬───────┐
│ W0 │ W1 │ W2 │ W3 │ W4 │ W5 │ W6 │ W7 │ sinc. │
└────┴────┴────┴────┴────┴────┴────┴────┴───────┘
       │
       └── Cada word tem N bits (ex: 35 bits no EDSAC)
       
Bits circulam continuamente: ──────────────────►
                              │              │
                              └──────────────┘
                                realimentação
```

---

## Capítulo 4: O EDVAC (Electronic Discrete Variable Automatic Computer)

### 4.1 Desenvolvimento e Especificações

O EDVAC foi proposto por Eckert e Mauchly em agosto de 1944, antes do First Draft de Von Neumann. O contrato foi assinado em abril de 1946. Entretanto, atrasos significativos fizeram com que o EDVAC só ficasse operacional em 1951 — depois do EDSAC.

**Especificações técnicas:**

| Característica | Valor |
|----------------|-------|
| Tipo | Binário serial |
| Tamanho da word | 44 bits |
| Capacidade de memória | 1.024 words (5.6 KB) |
| Tecnologia de memória | Mercury delay lines |
| Operações | Add, subtract, multiply, programmed division |
| Custo | Aproximadamente $500.000 |

### 4.2 Estrutura da Memória

O EDVAC usava **128 tubos de mercúrio**, organizados em:
- **Duas baterias** de 64 delay lines cada
- **Cada delay line** armazenava 8 words de 44 bits
- **Total:** 1.024 words

```
Organização da memória EDVAC:

Battery 0                          Battery 1
┌──────────────────────┐          ┌──────────────────────┐
│ DL0:  [W0-W7]        │          │ DL64: [W512-W519]    │
│ DL1:  [W8-W15]       │          │ DL65: [W520-W527]    │
│ DL2:  [W16-W23]      │          │ ...                  │
│ ...                  │          │ DL127:[W1016-W1023]  │
│ DL63: [W504-W511]    │          │                      │
└──────────────────────┘          └──────────────────────┘
```

### 4.3 Formato das Instruções EDVAC

Cada instrução EDVAC ocupava uma word de 44 bits:

```
Formato de instrução EDVAC (44 bits):

┌───────────────────────────────────────────────┐
│ Opcode │ Endereço 1 │ Endereço 2 │ Endereço 3 │
│ 4 bits │  10 bits   │  10 bits   │  10 bits   │
└───────────────────────────────────────────────┘
│◄──────────────── 44 bits ────────────────────►│

O formato era "três-endereços" (ou quatro-endereços contando o próximo):
- Endereço do primeiro operando
- Endereço do segundo operando  
- Endereço para armazenar resultado
- (implícito: próxima instrução = PC+1, ou explícito em algumas instruções)
```

### 4.4 Unidades Funcionais do EDVAC

1. **Magnetic tape reader-recorder:** Para E/S
2. **Dispatcher unit:** Recebia instruções do controle e memória, direcionava para outras unidades
3. **Computational unit:** Realizava operações aritméticas
4. **Dual memory unit:** Os dois conjuntos de delay lines

---

## Capítulo 5: O EDSAC (Electronic Delay Storage Automatic Calculator)

### 5.1 Contexto e Desenvolvimento

O EDSAC foi construído na Universidade de Cambridge, Inglaterra, por Maurice Wilkes e sua equipe no Mathematical Laboratory. Wilkes havia participado das Moore School Lectures em 1946, onde aprendeu sobre os conceitos do EDVAC.

**Motivação de Wilkes:** Construir um computador útil para pesquisa universitária, não um projeto de pesquisa em si.

**Timeline:**
- 1947: Início da construção
- 6 de maio de 1949: Primeiro programa executado (cálculo de quadrados)
- 1949-1958: Operação contínua servindo pesquisadores de Cambridge

### 5.2 Especificações Técnicas do EDSAC

| Característica | Valor |
|----------------|-------|
| Tamanho da word | 17 bits (short) ou 35 bits (long) |
| Memória | 512 words (inicialmente) |
| Delay lines | 32 tubos de mercúrio |
| Bits por delay line | 576 bits (16 words de 36 bits cada, com espaçadores) |
| Tempo de ciclo | 1.5 ms para instruções normais; 6 ms para multiplicação |
| Consumo | 11 kW |
| Entrada | Fita de papel de 5 furos |
| Saída | Teleprinter |

### 5.3 Arquitetura do EDSAC

```
ARQUITETURA EDSAC

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│  ┌─────────────┐                     ┌──────────────────┐   │
│  │  Paper Tape │                     │    Teleprinter   │   │
│  │   Reader    │                     │     Output       │   │
│  └──────┬──────┘                     └────────▲─────────┘   │
│         │                                     │             │
│         ▼                                     │             │
│  ┌──────────────────────────────────────────────────────┐   │
│  │                    CONTROL UNIT                      │   │
│  │  ┌────────────────────────────────────────────────┐  │   │
│  │  │            Sequence Control Tank               │  │   │
│  │  │         (instruction register, PC, etc.)       │  │   │
│  │  └────────────────────────────────────────────────┘  │   │
│  └──────────────────────────┬───────────────────────────┘   │
│                             │                               │
│         ┌───────────────────┼───────────────────┐           │
│         │                   │                   │           │
│         ▼                   ▼                   ▼           │
│  ┌────────────┐     ┌────────────────┐     ┌────────────┐   │
│  │ Accumulator│     │     Memory     │     │ Multiplier │   │
│  │    (A)     │◄───►│   (32 delay    │◄───►│  Register  │   │
│  │  78 bits   │     │     lines)     │     │    (R)     │   │
│  └────────────┘     └────────────────┘     └────────────┘   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 5.4 Conjunto de Instruções do EDSAC

O EDSAC tinha um conjunto de instruções simples mas efetivo:

| Mnemônico | Operação | Descrição |
|-----------|----------|-----------|
| A n | Add | Adiciona m[n] ao acumulador |
| S n | Subtract | Subtrai m[n] do acumulador |
| H n | Transfer to R | Carrega m[n] no registrador multiplicador |
| V n | Multiply and Add | Multiplica R por m[n], adiciona ao acumulador |
| N n | Multiply and Subtract | Multiplica R por m[n], subtrai do acumulador |
| T n | Transfer and Clear | Armazena acumulador em m[n], limpa acumulador |
| U n | Transfer | Armazena acumulador em m[n], mantém acumulador |
| C n | Collate (AND) | AND bit-a-bit de m[n] com acumulador |
| R | Shift Right | Desloca acumulador para direita |
| L | Shift Left | Desloca acumulador para esquerda |
| E n | Jump if positive | Salta para n se acumulador ≥ 0 |
| G n | Jump if negative | Salta para n se acumulador < 0 |
| I n | Read | Lê caractere da fita para m[n] |
| O n | Output | Imprime caractere de m[n] |
| F n | Verify | Verifica último caractere impresso |
| X | No operation | Nenhuma operação |
| Z | Stop | Para a máquina e toca sino |

### 5.5 Formato das Instruções EDSAC

```
Instrução EDSAC (17 bits para short word):

┌─────────────────────────────────────────────────┐
│  Opcode │  Unused │   Address   │ Length (S/L) │
│  5 bits │  1 bit  │   10 bits   │    1 bit     │
└─────────────────────────────────────────────────┘

Bit de comprimento:
- S (Short): Operando é word de 17 bits
- L (Long):  Operando é word de 35 bits

Exemplo de codificação:
A 100 S  →  Add word curta do endereço 100 ao acumulador
T 200 L  →  Transfere acumulador para endereço 200 (word longa)
```

### 5.6 Codificação de Caracteres e Mnemônicos

O EDSAC usava código de 5 bits derivado do teleprinter (semelhante a Baudot):

```
Tabela de caracteres EDSAC (modo letras):

Código │ Caractere   Código │ Caractere
───────┼───────────  ───────┼───────────
  00   │    P          16   │   null
  01   │    Q          17   │    F
  02   │    W          18   │    cr
  03   │    E          19   │    D
  04   │    R          20   │   space
  05   │    T          21   │    H
  06   │    Y          22   │    N
  07   │    U          23   │    M
  08   │    I          24   │    lf
  09   │    O          25   │    L
  10   │    J          26   │    X
  11   │   figs        27   │    G
  12   │    S          28   │    A
  13   │    Z          29   │    B
  14   │    K          30   │    C
  15   │   lets        31   │    V
```

**Elegância do design:** Os mnemônicos das instruções foram escolhidos para que o código de 5 bits do caractere correspondesse ao opcode desejado! Assim:

- 'A' tem código 28₁₀ = 11100₂ — usado para ADD
- 'S' tem código 12₁₀ = 01100₂ — usado para SUBTRACT
- 'T' tem código 05₁₀ = 00101₂ — usado para TRANSFER

Isso simplificava a entrada de programas via fita de papel.

---

## Capítulo 6: O Assembly e as Initial Orders do EDSAC

### 6.1 O Primeiro Assembler do Mundo

David Wheeler, estudante de pesquisa trabalhando com Wilkes, criou em maio de 1949 as **"Initial Orders"** — o primeiro assembler do mundo.

**O problema que as Initial Orders resolviam:**

Antes das Initial Orders, para programar o EDSAC seria necessário:
1. Escrever o programa em binário
2. Converter manualmente para padrões de furos na fita
3. Não havia tradução automática de mnemônicos para binário

**A solução de Wheeler:**

As Initial Orders eram um programa de 31 instruções, permanentemente armazenado em **uniselectors** (memória somente-leitura mecânica). Quando o EDSAC era ligado, essas instruções eram automaticamente carregadas nos primeiros 31 endereços da memória.

### 6.2 Funcionamento das Initial Orders

```
FLUXO DAS INITIAL ORDERS

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   FITA DE PAPEL                                             │
│   (programa em forma simbólica)                             │
│                                                             │
│   Formato: [opcode mnemônico][dígitos decimais][S ou L]     │
│   Exemplo: A 100 S                                          │
│            T 200 L                                          │
│            E 50 S                                           │
│                                                             │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    INITIAL ORDERS                           │
│                                                             │
│   1. Lê caractere da fita                                   │
│   2. Se é letra (opcode): extrai 5 bits do opcode           │
│   3. Se são dígitos: monta endereço decimal→binário         │
│   4. Se é S/L: define bit de comprimento                    │
│   5. Combina campos em instrução binária de 17 bits         │
│   6. Armazena na próxima posição de memória disponível      │
│   7. Repete até encontrar indicador de fim                  │
│   8. Transfere controle para o programa carregado           │
│                                                             │
└─────────────────────────────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                 MEMÓRIA PRINCIPAL                           │
│                                                             │
│   [0-30]:  Initial Orders (residentes)                      │
│   [31+]:   Programa do usuário (carregado da fita)          │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### 6.3 Initial Orders 1: O Código

As Initial Orders 1 ocupavam exatamente 31 words. Aqui está uma análise simplificada:

```
Posição │ Instrução │ Função
────────┼───────────┼─────────────────────────────────────────
   0    │   T F     │ (será sobrescrita - usada como dado)
   1    │   E 20 F  │ (será sobrescrita - usada como dado)
   2    │   P 1 F   │ Constante 1 no campo de endereço
   3    │   U 2 F   │ Constante para criar retornos de subrotina
   4    │   A 39 F  │ ┐
   5    │   R 4 F   │ │ Loop para ler dígitos decimais
   6    │   V F     │ │ e montar endereço
   7    │   L 8 F   │ │
   8    │   T F     │ │
   9    │   I 1 F   │ │ Lê próximo caractere
  10    │   A 1 F   │ │
  11    │   S 39 F  │ │
  12    │   G 4 F   │ ┘ Volta se ainda é dígito
  13-18 │   ...     │ Testa caractere, processa opcode
  19-30 │   ...     │ Armazena instrução, controla endereço
```

### 6.4 Initial Orders 2: A Evolução

Em setembro de 1949, Wheeler criou as **Initial Orders 2**, um tour de force de programação em apenas 41 instruções que incluía:

1. **Assembler:** Conversão de mnemônicos para binário
2. **Loader relocador:** Ajustava endereços automaticamente
3. **Suporte a sub-rotinas:** Permitia incluir código de biblioteca

**Inovações das Initial Orders 2:**

- **Códigos de controle:** Caracteres especiais na fita controlavam onde carregar código
- **Relocação automática:** Sub-rotinas podiam ser carregadas em qualquer endereço
- **Coordenação:** Endereços relativos eram ajustados automaticamente

```
EXEMPLO DE PROGRAMA EDSAC COM SUB-ROTINAS

Fita de entrada:
┌─────────────────────────────────────────────────────┐
│ [Código de controle: início]                        │
│ T 64 K        ; K = definir base de coordenação     │
│ G K           ; saltar para início do programa      │
│ [aqui vem código de sub-rotina da biblioteca]       │
│ E Z P F       ; marcador de fim de programa         │
│ [Código do programa principal]                      │
│ A 0 F         ; instruções do programa              │
│ ...                                                 │
└─────────────────────────────────────────────────────┘
```

### 6.5 A Invenção da Sub-rotina: O Wheeler Jump

David Wheeler inventou o conceito fundamental de **sub-rotina** — código reutilizável que pode ser chamado de múltiplos pontos.

**O Problema:**
Como retornar ao ponto correto após executar uma sub-rotina?

**A Solução de Wheeler (Wheeler Jump):**

```
MECANISMO DO WHEELER JUMP

Programa principal:
┌─────────────────────────────────────────────────────────────┐
│ Posição 100:  A 42 F     ; algum código                     │
│ Posição 101:  ...                                           │
│ Posição 102:  ...                                           │
│ Posição 103:  A 103 F    ; Carrega endereço 103 no ACC      │
│ Posição 104:  G 200 F    ; Salta para sub-rotina em 200     │
│ Posição 105:  ...        ; ← Retorno aqui (103+2=105)       │
└─────────────────────────────────────────────────────────────┘

Sub-rotina (em posição 200):
┌─────────────────────────────────────────────────────────────┐
│ Posição 200:  A 2 F      ; Adiciona 2 ao endereço de retorno│
│ Posição 201:  T 220 F    ; Armazena em posição de salto     │
│ Posição 202:  ...        ; corpo da sub-rotina              │
│ Posição 203:  ...                                           │
│ ...                                                         │
│ Posição 220:  E ? F      ; Salto de retorno (? modificado)  │
└─────────────────────────────────────────────────────────────┘

Convenção:
1. Antes de chamar, coloca-se o próprio endereço no acumulador
2. A sub-rotina adiciona 2 (para pular o salto de ida)
3. A sub-rotina modifica sua instrução de retorno final
4. O salto de retorno vai para o endereço calculado
```

**Por que "Wheeler Jump" era necessário:**

- O EDSAC não tinha registrador de retorno dedicado
- Não havia pilha (stack)
- A solução era **código auto-modificável** — a sub-rotina reescrevia sua própria instrução de saída

**Limitações:**
- Sub-rotinas não podiam chamar a si mesmas (recursão impossível sem pilha)
- Múltiplas chamadas aninhadas requeriam cálculo cuidadoso

### 6.6 A Biblioteca de Sub-rotinas do EDSAC

Por volta de 1951, o EDSAC tinha uma biblioteca com 87 sub-rotinas categorizadas:

| Categoria | Exemplos |
|-----------|----------|
| Aritmética de ponto flutuante | Adição, subtração, multiplicação, divisão em FP |
| Números complexos | Operações com parte real e imaginária |
| Divisão | Várias rotinas de divisão inteira |
| Exponenciação | Potências, exponencial |
| Funções | Funções matemáticas diversas |
| Equações diferenciais | Métodos numéricos |
| Funções especiais | Bessel, gamma, etc. |
| Séries de potência | Avaliação de polinômios |
| Logaritmos | Log natural, log base 10 |
| Impressão e layout | Formatação de saída |
| Quadratura | Integração numérica |
| Leitura (input) | Rotinas de entrada |
| Raiz n-ésima | Raiz quadrada, cúbica, etc. |
| Trigonometria | Seno, cosseno, tangente, etc. |
| Contagem | Loops for, while, until |
| Vetores | Operações vetoriais |
| Matrizes | Operações matriciais |

### 6.7 O Primeiro Livro de Programação

Em 1951, Wilkes, Wheeler e Gill publicaram **"The Preparation of Programs for an Electronic Digital Computer"** — o primeiro livro-texto de programação da história.

Conhecido como "WWG", o livro estabeleceu:
- Técnicas de programação estruturada
- Uso de sub-rotinas e bibliotecas
- Depuração sistemática
- Documentação de programas

**Influência do WWG:**
- A IBM adotou o esquema de sub-rotinas de Wheeler para o IBM 701 (1953)
- O TAC (Tokyo Automatic Computer) foi projetado com código de instruções idêntico ao EDSAC para usar a biblioteca do WWG
- Virtualmente todos os sistemas de programação subsequentes têm ancestralidade no WWG

---

## Capítulo 7: A Decisão pela Orientação a Word — Análise Técnica

### 7.1 Fatores que Levaram à Orientação a Word

A orientação a word não foi acaso nem herança — foi uma **decisão calculada** baseada em múltiplos fatores:

#### 7.1.1 Fator 1: Tecnologia de Memória Serial

As delay lines eram inerentemente seriais:

```
Acesso à memória delay line:

Tempo ──────────────────────────────────────────────────►

       │ W0 │ W1 │ W2 │ W3 │ W4 │ W5 │ W6 │ W7 │ W0 │ W1 │
       ▲
       └── Ponto de leitura/escrita

Para acessar W5:
- Se acabou de passar W1, espere W2, W3, W4, então leia W5
- Tempo de espera = função da posição atual

Word como unidade natural:
- Marca pontos de sincronização conhecidos
- Permite cálculo de tempo de acesso
```

#### 7.1.2 Fator 2: Aritmética Serial Bit-a-Bit

Para economizar válvulas (caras e pouco confiáveis), a aritmética era serial:

```
SOMADOR SERIAL DE 1 BIT

      A(i) ────┐
               ├──► Full ──► S(i) (bit de soma)
      B(i) ────┤    Adder
               │
Carry(i-1) ────┘      │
                      ▼
                  Carry(i) ──► [delay de 1 bit] ──► próxima iteração

Operação (para somar duas words de n bits):
- Ciclo 1: soma A(0) + B(0) + 0 → S(0), Carry(0)
- Ciclo 2: soma A(1) + B(1) + Carry(0) → S(1), Carry(1)
- ...
- Ciclo n: soma A(n-1) + B(n-1) + Carry(n-2) → S(n-1), Carry(n-1)

Economia: 1 full adder vs n full adders para soma paralela
```

A word define quantos ciclos são necessários para uma operação aritmética.

#### 7.1.3 Fator 3: Endereçamento Eficiente

```
Comparação de esquemas de endereçamento:

Orientado a BIT:
- Para 32.768 bits, precisa de 15 bits de endereço
- Endereço especifica um único bit
- Operações típicas requerem múltiplos bits → múltiplos acessos
- Ineficiente!

Orientado a WORD (36 bits por word):
- Para 1024 words, precisa de 10 bits de endereço
- Cada acesso retorna 36 bits úteis
- Operações típicas usam uma word inteira
- Muito mais eficiente!
```

#### 7.1.4 Fator 4: Representação Natural de Dados

```
Word de 36 bits pode representar:

Inteiros:
- Signed: -2³⁵ a +2³⁵-1 (±34 bilhões)
- Suficiente para cálculos científicos da época

Instruções:
- Opcode (6 bits): 64 instruções possíveis
- Endereço (12-15 bits): milhares de words
- Modificadores e flags

Caracteres:
- 6 caracteres de 6 bits cada
- Ou 4 caracteres de 9 bits

Ponto flutuante:
- Expoente + mantissa em uma word
```

### 7.2 Por Que Não Orientado a Byte desde o Início?

O byte (8 bits) como unidade fundamental só se popularizou com máquinas posteriores. Na era EDSAC/EDVAC:

1. **Processamento de texto era secundário:**
   - Computadores eram para cálculos numéricos
   - Caracteres de 5-6 bits eram suficientes
   - Não havia necessidade de byte de 8 bits

2. **Hardware não suportava:**
   - Acesso a byte individual em memória serial era impraticável
   - Extrair um byte de uma word requeria masking e shifting

3. **Custo:**
   - Mais granularidade = mais hardware de decodificação
   - Válvulas eram caras

### 7.3 Comparação: ENIAC vs EDVAC vs EDSAC

| Aspecto | ENIAC | EDVAC | EDSAC |
|---------|-------|-------|-------|
| Sistema numérico | Decimal | Binário | Binário |
| Orientação | N/A (não stored-program) | Word (44 bits) | Word (17/35 bits) |
| Memória de programa | Plugues e cabos | Delay line | Delay line |
| Processamento | Paralelo (por dígito) | Serial (bit-a-bit) | Serial (bit-a-bit) |
| Operacional | 1945 | 1951 | 1949 |
| Razão do design | Máquina decimal mecânica | Von Neumann architecture | Von Neumann architecture |

---

# PARTE II: A EVOLUÇÃO DO ASSEMBLY

## Capítulo 8: Assemblers Pós-EDSAC

### 8.1 Disseminação dos Conceitos

Os conceitos do EDSAC se espalharam rapidamente:

**1951-1953: IBM 701**
- Primeiro computador científico comercial da IBM
- Adotou esquema de sub-rotinas de Wheeler
- "Assembler" era chamado de "loader" ou "coding system"

**1952-1954: UNIVAC I**
- Usou assembly similar
- Memória também era delay line (mercury)
- Word de 12 caracteres (72 bits)

### 8.2 Evolução dos Assemblers

```
TIMELINE DA EVOLUÇÃO DOS ASSEMBLERS

1949 ───── EDSAC Initial Orders (Wheeler)
           │  • Primeiro assembler
           │  • Mnemônicos → binário
           │  • Relocação básica
           │
1951 ───── IBM 701 Assembly System
           │  • Pseudo-instruções
           │  • Melhor gerenciamento de símbolos
           │
1954 ───── IBM 704 SAP (Symbolic Assembly Program)
           │  • Labels simbólicos
           │  • Macros primitivas
           │  • Expressões aritméticas em endereços
           │
1957 ───── IBM 704 UASAP (United Aircraft SAP)
           │  • Sistema de macros completo
           │
1959+ ──── Assemblers "Modernos"
           • Macros condicionais
           • Pseudo-ops extensivas
           • Linking e loading separados
```

### 8.3 Inovações nos Assemblers

#### 8.3.1 Labels Simbólicos

**Antes (EDSAC):**
```
T 64 F      ; Endereço numérico explícito
A 100 F     ; Programador deve calcular endereços
E 75 F      ; Mudanças requerem recálculo manual
```

**Depois (SAP e posteriores):**
```
LOOP    LDA DATA      ; Label simbólico
        ADD ONE       ; Referência a símbolo
        STA RESULT    ; Assembler resolve endereços
        JMP LOOP      ; Referência automática
DATA    DC  0         ; Define constante
ONE     DC  1
RESULT  DS  1         ; Define espaço
```

#### 8.3.2 Pseudo-instruções (Diretivas)

```
Exemplo de pseudo-instruções típicas:

ORG  1000       ; Define origem (endereço inicial)
EQU  CONST, 42  ; Define constante simbólica
DC   100        ; Define constante na memória
DS   50         ; Define espaço (50 words)
END  START      ; Marca fim e ponto de entrada
```

#### 8.3.3 Sistema de Macros

**Definição de macro:**
```
MACRO SAVE
    STA TEMP
    STB TEMP+1
    STX TEMP+2
MEND
```

**Uso:**
```
    SAVE          ; Expande para 3 instruções
    JSR SUBR
    ...
```

**Macros com parâmetros:**
```
MACRO PUSH(REG)
    STA STACKPTR
    LDA REG
    STA @STACKPTR
    DCR STACKPTR
MEND
```

### 8.4 O Processo de Assembly em Duas Passadas

A maioria dos assemblers usa duas passadas:

```
ASSEMBLY EM DUAS PASSADAS

PASSADA 1 (Construção da Tabela de Símbolos):
─────────────────────────────────────────────
Código fonte → Analisa labels → Tabela de símbolos

Exemplo:
        ORG  100
START   LDA  X        ; START = 100
        ADD  Y        ; 
        STA  Z        ; 
LOOP    CMP  MAX      ; LOOP = 103
        ...
X       DC   0        ; X = endereço calculado
Y       DC   0        ; Y = X + 1
Z       DS   1        ; Z = Y + 1
MAX     DC   100      ; MAX = Z + 1

Tabela de símbolos após passada 1:
┌────────┬──────────┐
│ Símbolo│ Endereço │
├────────┼──────────┤
│ START  │   100    │
│ LOOP   │   103    │
│ X      │   110    │
│ Y      │   111    │
│ Z      │   112    │
│ MAX    │   113    │
└────────┴──────────┘

PASSADA 2 (Geração de Código):
───────────────────────────────
Código fonte + Tabela → Código binário

Exemplo:
LDA X → opcode(LDA) + endereço(110) → código binário
ADD Y → opcode(ADD) + endereço(111) → código binário
...
```

---

## Capítulo 9: A Necessidade de Linguagens de Alto Nível

### 9.1 O Problema da Produtividade

Por volta de 1953-1954, ficou claro que assembly tinha limitações sérias:

1. **Tempo de programação:**
   - Programar em assembly era lento
   - Típico: 1 instrução por hora de trabalho (incluindo depuração)
   
2. **Custo:**
   - Programadores eram escassos e caros
   - Tempo de computador era caro
   - Até 50% do tempo era gasto em depuração

3. **Portabilidade zero:**
   - Cada máquina tinha assembly diferente
   - Reescrever programas para nova máquina era trabalhoso

4. **Propensão a erros:**
   - Gerenciamento manual de endereços
   - Fácil cometer erros em código repetitivo

### 9.2 Tentativas Anteriores ao Fortran

#### 9.2.1 Speedcoding (IBM 701, 1953)

John Backus desenvolveu Speedcoding para o IBM 701:

- **Interpretador**, não compilador
- Suportava aritmética de ponto flutuante em software
- Programas executavam 10-20x mais lento que assembly

```
Exemplo Speedcoding:
    1  0   X + Y STORE Z
    2  0   Z * 2 STORE W
```

**Problema:** Lentidão inaceitável para cálculos científicos.

#### 9.2.2 A-0 a A-2 (UNIVAC, Grace Hopper)

Grace Hopper e sua equipe desenvolveram:

- **A-0 (1952):** Primeiro "compilador" (mais um linker)
- **A-2 (1953):** Melhorias no A-0
- **MATH-MATIC (1957):** Linguagem algébrica para UNIVAC

#### 9.2.3 Laning and Zierler System (MIT, 1952)

No MIT Whirlwind:
- Entrada de equações em notação algébrica
- Primeiro sistema a demonstrar tradução de fórmulas
- Influenciou o design do Fortran

```
Exemplo Laning-Zierler:
    Y = (A + B) * C
    Z = SQRT(X)
```

---

# PARTE III: FORTRAN — A PRIMEIRA LINGUAGEM DE ALTO NÍVEL DE SUCESSO

## Capítulo 10: O Desenvolvimento do Fortran

### 10.1 A Proposta de Backus

Em novembro de 1953, John W. Backus submeteu à gerência da IBM uma proposta para desenvolver uma alternativa prática ao assembly para o IBM 704.

**Membros da equipe Fortran:**
- John W. Backus (líder)
- Sheldon Best
- Harlan Herrick
- Peter Sheridan
- Roy Nutt
- Robert Nelson
- Irving Ziller
- Harold Stern
- Lois Haibt
- David Sayre
- Richard Goldberg
- Robert Hughes (do Livermore Lab)

### 10.2 O IBM 704: A Máquina Alvo

O Fortran foi desenvolvido especificamente para o IBM 704:

**Especificações do IBM 704:**

| Característica | Valor |
|----------------|-------|
| Word | 36 bits |
| Memória | 4K-32K words (core memory magnético) |
| Registradores | Acumulador (38 bits), MQ (36 bits), 3 index registers |
| Ponto flutuante | Hardware nativo |
| Caracteres | 6 bits cada, 6 por word |
| Ciclo de memória | 12 µs |

**Inovações do 704 que possibilitaram o Fortran:**

1. **Index registers:** Permitiam loops eficientes
2. **Floating-point hardware:** Cálculos científicos rápidos
3. **Core memory:** Acesso aleatório (não serial como delay lines)

### 10.3 Objetivos do Projeto Fortran

Backus estabeleceu objetivos ambiciosos:

1. **Código eficiente:** O código gerado deveria ser quase tão eficiente quanto assembly escrito à mão
2. **Notação algébrica:** Programadores deveriam escrever fórmulas matemáticas
3. **Facilidade de uso:** Reduzir drasticamente o tempo de programação

**O ceticismo da comunidade:**

> "Programmers formed a 'priesthood' used to coding around the highly obscure oddities of early hardware." — Backus

Muitos programadores experientes duvidavam que código gerado automaticamente pudesse ser eficiente.

### 10.4 A Linguagem Fortran Original (1957)

#### 10.4.1 Estrutura de um Programa Fortran

```fortran
C     EXEMPLO DE PROGRAMA FORTRAN ORIGINAL (1957)
C     CALCULA RAIZES DE EQUACAO QUADRATICA
      DIMENSION ROOT(2)
      READ 1, A, B, C
    1 FORMAT(3F10.5)
      D = B*B - 4.0*A*C
      IF (D) 10, 20, 30
   10 WRITE 2
    2 FORMAT(13H RAIZES COMPLEXAS)
      GO TO 100
   20 ROOT(1) = -B / (2.0*A)
      ROOT(2) = ROOT(1)
      GO TO 50
   30 SD = SQRTF(D)
      ROOT(1) = (-B + SD) / (2.0*A)
      ROOT(2) = (-B - SD) / (2.0*A)
   50 WRITE 3, ROOT(1), ROOT(2)
    3 FORMAT(2F15.7)
  100 STOP
      END
```

#### 10.4.2 Elementos da Linguagem

**Tipos de dados:**

| Tipo | Descrição | Convenção de nome |
|------|-----------|-------------------|
| INTEGER | Inteiro | Variáveis I, J, K, L, M, N |
| REAL | Ponto flutuante | Outras letras iniciais |
| (Arrays) | Dimensionados explicitamente | DIMENSION statement |

**Observação importante:** Fortran original NÃO tinha tipos explícitos. O tipo era determinado pela primeira letra do nome:
- I, J, K, L, M, N → INTEGER
- Outras → REAL

**Estruturas de controle:**

```fortran
C     IF ARITMETICO (three-way branch)
      IF (expr) label_neg, label_zero, label_pos

C     GOTO INCONDICIONAL
      GO TO label

C     COMPUTED GOTO
      GO TO (label1, label2, label3), index

C     DO LOOP
      DO 100 I = 1, N
        ... corpo do loop ...
  100 CONTINUE
```

**O IF aritmético:**

O IF aritmético era uma construção peculiar que testava o sinal de uma expressão:

```fortran
      IF (X - Y) 10, 20, 30
C     Se X-Y < 0, vai para 10
C     Se X-Y = 0, vai para 20
C     Se X-Y > 0, vai para 30
```

Esta construção derivava da instrução CAS (Compare Accumulator with Storage) do IBM 704.

**Entrada/Saída:**

```fortran
      READ n, lista_de_variaveis
      WRITE n, lista_de_variaveis
      PRINT n, lista_de_variaveis
      PUNCH n, lista_de_variaveis
    n FORMAT(especificacao)
```

### 10.5 O Compilador Fortran: Uma Obra-Prima de Otimização

O compilador Fortran original era notável por suas técnicas de otimização:

#### 10.5.1 Análise de Fluxo

O compilador analisava o fluxo do programa para otimizar:

```
TÉCNICA: Simulação Monte Carlo em tempo de compilação

O compilador Fortran original usava simulação Monte Carlo 
para estimar a frequência de execução de diferentes caminhos:

1. O statement FREQUENCY dava hints sobre probabilidades
2. O compilador simulava execuções do programa
3. Blocos básicos frequentes eram posicionados para 
   minimizar saltos
4. Código mais executado ficava em posições de memória 
   otimizadas
```

#### 10.5.2 Otimização de Loops

```fortran
      DO 100 I = 1, 1000
        A(I) = B(I) + C(I)
  100 CONTINUE
```

O compilador otimizava:
- Cálculo de endereços de arrays
- Uso de index registers
- Minimização de loads/stores redundantes

#### 10.5.3 Resultados

Quando lançado em abril de 1957:

- Código gerado era tipicamente apenas 2x mais lento que assembly otimizado manualmente
- Para código não otimizado, era frequentemente MAIS rápido
- Tempo de programação reduzido por fator de 5-10x

### 10.6 Fortran II e III

**Fortran II (1958):**
- Adicionou SUBROUTINE e FUNCTION
- Permitiu compilação separada
- COMMON blocks para dados compartilhados

```fortran
      SUBROUTINE SOLVE(A, B, C, X1, X2)
      COMMON /WORK/ TEMP(100)
      ...
      RETURN
      END

      FUNCTION DIST(X, Y)
      DIST = SQRTF(X*X + Y*Y)
      RETURN
      END
```

**Fortran III (1958):**
- Nunca lançado como produto
- Permitia assembly inline
- Features dependentes de máquina

### 10.7 Como o Fortran Funcionava nos Sistemas

#### 10.7.1 Processo de Compilação

```
PROCESSO DE COMPILAÇÃO FORTRAN (IBM 704)

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   CARTÕES PERFURADOS                                        │
│   (programa fonte)                                          │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐   │
│   │ Col 1-5:  Número do statement (labels)              │   │
│   │ Col 6:    Continuação (se não branco)               │   │
│   │ Col 7-72: Statement Fortran                         │   │
│   │ Col 73-80: Identificação (ignorado)                 │   │
│   └─────────────────────────────────────────────────────┘   │
│                                                             │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                 COMPILADOR FORTRAN                          │
│                                                             │
│   Fase 1: Análise léxica e sintática                        │
│   Fase 2: Geração de código intermediário                   │
│   Fase 3: Otimização                                        │
│   Fase 4: Geração de código IBM 704                         │
│                                                             │
│   Características:                                          │
│   - Compilador em assembly (26.000 linhas)                  │
│   - Single-pass onde possível                               │
│   - Tabelas extensas de otimização                          │
│                                                             │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                   CÓDIGO OBJETO                             │
│       (código de máquina IBM 704 em cartões ou fita)        │
│                                                             │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                      LOADER                                 │
│       Carrega código na memória e resolve referências       │
└─────────────────────────┬───────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────┐
│                     EXECUÇÃO                                │
└─────────────────────────────────────────────────────────────┘
```

#### 10.7.2 Gerenciamento de Memória em Fortran

**Fortran NÃO tinha ponteiros no sentido moderno:**

```
Modelo de memória Fortran:

┌────────────────────────────────────────────────────────┐
│  ÁREA COMUM (COMMON blocks)                            │
│  - Compartilhada entre unidades de programa.           │
│  - Endereços fixos determinados em link-time.          │
├────────────────────────────────────────────────────────┤
│  VARIÁVEIS LOCAIS                                      │
│  - Alocação estática                                   │
│  - Endereços fixos em tempo de compilação.             │
│  - NÃO havia alocação dinâmica.                        │
├────────────────────────────────────────────────────────┤
│  CÓDIGO DO PROGRAMA                                    │
│  - Instruções de máquina.                              │
└────────────────────────────────────────────────────────┘

Arrays:
- Tamanho determinado em tempo de compilação
- DIMENSION A(100) → 100 words alocadas estaticamente
- Acesso: A(I) → endereço_base + (I-1) * tamanho_elemento
```

**Por que sem ponteiros?**

1. Simplificava o compilador
2. Otimização era mais fácil (endereços conhecidos)
3. Aplicações científicas não precisavam de estruturas dinâmicas
4. Hardware da época não suportava bem indireção complexa

#### 10.7.3 Passagem de Parâmetros

Fortran usava **call by reference** (passagem por referência):

```fortran
      CALL SWAP(X, Y)
      ...
      SUBROUTINE SWAP(A, B)
      TEMP = A
      A = B
      B = TEMP
      RETURN
      END
```

```
Mecanismo:
- O chamador passa ENDEREÇOS de X e Y
- A e B na subrotina são aliases para X e Y
- Modificações em A/B afetam X/Y diretamente
```

### 10.8 Contribuições do Fortran para Linguagens Modernas

O Fortran estabeleceu conceitos que ainda usamos:

1. **Expressões aritméticas infix:** A = B + C * D
2. **Arrays com índices:** A(I, J)
3. **Loops estruturados:** DO loop
4. **Subprogramas:** SUBROUTINE e FUNCTION
5. **Compilação separada:** Módulos independentes
6. **I/O formatada:** FORMAT statements
7. **Convenção de chamada:** Passagem de parâmetros padronizada

---

# PARTE IV: ALGOL — A LINGUAGEM ACADÊMICA

## Capítulo 11: O Contexto e Desenvolvimento do ALGOL

### 11.1 A Necessidade de um Padrão Internacional

Por volta de 1957, havia preocupação na comunidade acadêmica:

1. **Proliferação de linguagens incompatíveis:**
   - Fortran (IBM)
   - MATH-MATIC (UNIVAC)
   - Outras linguagens proprietárias

2. **Necessidade de comunicação:**
   - Pesquisadores queriam compartilhar algoritmos
   - Publicações científicas precisavam de notação padrão

3. **Independência de fabricantes:**
   - Não depender de uma única empresa
   - Portabilidade entre máquinas

### 11.2 As Organizações Envolvidas

**ACM (Association for Computing Machinery) - EUA:**
- Formou subcomitê em junho de 1957
- Membros incluíam John Backus, John McCarthy, Alan Perlis

**GAMM (Gesellschaft für Angewandte Mathematik und Mechanik) - Europa:**
- Sociedade alemã de matemática aplicada
- Incluía F.L. Bauer, K. Samelson, H. Rutishauser

### 11.3 ALGOL 58 (IAL - International Algebraic Language)

Em maio-junho de 1958, representantes se reuniram em Zurique:

**Participantes americanos:**
- John Backus
- Charles Katz
- Alan Perlis
- Joseph Wegstein

**Participantes europeus:**
- Friedrich Bauer
- Hermann Bottenbruch
- Heinz Rutishauser
- Klaus Samelson

**Resultado:** O "Zurich Report" descrevendo IAL (International Algebraic Language), posteriormente renomeado ALGOL 58.

#### 11.3.1 Inovações do ALGOL 58

1. **Compound statements (blocos):**
```algol
begin
    statement1;
    statement2;
    statement3
end
```

2. **Três níveis de linguagem:**
   - **Reference language:** Definição formal
   - **Publication language:** Para publicações (com símbolos matemáticos)
   - **Hardware representation:** Implementação real

3. **Distinção entre := e =:**
```algol
x := y + z    // Atribuição
if x = y      // Comparação
```

4. **Procedimentos com parâmetros:**
```algol
procedure max(a, b); value a, b; real a, b;
begin
    if a > b then max := a else max := b
end
```

### 11.4 ALGOL 60: A Versão Definitiva

Em janeiro de 1960, uma conferência em Paris produziu o "ALGOL 60 Report".

**Participantes (Paris, 11-16 janeiro 1960):**

Da Europa:
- Friedrich L. Bauer (Alemanha)
- Peter Naur (Dinamarca) — editor do relatório
- Heinz Rutishauser (Suíça)
- Klaus Samelson (Alemanha)
- Bernard Vauquois (França)
- Adriaan van Wijngaarden (Holanda)
- Michael Woodger (Inglaterra)

Dos EUA:
- John W. Backus
- Julien Green
- Charles Katz
- John McCarthy
- Alan J. Perlis
- Joseph H. Wegstein

Alan Perlis descreveu as reuniões:

> "The meetings were exhausting, interminable, and exhilarating. One became aggravated when one's good ideas were discarded along with the bad ones of others."

### 11.5 Características do ALGOL 60

#### 11.5.1 BNF (Backus-Naur Form)

O ALGOL 60 foi o primeiro a usar notação formal para sintaxe:

```bnf
<assignment statement> ::= <variable> := <expression>

<expression> ::= <simple expression> | 
                 <if clause> <simple expression> else <expression>

<if clause> ::= if <Boolean expression> then

<for statement> ::= for <variable> := <for list> do <statement>

<for list> ::= <for list element> | <for list>, <for list element>

<for list element> ::= <expression> | 
                       <expression> step <expression> until <expression> |
                       <expression> while <Boolean expression>
```

#### 11.5.2 Estrutura de Blocos e Escopo

ALGOL 60 introduziu **escopo léxico** com blocos:

```algol
begin
    integer x;    comment x visível neste bloco;
    x := 10;
    begin
        integer y;    comment y visível apenas aqui;
        y := x + 5;   comment x ainda visível;
    end;
    comment y não mais visível aqui;
end
```

#### 11.5.3 Recursão

ALGOL 60 suportava procedimentos recursivos:

```algol
integer procedure factorial(n); value n; integer n;
begin
    if n <= 1 then factorial := 1
    else factorial := n * factorial(n - 1)
end
```

**Nota histórica:** A recursão foi inserida na especificação no último minuto, contra a vontade de alguns membros do comitê!

#### 11.5.4 Call by Name vs Call by Value

ALGOL 60 tinha dois mecanismos de passagem:

**Call by value:**
```algol
procedure p(x); value x; integer x;
begin
    x := x + 1    comment modificação local, não afeta argumento original;
end
```

**Call by name (o padrão):**
```algol
procedure p(x); integer x;
begin
    x := x + 1    comment substitui textualmente, pode ter efeitos estranhos;
end
```

O "call by name" era essencialmente substituição textual, levando ao famoso "Jensen's Device":

```algol
real procedure sum(i, lo, hi, term);
    value lo, hi; integer i, lo, hi; real term;
begin
    real temp;
    temp := 0;
    for i := lo step 1 until hi do
        temp := temp + term;
    sum := temp
end;

comment Uso: soma de i² para i de 1 a 100;
s := sum(j, 1, 100, j*j)    comment j*j reavaliado a cada iteração;
```

### 11.6 Por Que o ALGOL Não Dominou Comercialmente?

#### 11.6.1 Ausência de I/O Padrão

O ALGOL 60 Report **não especificava** entrada e saída:

> "Input and output facilities are not part of the language itself."

Cada implementação tinha seu próprio sistema de I/O incompatível.

#### 11.6.2 Desinteresse de Fabricantes

- IBM já tinha Fortran estabelecido
- Não havia incentivo comercial para promover ALGOL
- Implementações eram acadêmicas, não industriais

#### 11.6.3 Complexidade de Implementação

- Call by name era difícil de implementar eficientemente
- Blocos aninhados com escopo léxico requeriam técnicas sofisticadas
- A pilha de ativação (stack frame) ainda estava sendo desenvolvida

#### 11.6.4 Burocracia Acadêmica

Você acertou ao suspeitar disso:

- Decisões por comitê eram lentas
- Compromissos nem sempre produziam boas decisões
- Implementações divergiam enquanto debates continuavam

### 11.7 O Legado do ALGOL

Apesar do fracasso comercial, ALGOL 60 foi enormemente influente:

```
ÁRVORE DE INFLUÊNCIA DO ALGOL 60

                        ALGOL 60
                           │
         ┌────────┬────────┼────────┬────────┐
         │        │        │        │        │
         ▼        ▼        ▼        ▼        ▼
       Simula    CPL    ALGOL W   Pascal    PL/I
       (1967)  (1963)   (1966)   (1970)   (1966)
         │        │               │
         ▼        ▼               ▼
        C++      BCPL           Modula
      (1979)    (1967)          (1975)
                  │
                  ▼
                  B ──────────► C ──────► C++, Java, C#
                (1969)        (1972)
```

Tony Hoare disse:

> "Here is a language so far ahead of its time that it was not only an improvement on its predecessors but also on nearly all its successors."

---

## Capítulo 12: Conceitos Fundamentais Desenvolvidos com ALGOL

### 12.1 A Pilha de Ativação (Activation Stack)

Para implementar ALGOL 60, foi necessário desenvolver o conceito de **stack frame**:

```
PILHA DE ATIVAÇÃO (Call Stack)

Para cada chamada de procedimento:

┌────────────────────────────────┐  ◄── Topo da pilha
│    Frame de P3                 │
│  ┌──────────────────────────┐  │
│  │ Variáveis locais de P3   │  │
│  │ Parâmetros de P3         │  │
│  │ Endereço de retorno      │  │
│  │ Link para frame anterior │  │
│  └──────────────────────────┘  │
├────────────────────────────────┤
│    Frame de P2                 │
│  ┌──────────────────────────┐  │
│  │ Variáveis locais de P2   │  │
│  │ ...                      │  │
│  └──────────────────────────┘  │
├────────────────────────────────┤
│    Frame de P1                 │
│  ┌──────────────────────────┐  │
│  │ Variáveis locais de P1   │  │
│  │ ...                      │  │
│  └──────────────────────────┘  │
├────────────────────────────────┤
│    Frame do programa principal │
└────────────────────────────────┘  ◄── Base da pilha
```

### 12.2 Display de Dijkstra

Para acessar variáveis de escopos externos em procedimentos aninhados:

```
DIJKSTRA DISPLAY

Procedimento aninhado em 3 níveis:

begin               // Nível 0
    integer a;
    procedure P;    // Nível 1
    begin
        integer b;
        procedure Q;  // Nível 2
        begin
            integer c;
            // Aqui, como acessar 'a' e 'b'?
        end;
    end;
end;

Display (array de ponteiros):
┌─────────┐
│ D[0] ───┼───► Frame nível 0 (contém 'a')
├─────────┤
│ D[1] ───┼───► Frame nível 1 (contém 'b')
├─────────┤
│ D[2] ───┼───► Frame nível 2 (contém 'c')
└─────────┘

Para acessar variável de nível n:
1. Use D[n] para encontrar frame correto
2. Use offset dentro do frame para a variável
```

### 12.3 Técnicas de Compilação

O ALGOL estimulou avanços em compilação:

#### 12.3.1 Análise Sintática Dirigida por Sintaxe

```
COMPILADOR DIRIGIDO POR SINTAXE

Gramática BNF define estrutura
            │
            ▼
Parser reconhece estruturas
            │
            ▼
Ações semânticas geram código

Exemplo:
<assignment> ::= <var> := <expr>

Quando reconhecido:
1. Gera código para avaliar <expr>
2. Gera código para armazenar em <var>
```

#### 12.3.2 Precedência de Operadores

```
TABELA DE PRECEDÊNCIA ALGOL 60

Maior precedência
    ↑
    │  ↑ (exponenciação)
    │  * /  ÷ (multiplicação, divisão)
    │  + - (adição, subtração)
    │  < ≤ = ≥ > ≠ (comparações)
    │  ¬ (NOT)
    │  ∧ (AND)
    │  ∨ (OR)
    │  ⊃ (implicação)
    │  ≡ (equivalência)
    ↓
Menor precedência
```

---

# PARTE V: DE CPL A C

## Capítulo 13: CPL (Combined Programming Language)

### 13.1 Contexto e Motivação

Por volta de 1960-1962, na Universidade de Cambridge e na Universidade de Londres, havia insatisfação com ALGOL 60:

1. **Muito acadêmico:** Não adequado para sistemas reais
2. **Falta de tipos de dados:** Não tinha ponteiros, estruturas
3. **I/O não especificado:** Cada implementação era diferente

Christopher Strachey, Maurice Wilkes, David Barron e outros começaram a desenvolver CPL.

### 13.2 O Projeto CPL

**Timeline:**
- 1962: Início do projeto em Cambridge
- 1963: Paper "The Main Features of CPL" publicado
- 1963-1966: Desenvolvimento lento, linguagem crescendo em complexidade
- 1966: CPL Working Papers (nunca completamente implementado)

### 13.3 Características do CPL

#### 13.3.1 L-values e R-values

Strachey formalizou a distinção crucial entre:

**L-value (Left value):** Local onde um valor pode ser armazenado
**R-value (Right value):** O valor em si

```
Exemplo em CPL (e posteriormente em C):

x := y + 1

x é usado como L-value (lado esquerdo, destino)
y é usado como R-value (lado direito, fonte de valor)

x pode aparecer como R-value também:
z := x + 2    // x é R-value aqui

Mas constantes só podem ser R-values:
5 := x        // ERRO! 5 não é L-value
```

Esta distinção é fundamental para entender ponteiros e referências.

#### 13.3.2 Múltiplos Tipos de Dados

```
Tipos em CPL (planejados):

- integer
- real
- boolean (logical)
- character
- string
- pointer
- array
- function
- structure (agregados)
```

#### 13.3.3 Condicionais Expressivos

```
CPL tinha construções como:

value of
    §   condition1 → expression1
    §   condition2 → expression2
    §   otherwise  → expression3
    §̸

(§ era usado para abrir seções, §̸ para fechar)
```

### 13.4 O Fracasso do CPL

O CPL nunca foi completamente implementado porque:

1. **Linguagem muito grande:** Cresceu demais em features
2. **Recursos insuficientes:** Poucos programadores no projeto
3. **Mudança de hardware:** No meio do projeto, tiveram que migrar do EDSAC 2 para o Titan
4. **Complexidade de implementação:** Tipos complexos eram difíceis

**No entanto**, as ideias do CPL influenciaram profundamente as linguagens seguintes.

---

## Capítulo 14: BCPL (Basic Combined Programming Language)

### 14.1 Martin Richards e a Criação do BCPL

Martin Richards era estudante de doutorado em Cambridge, trabalhando no projeto CPL. Frustrado com a complexidade do CPL, ele decidiu criar uma versão simplificada: BCPL.

**Filosofia de Richards:**

> "Removing those features of the full language which make compilation difficult."

### 14.2 Desenvolvimento do BCPL

**Timeline:**
- 1966: Richards começa o design no Cambridge
- 1967: Primeiro compilador no MIT (IBM 7094 sob CTSS)
- 1967-1979: BCPL se espalha para dezenas de arquiteturas

### 14.3 Características Fundamentais do BCPL

#### 14.3.1 Linguagem sem Tipos (Typeless)

A característica mais distintiva do BCPL: **todos os dados são words**.

```bcpl
LET x = 42         // x é uma word
LET p = @x         // p é uma word (contendo endereço de x)
LET c = 'A'        // c é uma word (contendo código de 'A')

// Todos são tratados uniformemente como padrões de bits
// O significado depende de como são usados
```

**Implicações:**

1. **Simplicidade do compilador:** Não precisa verificar tipos
2. **Flexibilidade:** Qualquer dado pode ser tratado como qualquer coisa
3. **Perigo:** Erros de tipo não são detectados

#### 14.3.2 Operadores de Indireção

```bcpl
!ptr        // Indireção através de ptr (equivalente a *ptr em C)
@var        // Endereço de var (equivalente a &var em C)

// Exemplo:
LET x = 100
LET p = @x      // p aponta para x
!p := 200       // x agora é 200
```

#### 14.3.3 Vetores e Strings

```bcpl
LET vec = VEC 10    // Aloca vetor de 11 words (0..10)
vec!0 := 5          // Primeiro elemento
vec!10 := 15        // Último elemento

// Strings são vetores de bytes empacotados em words
LET str = "Hello"   // String constante
```

#### 14.3.4 Estruturas de Controle

```bcpl
// IF-THEN-ELSE
TEST condition THEN
    statement1
ELSE
    statement2

// SWITCH
SWITCHON expression INTO
$(
    CASE 1: statements; ENDCASE
    CASE 2: statements; ENDCASE
    DEFAULT: statements
$)

// LOOPS
FOR i = 1 TO 100 DO
    statement

WHILE condition DO
    statement

expression REPEATWHILE condition
expression REPEATUNTIL condition
```

### 14.4 O OCODE: Código Intermediário Portável

Uma inovação crucial do BCPL foi o **OCODE** (Object Code):

```
ARQUITETURA DO COMPILADOR BCPL

┌─────────────────────────────────────────────────────────────┐
│                    CÓDIGO FONTE BCPL                        │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                    FRONT-END DO COMPILADOR                  │
│                   (Independente de máquina)                 │
│                  - Análise léxica.                          │
│                  - Análise sintática.                       │
│                  - Geração de OCODE.                        │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                            OCODE                            │
│               (Código intermediário portável)               │
│              - Abstração de máquina de pilha.               │
│             - Independente de arquitetura alvo.             │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                   CODE GENERATOR (Back-end)                 │
│              (Específico para cada arquitetura)             │
│           - Traduz OCODE para código de máquina.            │
│           - Existe um para cada arquitetura alvo.           │
└──────────────────────────────┬──────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────┐
│                 CÓDIGO DE MÁQUINA EXECUTÁVEL                │
└─────────────────────────────────────────────────────────────┘
```

**Instruções OCODE típicas:**

```
OCODE instruction examples:

LOAD    n       ; Carrega valor de posição n na pilha
STORE   n       ; Armazena topo da pilha em posição n
ADD             ; Soma dois valores do topo
SUB             ; Subtrai
MUL             ; Multiplica
DIV             ; Divide
JUMP    label   ; Salto incondicional
JUMPF   label   ; Salta se falso
CALL    proc    ; Chama procedimento
RETURN          ; Retorna de procedimento
```

### 14.5 O Global Vector

BCPL usava um **Global Vector** para comunicação entre módulos:

```bcpl
GLOBAL $(
    var1: 100       // var1 está na posição 100 do global vector
    var2: 101
    proc1: 102
$)
```

```
GLOBAL VECTOR

┌─────────────────────────────────────────┐
│ Posição 0: reservado (sistema)          │
│ Posição 1: reservado                    │
│ ...                                     │
│ Posição 100: var1                       │
│ Posição 101: var2                       │
│ Posição 102: endereço de proc1          │
│ ...                                     │
└─────────────────────────────────────────┘

- Similar ao COMMON do Fortran
- Permite módulos compilados separadamente compartilharem dados
- Linkagem por posição numérica
```

### 14.6 Aplicações do BCPL

O BCPL foi usado em projetos significativos:

1. **TRIPOS:** Sistema operacional portável (ancestral do AmigaOS)
2. **Alto:** Parte do software do Xerox Alto (computador pessoal pioneiro)
3. **OS6:** Sistema operacional experimental em Oxford
4. **MUD1:** O primeiro Multi-User Dungeon (jogo online)

---

## Capítulo 15: A Linguagem Bon

### 15.1 Ken Thompson e o Multics

Ken Thompson trabalhou no projeto Multics nos Bell Labs. Durante esse período, ele criou a linguagem **Bon** (circa 1967).

### 15.2 Características do Bon

Pouco se sabe sobre Bon, pois nunca foi amplamente documentado:

- Linguagem interpretada
- Usada para pequenas utilidades
- Nome possivelmente de "Bonnie" (esposa de Thompson) ou de uma religião cujos rituais envolvem murmúrio de fórmulas mágicas

### 15.3 Relevância do Bon

O Bon não teve influência direta significativa, mas representa a mentalidade de Thompson de criar ferramentas customizadas para seus problemas — mentalidade que levaria ao B e ao Unix.

---

## Capítulo 16: B — O Predecessor Imediato de C

### 16.1 O Contexto: O Nascimento do Unix

Após os Bell Labs abandonarem o Multics em 1969, Ken Thompson queria recriar um ambiente de computação agradável em hardware disponível — um DEC PDP-7 obsoleto.

**O PDP-7:**
- 18 bits por word
- 8K words de memória (18KB)
- Sem sistema operacional útil
- Thompson precisava escrever tudo do zero

### 16.2 A Criação do B

Thompson queria usar uma linguagem de alto nível, não assembly. Ele tentou Fortran primeiro, mas rapidamente desistiu.

**A solução:** Criar sua própria linguagem, baseada em BCPL.

```
GENEALOGIA BCPL → B

BCPL (Richards, 1967)
    │
    │ Thompson "espreme" para caber em 8K
    │ - Remove features complexas
    │ - Simplifica sintaxe
    │ - Adapta para PDP-7
    │
    ▼
B (Thompson, 1969)
```

### 16.3 Diferenças entre BCPL e B

| Aspecto | BCPL | B |
|---------|------|---|
| Palavras-chave | LET, TEST, RESULTIS | auto, extrn, return |
| Blocos | $( ... $) | { ... } |
| Comentários | // ... | /* ... */ |
| Indireção | ! | * |
| Endereço | @ | & |
| Sintaxe geral | Verbosa | Compacta |

### 16.4 Características do B

#### 16.4.1 Estrutura de um Programa B

```b
/* Exemplo de programa B */

main() {
    extrn putchar;
    auto i, str[6];
    
    str[0] = 'H';
    str[1] = 'e';
    str[2] = 'l';
    str[3] = 'l';
    str[4] = 'o';
    str[5] = '*n';  /* *n = newline */
    str[6] = 0;
    
    i = 0;
    while (str[i] != 0) {
        putchar(str[i]);
        i = i + 1;
    }
}
```

#### 16.4.2 Typelessness Herdado do BCPL

B era completamente typeless:

```b
auto x, p;
x = 42;         /* x contém um inteiro */
p = &x;         /* p contém endereço de x */
*p = 100;       /* x agora é 100 */

/* Nenhuma verificação de tipos! */
```

#### 16.4.3 Operadores Incremento/Decremento

Thompson inventou os operadores ++ e --:

```b
auto i;
i = 0;
while (i++ < 10) {
    /* ... */
}
```

**Motivação:** Não foi (como frequentemente se supõe) para usar os modos de auto-incremento do PDP-11 — o PDP-11 nem existia quando B foi criado! Thompson observou que a tradução de `++x` era menor que `x=x+1`.

#### 16.4.4 Operadores de Atribuição Compostos

B introduziu (com sintaxe diferente) os operadores de atribuição:

```b
x =+ y;    /* Equivalente a x = x + y (sintaxe B original) */
x =- y;    /* Equivalente a x = x - y */
x =* y;    /* Equivalente a x = x * y */
```

**Nota:** A sintaxe `=+` foi depois mudada para `+=` em C, pois `x=-1` era ambíguo (era `x = -1` ou `x =- 1`?).

### 16.5 Implementação do B

#### 16.5.1 Compilador TMG

O primeiro compilador B foi escrito usando TMG (TransMoGrifier), um sistema de escrita de compiladores criado por Doug McIlroy.

```
PROCESSO DE DESENVOLVIMENTO DO B

1. McIlroy porta TMG para PDP-7 assembly
2. Thompson usa TMG para criar compilador B
3. Compilador B gera threaded code
4. B é usado para escrever utilitários Unix
```

#### 16.5.2 Threaded Code

O compilador B não gerava código de máquina diretamente, mas **threaded code**:

```
THREADED CODE

Código fonte B:
    x = y + z;

Threaded code gerado:
    ┌───────────────────────┐
    │ addr(routine_load_y)  │
    │ addr(routine_load_z)  │
    │ addr(routine_add)     │
    │ addr(routine_store_x) │
    └───────────────────────┘

Execução:
- Interpretador percorre a lista
- Para cada endereço, salta para a rotina
- Rotina executa operação e retorna ao interpretador

Vantagens:
- Compilador simples
- Código compacto

Desvantagens:
- Overhead de interpretação
- Mais lento que código de máquina nativo
```

### 16.6 Limitações do B que Levaram ao C

Quando o Unix foi portado para o PDP-11 em 1970-1971, as limitações do B ficaram evidentes:

1. **Caracteres:** O PDP-7 tinha words de 18 bits, onde caracteres cabiam bem. O PDP-11 tinha words de 16 bits e era orientado a byte — caracteres de 8 bits não se alinhavam bem.

2. **Ponto flutuante:** Operações de ponto flutuante eram difíceis em uma linguagem typeless onde tudo é uma word.

3. **Ponteiros:** O modelo de B onde ponteiros são índices de words não funcionava bem em máquinas orientadas a byte.

4. **Performance:** Threaded code era lento demais para sistemas.

---

## Capítulo 17: C — A Linguagem que Revolucionou a Computação

### 17.1 A Transição de B para C

A evolução de B para C ocorreu entre 1971 e 1973, principalmente por Dennis Ritchie.

```
TIMELINE B → C

1969    B criado por Thompson para PDP-7
        │
1970    PDP-11 chega aos Bell Labs
        │ Limitações de B ficam evidentes
        │
1971    Ritchie começa a adicionar tipos
        │ "New B" (NB) - versão transitória
        │
1972    Linguagem renomeada para C
        │ Compilador gera código de máquina
        │ Estruturas adicionadas
        │
1973    Unix V4 reescrito em C
        │ Linguagem estabiliza
        │
1978    K&R: "The C Programming Language"
```

### 17.2 O PDP-11: A Máquina que Moldou C

**Especificações do PDP-11:**

| Característica | Valor |
|----------------|-------|
| Word | 16 bits |
| Byte | 8 bits (endereçável!) |
| Registradores | 8 registradores de 16 bits (R0-R7) |
| R6 | Stack Pointer (SP) |
| R7 | Program Counter (PC) |
| Memória | Até 64KB (endereços de 16 bits) |
| Modos de endereçamento | 8 modos × 8 registradores |

**Modos de endereçamento do PDP-11:**

```
Modo        Sintaxe    Descrição
──────────────────────────────────────────────────────
Register    Rn         Operando está no registrador
Register    (Rn)       Operando no endereço em Rn
Indirect
Autoincr    (Rn)+      Usa Rn como endereço, incrementa Rn
Autodecr    -(Rn)      Decrementa Rn, usa como endereço
Indexed     X(Rn)      Rn + X é o endereço
```

Esses modos de endereçamento influenciaram os operadores de C:
- `*p` corresponde ao modo Register Indirect
- `*p++` corresponde ao Autoincrement
- `*--p` corresponde ao Autodecrement
- `p[i]` corresponde ao Indexed

### 17.3 As Inovações Fundamentais do C

#### 17.3.1 Sistema de Tipos

A principal inovação de C sobre B foi o **sistema de tipos**:

```c
/* Declarações com tipos */
int x;          /* inteiro de 16 bits no PDP-11 */
char c;         /* caractere de 8 bits */
float f;        /* ponto flutuante */
double d;       /* ponto flutuante dupla precisão */

int *p;         /* ponteiro para inteiro */
char *s;        /* ponteiro para caractere (string) */

int arr[10];    /* array de 10 inteiros */
```

**Por que tipos eram necessários:**

1. **Caracteres:** No PDP-11, char ocupa 1 byte, não uma word inteira
2. **Ponto flutuante:** Representação diferente de inteiros
3. **Ponteiros:** Aritmética de ponteiros depende do tamanho do tipo apontado

#### 17.3.2 Aritmética de Ponteiros

Em C, aritmética de ponteiros considera o tipo:

```c
int *pi;
char *pc;

pi = (int *)1000;
pc = (char *)1000;

pi + 1;    /* = 1002 (avança 2 bytes, sizeof(int) no PDP-11) */
pc + 1;    /* = 1001 (avança 1 byte) */
```

**Implementação:**

```
ARITMÉTICA DE PONTEIROS

ptr + n  é computado como:  ptr + (n * sizeof(*ptr))

Para int *p (sizeof(int) = 2 no PDP-11):
    p + 1  →  endereço_numérico + 2

Para char *c (sizeof(char) = 1):
    c + 1  →  endereço_numérico + 1

O compilador gera código diferente dependendo do tipo!
```

#### 17.3.3 Estruturas (structs)

C introduziu agregados de dados:

```c
struct point {
    int x;
    int y;
};

struct point p1;
p1.x = 10;
p1.y = 20;

struct point *pp = &p1;
pp->x = 30;     /* equivalente a (*pp).x */
```

**Layout de memória:**

```
struct point (no PDP-11):

Endereço    Conteúdo
────────────────────────
1000        x (2 bytes)
1002        y (2 bytes)
────────────────────────
Total: 4 bytes

Se p1 está no endereço 1000:
    &p1.x = 1000
    &p1.y = 1002
```

#### 17.3.4 Declarações Refletem Uso

Ritchie criou a sintaxe de declaração C com o princípio "declaration reflects use":

```c
int *p;        /* *p é um int, logo p é ponteiro para int */
int a[10];     /* a[i] é um int, logo a é array de int */
int *f();      /* *f() é um int, logo f é função retornando ponteiro para int */
int (*fp)();   /* (*fp)() é int, logo fp é ponteiro para função retornando int */
```

### 17.4 Como C Funciona no PDP-11

#### 17.4.1 Convenção de Chamada

```
CONVENÇÃO DE CHAMADA C NO PDP-11

Antes da chamada:
┌──────────────────────────────────────────┐
│        Stack (cresce para baixo)         │
│                                          │
│         ... variáveis locais ...         │
│  SP →  ┌───────────────────────┐         │
│        │                       │         │
└────────┴───────────────────────┴─────────┘

Chamada: func(a, b, c)

1. Push argumentos (direita para esquerda):
   MOV  c, -(SP)    ; push c
   MOV  b, -(SP)    ; push b
   MOV  a, -(SP)    ; push a

2. Chama função:
   JSR  PC, func    ; salta, salvando retorno

Stack após JSR:
┌──────────────────────────────────────────┐
│         │ endereço de retorno  │         │
│  SP →   ├──────────────────────┤         │
│         │ argumento a          │         │
│         ├──────────────────────┤         │
│         │ argumento b          │         │
│         ├──────────────────────┤         │
│         │ argumento c          │         │
│         └──────────────────────┘         │
└──────────────────────────────────────────┘

Prólogo da função:
   MOV  R5, -(SP)   ; salva frame pointer antigo
   MOV  SP, R5      ; novo frame pointer

Stack após prólogo:
┌──────────────────────────────────────────┐
│       │ variáveis locais     │ ◄── SP    │
│       ├──────────────────────┤           │
│       │ R5 antigo (saved FP) │ ◄── R5    │
│       ├──────────────────────┤           │
│       │ endereço de retorno  │           │
│       ├──────────────────────┤           │
│       │ argumento a          │ 4(R5)     │
│       ├──────────────────────┤           │
│       │ argumento b          │ 6(R5)     │
│       ├──────────────────────┤           │
│       │ argumento c          │ 8(R5)     │
│       └──────────────────────┘           │
└──────────────────────────────────────────┘
```

#### 17.4.2 Exemplo de Compilação

```c
/* Código C */
int sum(int a, int b) {
    int result;
    result = a + b;
    return result;
}
```

```assembly
; Assembly PDP-11 gerado (simplificado)

sum:
    MOV  R5, -(SP)     ; salva frame pointer
    MOV  SP, R5        ; estabelece novo frame
    TST  -(SP)         ; aloca espaço para 'result'
    
    MOV  4(R5), R0     ; carrega 'a'
    ADD  6(R5), R0     ; soma 'b'
    MOV  R0, -2(R5)    ; armazena em 'result'
    
    MOV  -2(R5), R0    ; retorna result em R0
    MOV  R5, SP        ; restaura stack
    MOV  (SP)+, R5     ; restaura frame pointer
    RTS  PC            ; retorna
```

### 17.5 Evolução do C

#### 17.5.1 C Pré-K&R (1972-1978)

O C inicial tinha algumas diferenças:

```c
/* Sintaxe antiga de declaração de função */
int add(a, b)
int a;
int b;
{
    return a + b;
}

/* Não havia 'void' - funções sem retorno não tinham tipo */
/* Não havia 'enum' */
/* Não havia 'const' ou 'volatile' */
```

#### 17.5.2 K&R C (1978)

O livro "The C Programming Language" de Kernighan e Ritchie padronizou a linguagem:

- Definiu a sintaxe e semântica
- Incluiu biblioteca padrão
- Tornou-se o padrão de facto

#### 17.5.3 ANSI C (C89/C90)

O padrão ANSI de 1989 adicionou:

```c
/* Protótipos de função */
int add(int a, int b);  /* declaração com tipos */

/* void */
void procedure(void);   /* não retorna nada, não recebe nada */

/* const e volatile */
const int MAX = 100;
volatile int *io_port;

/* Enumerações */
enum color { RED, GREEN, BLUE };
```

### 17.6 Por Que C se Tornou Dominante

1. **Portabilidade do Unix:** Unix escrito em C → C disponível em todas as máquinas Unix

2. **Eficiência:** C produz código próximo ao assembly

3. **Baixo nível + Alto nível:** Ponteiros e manipulação de bits + funções e estruturas

4. **Simplicidade relativa:** Linguagem pequena, fácil de implementar compiladores

5. **Flexibilidade:** "Dangerous" mas poderosa — o programador está no controle

6. **Ecossistema:** Bibliotecas, ferramentas, comunidade

### 17.7 Conceitos de C Herdados por Linguagens Modernas

```
LEGADO DO C

C (1972)
    │
    ├──► C++ (1979-1983)
    │    - Classes, herança, polimorfismo
    │    - Templates
    │    - STL
    │
    ├──► Objective-C (1984)
    │    - Mensagens estilo Smalltalk
    │    - Base do iOS/macOS
    │
    ├──► Java (1995)
    │    - Sintaxe similar
    │    - Garbage collection
    │    - JVM
    │
    ├──► C# (2000)
    │    - Sintaxe C
    │    - .NET framework
    │
    ├──► JavaScript (1995)
    │    - Sintaxe inspirada em C
    │    - Semântica diferente
    │
    ├──► PHP (1995)
    │    - Sintaxe C-like
    │    - Web scripting
    │
    ├──► Go (2009)
    │    - Criado por Thompson et al.!
    │    - Simplicidade de C
    │    - Concorrência moderna
    │
    └──► Rust (2010)
         - Sintaxe inspirada em C
         - Segurança de memória
```

---

# PARTE VI: A EVOLUÇÃO DO HARDWARE

## Capítulo 18: De Máquinas Orientadas a Word para Orientadas a Byte

### 18.1 A Transição Histórica

```
EVOLUÇÃO DA ORIENTAÇÃO DE HARDWARE

1945-1955: Word-Oriented (tamanho variável)
──────────────────────────────────────────
EDSAC   : 17/35 bits
EDVAC   : 44 bits
UNIVAC I: 72 bits (12 caracteres × 6 bits)

1955-1965: Word-Oriented (convergindo)
──────────────────────────────────────────
IBM 704 : 36 bits
IBM 709 : 36 bits
PDP-1   : 18 bits
CDC 6600: 60 bits

1965-1975: Transição para Byte-Oriented
──────────────────────────────────────────
IBM S/360 (1964): 8-bit byte fundamental
PDP-11 (1970)   : 16-bit word, 8-bit byte addressable
Intel 8008/8080 : 8-bit arquitecture

1975+: Byte-Oriented Dominante
──────────────────────────────────────────
8 bits = 1 byte (padrão universal)
Memória endereçada por byte
Words são múltiplos de bytes
```

### 18.2 IBM System/360: O Padronizador

O IBM System/360 (1964) foi crucial na padronização:

**Características revolucionárias:**

1. **Byte de 8 bits:** Padrão para caracteres
2. **Família de máquinas compatíveis:** Do pequeno ao grande
3. **EBCDIC:** Codificação de 8 bits para caracteres
4. **Registradores de 32 bits:** 16 registradores gerais
5. **Endereçamento por byte:** Cada byte tem endereço único

```
ESTRUTURA DE DADOS IBM S/360

Byte:       8 bits
Halfword:   16 bits (2 bytes)
Word:       32 bits (4 bytes)
Doubleword: 64 bits (8 bytes)

Alinhamento importante:
- Halfword em endereço par
- Word em endereço múltiplo de 4
- Doubleword em múltiplo de 8
```

### 18.3 O PDP-11 e a Influência em C

O PDP-11 foi particularmente influente por seu design elegante:

```
CARACTERÍSTICAS DO PDP-11 QUE INFLUENCIARAM C

1. Orthogonalidade:
   - Qualquer operação com qualquer modo de endereçamento
   - Qualquer registrador pode ser usado igualmente

2. Byte e Word addressing:
   - Instruções para bytes: MOVB, CMPB, etc.
   - Instruções para words: MOV, CMP, etc.

3. Auto-increment/decrement:
   - (R)+  : usa R, depois incrementa
   - -(R)  : decrementa, depois usa R
   - Inspirou ++p e --p em C

4. Stack em hardware:
   - SP (Stack Pointer) dedicado
   - Push/Pop implícitos

5. Condições:
   - Flags N, Z, V, C testáveis
   - Branch condicional flexível
```

### 18.4 A Arquitetura de Von Neumann no PDP-11

O PDP-11 ainda seguia a arquitetura Von Neumann:

```
ARQUITETURA PDP-11 (Von Neumann)

┌─────────────────────────────────────────────────────────────┐
│                                                             │
│                      UNIBUS                                 │
│  ══════════════════════════════════════════════════════     │
│       │           │              │               │          │
│       ▼           ▼              ▼               ▼          │
│  ┌─────────┐ ┌─────────┐  ┌───────────┐  ┌───────────────┐  │
│  │   CPU   │ │ Memory  │  │   Disk    │  │   Terminal    │  │
│  │         │ │ (Core/  │  │Controller │  │  Controller   │  │
│  │ R0-R5   │ │ Semi-   │  │           │  │               │  │
│  │ SP (R6) │ │conductor│  │           │  │               │  │
│  │ PC (R7) │ │         │  │           │  │               │  │
│  │ PSW     │ │  64KB   │  │           │  │               │  │
│  └─────────┘ └─────────┘  └───────────┘  └───────────────┘  │
│                                                             │
└─────────────────────────────────────────────────────────────┘

Características Von Neumann:
- Programa e dados na mesma memória
- Busca sequencial de instruções
- Um barramento para tudo
```

---

# PARTE VII: SÍNTESE E CONCLUSÕES

## Capítulo 19: Resumo da Evolução

### 19.1 A Linha do Tempo Completa

```
TIMELINE COMPLETA: VON NEUMANN A C

1936    Turing: Máquina Universal (conceito teórico)
1944    Von Neumann conhece o ENIAC
1945    First Draft of a Report on the EDVAC
        → Arquitetura de programa armazenado
        → Memória unificada para dados e instruções
        → Base de virtualmente todos computadores modernos

1945    ENIAC operacional (não stored-program)
        → Decimal, programado por cabos
        → Mostrou viabilidade de computação eletrônica

1946    Moore School Lectures
        → Disseminação dos conceitos Von Neumann

1947-49 EDSAC desenvolvido em Cambridge
        → Primeiro computador stored-program útil
        → David Wheeler cria Initial Orders (primeiro assembler)
        → Wheeler Jump (primeira sub-rotina)
        → Wilkes, Wheeler, Gill: primeiro livro de programação

1951    EDVAC finalmente operacional
        → Design influenciou muitos computadores

1953    Speedcoding (Backus, IBM)
        → Primeiro interpretador de alto nível

1954    Proposta do Fortran
1957    Fortran lançado para IBM 704
        → Primeira linguagem de alto nível de sucesso
        → Compilador otimizador
        → Provou que alto nível podia ser eficiente

1958    ALGOL 58 (IAL)
        → Primeiro padrão internacional
        → Blocos, escopo, notação BNF

1960    ALGOL 60
        → Recursão, escopo léxico
        → Influência enorme em design de linguagens

1962-66 CPL desenvolvido em Cambridge/London
        → Tentativa de linguagem prática baseada em ALGOL
        → Introduziu L-values, R-values
        → Nunca completamente implementado

1966-67 BCPL (Martin Richards)
        → Simplificação radical do CPL
        → Typeless, portável via OCODE
        → Usado para sistemas

1969    B (Ken Thompson)
        → BCPL "espremido" para PDP-7
        → Base para Unix inicial

1970    PDP-11 chega aos Bell Labs
        → Byte-addressable, 16 bits
        → Expõe limitações de B

1971-72 C desenvolvido por Ritchie
        → Adiciona tipos a B
        → Estruturas, ponteiros tipados
        → Aritmética de ponteiros correta

1973    Unix reescrito em C
        → Prova conceito de OS em linguagem de alto nível
        → Inicia era de Unix e C

1978    K&R: The C Programming Language
        → Padronização informal
        → Disseminação mundial

1989    ANSI C (C89)
        → Padronização formal
```

### 19.2 Conceitos que Persistem

```
CONCEITOS FUNDAMENTAIS DESENVOLVIDOS NESTA ERA

Da Arquitetura Von Neumann:
├── Programa armazenado
├── Memória endereçável
├── Busca-Decodifica-Executa
├── Aritmética binária
└── Unidade de controle sequencial

Do EDSAC e Assembly:
├── Assembler (tradutor simbólico)
├── Sub-rotinas
├── Biblioteca de código
├── Mnemônicos
└── Labels simbólicos

Do Fortran:
├── Expressões aritméticas
├── Arrays
├── Loops estruturados
├── Compilação otimizada
└── Subprogramas

Do ALGOL:
├── BNF para sintaxe
├── Escopo léxico
├── Blocos estruturados
├── Recursão
└── Stack de ativação

Do CPL/BCPL/B:
├── L-values e R-values
├── Código intermediário portável
├── Sintaxe compacta
├── Operadores ++/--
└── Linguagem de sistemas

Do C:
├── Tipos de dados com tamanhos definidos
├── Ponteiros tipados
├── Estruturas (structs)
├── Aritmética de ponteiros
├── Declaração reflete uso
└── Equilíbrio alto/baixo nível
```

### 19.3 Reflexões Finais

A evolução da arquitetura Von Neumann até a linguagem C representa uma das maiores jornadas intelectuais da história humana:

1. **De conceitos teóricos a prática:** Turing, Von Neumann → ENIAC, EDSAC

2. **De hardware específico a abstração:** Assembly específico → Fortran portável

3. **De programação manual a programação expressiva:** Códigos binários → expressões algébricas

4. **De sistemas acadêmicos a industriais:** ALGOL acadêmico → C prático

5. **De máquinas enormes a onipresença:** ENIAC de 30 toneladas → Unix/C em tudo

O que começou como cálculos balísticos em uma sala de máquinas de 150kW tornou-se a infraestrutura invisível que sustenta a civilização moderna.

---

# APÊNDICES

## Apêndice A: Cronologia Detalhada

```
1936    Turing: "On Computable Numbers"
1937    Atanasoff começa trabalho em computador eletrônico
1941    Zuse Z3 operacional (Alemanha)
1943    Colossus (UK, codebreaking)
1943    Proposta do ENIAC
1944    Von Neumann conhece projeto ENIAC
1945    ENIAC completado (fevereiro)
1945    First Draft on EDVAC (junho)
1946    ENIAC publicamente revelado
1946    Moore School Lectures
1947    Transistor inventado (Bell Labs)
1948    Manchester Baby (primeiro programa armazenado roda)
1949    EDSAC operacional (maio)
1949    Wilkes, Wheeler: Initial Orders
1950    UNIVAC I projetado
1951    EDVAC operacional
1951    UNIVAC I entregue ao Census Bureau
1951    WWG: primeiro livro de programação
1952    IBM 701 anunciado
1953    IBM 701 entregue
1953    Speedcoding (Backus)
1954    Proposta do Fortran
1954    IBM 704 anunciado (floating-point hardware)
1955    Memória de núcleos magnéticos se torna padrão
1956    IBM 704 entregue
1957    Fortran I lançado
1958    ALGOL 58
1958    Fortran II
1959    COBOL especificado
1960    ALGOL 60
1961    IBM 7090 (transistorizado)
1962    Início do projeto CPL
1963    PDP-6 (DEC)
1964    IBM System/360 (revolucionário)
1964    BASIC desenvolvido (Dartmouth)
1965    PDP-8 (primeiro minicomputador popular)
1966    BCPL criado por Richards
1967    Primeiro compilador BCPL (MIT)
1968    ALGOL 68
1969    B criado por Thompson
1969    Unix começa no PDP-7
1970    PDP-11 lançado
1970    Unix portado para PDP-11
1971    Intel 4004 (primeiro microprocessador)
1971    NB (New B) - transição B→C
1972    C emerge como linguagem distinta
1973    Unix V4 reescrito em C
1974    Intel 8080
1978    K&R C publicado
1979    C++ (como "C with Classes")
1983    Turbo Pascal (Borland)
1983    GNU Project começa
1985    C++ 1.0
1987    GCC 1.0
1989    ANSI C (C89)
1991    Linux kernel
1995    Java, JavaScript, PHP
1999    C99
2011    C11
```

## Apêndice B: Tabela de Tamanhos de Word

```
Máquina          Tamanho da Word    Ano
────────────────────────────────────────
ENIAC            10 dígitos dec.    1945
EDVAC            44 bits            1951
EDSAC            17/35 bits         1949
UNIVAC I         72 bits            1951
IBM 701          36 bits            1953
IBM 704          36 bits            1956
IBM 709          36 bits            1958
PDP-1            18 bits            1960
CDC 6600         60 bits            1964
IBM S/360        32 bits            1964
PDP-11           16 bits            1970
VAX-11           32 bits            1977
Intel 8086       16 bits            1978
Intel 80386      32 bits            1985
MIPS R2000       32 bits            1985
SPARC            32 bits            1987
Intel x86-64     64 bits            2003
```

## Apêndice C: Exemplo Comparativo de Código

O mesmo algoritmo (soma de 1 a N) em diferentes níveis:

```
=== CÓDIGO DE MÁQUINA PDP-11 (hexadecimal) ===
005000          CLR R0
012701 000001   MOV #1, R1
012702 000100   MOV #100, R2
060100   L:     ADD R1, R0
005201          INC R1
020102          CMP R1, R2
003774          BLE L
000000          HALT

=== ASSEMBLY PDP-11 ===
        CLR     R0          ; resultado = 0
        MOV     #1, R1      ; i = 1
        MOV     #100, R2    ; N = 100
LOOP:   ADD     R1, R0      ; resultado += i
        INC     R1          ; i++
        CMP     R1, R2      ; compara i com N
        BLE     LOOP        ; se i <= N, repete
        HALT

=== FORTRAN ===
      INTEGER RESULT, I, N
      N = 100
      RESULT = 0
      DO 10 I = 1, N
        RESULT = RESULT + I
   10 CONTINUE

=== ALGOL 60 ===
begin
    integer result, i, n;
    n := 100;
    result := 0;
    for i := 1 step 1 until n do
        result := result + i
end

=== BCPL ===
LET start() = VALOF
$(  LET result = 0
    FOR i = 1 TO 100 DO
        result := result + i
    RESULTIS result
$)

=== B ===
main() {
    auto result, i;
    result = 0;
    i = 1;
    while (i <= 100) {
        result = result + i;
        i = i + 1;
    }
}

=== C ===
int main() {
    int result = 0;
    for (int i = 1; i <= 100; i++) {
        result += i;
    }
    return result;
}
```

---

## Referências Bibliográficas Sugeridas

1. **Von Neumann, J.** (1945). "First Draft of a Report on the EDVAC"
2. **Wilkes, M.V., Wheeler, D.J., Gill, S.** (1951). "The Preparation of Programs for an Electronic Digital Computer"
3. **Backus, J.** (1978). "The History of FORTRAN I, II, and III"
4. **Naur, P.** (1960). "Report on the Algorithmic Language ALGOL 60"
5. **Richards, M.** (1967). "BCPL Reference Manual"
6. **Ritchie, D.M.** (1993). "The Development of the C Language"
7. **Kernighan, B.W., Ritchie, D.M.** (1978). "The C Programming Language"
8. **Campbell-Kelly, M.** (1980). "Programming the EDSAC"
9. **Ceruzzi, P.E.** (2003). "A History of Modern Computing"
10. **Metropolis, N., Howlett, J., Rota, G.C.** (1980). "A History of Computing in the Twentieth Century"

---

*Documento compilado para estudo aprofundado da história da computação, cobrindo aspectos técnicos, eletrônicos, conceituais e históricos desde a arquitetura de Von Neumann até a linguagem C.*
