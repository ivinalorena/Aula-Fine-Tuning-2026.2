# Desenvolvimento da Aula — Fine-Tuning de LLMs

## Objetivo

Este arquivo contém as instruções e fontes que devem orientar o desenvolvimento de uma aula sobre **Fine-Tuning de Large Language Models (LLMs)**.

O material final deverá incluir:

1. estrutura pedagógica da aula;
2. conteúdo dos slides;
3. sugestões de figuras, diagramas e exemplos;
4. notas de fala detalhadas para cada slide;
5. referências utilizadas.

A aula será ministrada em uma disciplina de **Modelos de Linguagem de Grande Escala**, para alunos de **mestrado e doutorado**, com duração aproximada de **1h30min**.

O conteúdo deve possuir rigor técnico compatível com pós-graduação, mas manter uma progressão didática clara.

---

# Escopo e narrativa da aula

A aula deve responder progressivamente à seguinte pergunta:

> **Como adaptamos um Large Language Model pré-treinado para uma tarefa ou comportamento específico e quais são os trade-offs das diferentes estratégias de Fine-Tuning?**

A narrativa geral deve seguir aproximadamente:

**Pre-training**
→ **Por que adaptar um LLM?**
→ **Fine-Tuning**
→ **Supervised Fine-Tuning (SFT)**
→ **Full Fine-Tuning**
→ **Limitações de custo e memória**
→ **Parameter-Efficient Fine-Tuning (PEFT)**
→ **LoRA**
→ **Quantização + LoRA**
→ **QLoRA**
→ **Quando utilizar cada abordagem?**

Essa sequência deve funcionar como uma **narrativa de problemas e soluções**, e não como uma lista de definições.

Cada nova técnica deve surgir a partir de uma limitação ou necessidade apresentada anteriormente.

---

## 1. Do Pre-training ao Fine-Tuning

Começar brevemente pelo **pre-training**, apenas com o contexto necessário para entender Fine-Tuning.

Responder:

* O que um LLM aprende durante o pre-training?
* Qual é o objetivo de treinamento?
* O que significa dizer que o modelo é "pré-treinado"?
* Por que um modelo pré-treinado ainda pode precisar ser adaptado?

Evitar transformar essa parte em uma aula completa sobre pre-training.

A pergunta que deve conduzir à próxima parte é:

> **Se o modelo já aprendeu linguagem durante o pre-training, por que ainda precisamos treiná-lo novamente?**

---

## 2. Por que adaptar um LLM?

Apresentar situações em que queremos modificar o comportamento de um modelo:

* especialização em domínio;
* execução de tarefas específicas;
* adaptação ao formato de resposta;
* instruction following;
* comportamento especializado.

Utilizar exemplos concretos antes de apresentar formalmente Fine-Tuning.

Diferenciar, quando relevante:

**Prompting vs. RAG vs. Fine-Tuning**

sem aprofundar excessivamente RAG, pois não é o tema central da aula.

A pergunta central deve ser:

> **Quando modificar os parâmetros do modelo é realmente necessário?**

---

## 3. Fine-Tuning

Introduzir Fine-Tuning primeiro intuitivamente e depois formalmente.

Explicar:

* modelo pré-treinado;
* novo dataset;
* função de perda;
* forward pass;
* backpropagation;
* atualização dos parâmetros;
* learning rate;
* epochs.

Utilizar um diagrama simples mostrando:

`Modelo pré-treinado → dados específicos → treinamento → modelo adaptado`

Conectar Fine-Tuning ao conhecimento prévio de treinamento de redes neurais.

---

## 4. Supervised Fine-Tuning (SFT)

Explicar o papel do **Supervised Fine-Tuning** na adaptação moderna de LLMs.

Mostrar:

* estrutura dos dados;
* pares instrução/resposta;
* tokenização;
* labels;
* cálculo da loss;
* atualização dos parâmetros.

Utilizar pelo menos um exemplo concreto de dataset de SFT.

Deixar clara a diferença entre:

**Fine-Tuning como conceito geral**

e

**Supervised Fine-Tuning como uma estratégia específica de adaptação supervisionada.**

---

## 5. Full Fine-Tuning

Apresentar o caso em que **todos ou praticamente todos os parâmetros do modelo são atualizados**.

Explicar:

* vantagens;
* flexibilidade;
* custo computacional;
* memória necessária;
* armazenamento;
* necessidade de manter diferentes versões do modelo.

A explicação deve levar naturalmente à pergunta:

> **Precisamos realmente atualizar bilhões de parâmetros para adaptar o comportamento do modelo?**

Essa pergunta introduz PEFT.

---

## 6. Parameter-Efficient Fine-Tuning — PEFT

Apresentar PEFT como uma **família de estratégias**, e não como uma técnica única.

Explicar a ideia central:

> Adaptar o modelo atualizando apenas uma pequena quantidade de parâmetros.

Mostrar brevemente que existem diferentes estratégias de PEFT, mas aprofundar apenas aquelas necessárias para compreender LoRA.

A pergunta de transição deve ser:

> **Como podemos representar a adaptação do modelo utilizando muito menos parâmetros?**

---

## 7. LoRA

Esta deve ser uma das partes tecnicamente mais importantes da aula.

Construir a explicação em camadas:

### Intuição

Explicar primeiro o problema que LoRA tenta resolver.

### Representação visual

Mostrar uma matriz de pesos original e a atualização representada por matrizes menores.

### Formalização

Introduzir a ideia de **low-rank adaptation** e explicar o significado das matrizes utilizadas.

Se houver equações, explicar:

1. o significado de cada termo;
2. a intuição;
3. o impacto sobre o número de parâmetros treináveis.

### Exemplo

Mostrar conceitualmente a diferença entre:

**Full Fine-Tuning**

e

**LoRA**

em quantidade de parâmetros treináveis e memória.

Ao final, os alunos devem conseguir responder:

> **Por que LoRA consegue adaptar um modelo sem atualizar todos os seus parâmetros?**

---

## 8. De LoRA para QLoRA

Depois de apresentar a economia de parâmetros proporcionada por LoRA, introduzir uma nova pergunta:

> **Mesmo treinando poucos parâmetros, ainda precisamos manter o modelo base inteiro em memória. Podemos reduzir esse custo também?**

Introduzir brevemente **quantização**.

Explicar apenas os conceitos necessários para compreender QLoRA.

Depois apresentar:

**modelo base quantizado + LoRA → QLoRA**

Explicar:

* qual problema QLoRA resolve;
* relação com LoRA;
* redução de memória;
* principais trade-offs.

Evitar transformar essa parte em uma aula completa sobre quantização.

---

## 9. Comparação final

Depois de apresentar as técnicas, construir uma comparação conceitual:

| Estratégia       | Parâmetros atualizados | Memória | Custo | Flexibilidade | Cenário típico |
| ---------------- | ---------------------: | ------: | ----: | ------------- | -------------- |
| Full Fine-Tuning |                        |         |       |               |                |
| LoRA             |                        |         |       |               |                |
| QLoRA            |                        |         |       |               |                |

Os valores e afirmações devem ser fundamentados nas fontes utilizadas.

Não preencher a comparação com números genéricos sem referência.

A discussão deve responder:

> **Quando escolher Full Fine-Tuning, LoRA ou QLoRA?**

---

# Distribuição aproximada dos 90 minutos

Não é necessário seguir rigidamente esta divisão, mas utilize-a como referência:

| Bloco                               | Tempo aproximado |
| ----------------------------------- | ---------------: |
| Motivação + Pre-training            |           10 min |
| Fine-Tuning + SFT                   |           15 min |
| Full Fine-Tuning                    |           10 min |
| PEFT                                |           10 min |
| LoRA                                |           20 min |
| QLoRA                               |           15 min |
| Comparação + discussão + fechamento |           10 min |

Ajuste os tempos se as fontes ou a construção didática indicarem uma distribuição melhor.

**LoRA deve receber mais atenção que uma simples definição**, pois compreender sua motivação e mecanismo é um dos objetivos técnicos importantes da aula.

---

# Princípio de construção dos slides

Evitar slides estruturados apenas como:

`Definição → vantagens → desvantagens`

Sempre que possível, construir sequências como:

**Slide A — Problema**

> Full Fine-Tuning atualiza bilhões de parâmetros.

↓

**Slide B — Pergunta**

> Precisamos atualizar todos eles?

↓

**Slide C — Ideia**

> Parameter-Efficient Fine-Tuning.

↓

**Slide D — Mecanismo**

> LoRA representa a atualização utilizando matrizes de baixo rank.

↓

**Slide E — Consequência**

> Menos parâmetros treináveis e menor custo de adaptação.

Essa estrutura deve fazer com que o aluno entenda **por que uma técnica existe antes de aprender como ela funciona**.

---

# Fontes para desenvolver o conteúdo

## 1. Fontes locais

Os PDFs e demais materiais acadêmicos estão disponíveis em:

`C:\Users\Ivina\Desktop\mestrado\LLM-2026.1\Aula\template\sources`

Antes de desenvolver o conteúdo, examine os arquivos disponíveis nessa pasta e identifique quais são relevantes para cada tópico da aula.

Priorize **papers, livros e documentação técnica** para fundamentar afirmações conceituais.

---

## 2. Fontes externas

Utilize também:

* https://arxiv.org/html/2408.13296v1
* https://www.youtube.com/watch?v=IIvORO248Zs

O vídeo deve servir também como **referência didática**.

Observe:

* como o professor motiva um conceito antes de defini-lo;
* progressão da explicação;
* exemplos e analogias;
* transições;
* uso de figuras;
* equilíbrio entre intuição e formalização.

Não copie literalmente sua apresentação. Extraia os princípios didáticos que possam ser adaptados à aula.

---

# Uso das fontes e rigor técnico

Sempre diferencie:

**Fonte científica → fundamentação técnica**

**Material didático/vídeo → inspiração pedagógica**

Para técnicas importantes, procure e utilize preferencialmente suas fontes primárias.

Exemplos:

* LoRA → paper original;
* QLoRA → paper original;
* demais métodos → trabalhos que introduziram ou formalizaram a abordagem.

Não sustente afirmações técnicas importantes exclusivamente em vídeos ou fontes secundárias quando houver literatura científica primária disponível.

---

# Rastreabilidade

Para cada slide, registre nas notas:

`Fontes: [paper/material utilizado]`

Para figuras:

`Figura adaptada de: [referência]`

ou:

`Figura própria baseada em: [referências]`

Não invente referências nem associe uma afirmação a uma fonte que não a sustente.

---

# Notas de fala

As notas são tão importantes quanto os slides.

Para cada slide, produzir:

### Objetivo

O que os alunos devem compreender.

### Fala sugerida

Como explicar oralmente o conteúdo sem simplesmente ler o slide.

### Conceito-chave

A ideia que deve permanecer após o slide.

### Transição

Como conectar naturalmente ao próximo slide.

### Possíveis dúvidas

Perguntas que alunos de mestrado/doutorado podem fazer.

As notas devem me ajudar a **compreender e ensinar**, e não ser um texto para decorar.

---

# Regra principal

O objetivo não é cobrir todas as técnicas de Fine-Tuning.

O objetivo é fazer com que, ao final dos 90 minutos, os alunos consigam construir mentalmente a sequência:

**"Temos um modelo pré-treinado."**

→ **"Queremos adaptá-lo."**

→ **"Podemos atualizar seus parâmetros com SFT."**

→ **"Atualizar tudo é caro."**

→ **"PEFT tenta reduzir esse custo."**

→ **"LoRA faz isso representando a adaptação de forma eficiente."**

→ **"QLoRA reduz também o custo de manter o modelo base em memória."**

→ **"A estratégia adequada depende do problema, dos recursos e do nível de adaptação necessário."**

Priorizar sempre:

**compreensão > quantidade**

**problema → solução > lista de técnicas**

**intuição → mecanismo → formalização → consequência**
