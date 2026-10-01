# Fontes e decisões editoriais da aula

## Versão de 120 minutos — 23/09/2026

Foram incorporados somente os blocos de LoRA no modelo inteiro e diagnóstico de falhas: 6 slides, 30 minutos planejados de exposição, sem atividades dependentes da turma. Total: 35 slides, 114 minutos de conteúdo e 6 de margem. As seções históricas abaixo conservam a numeração da versão a que se referem.

| Numeração anterior (29 slides) | Numeração atual |
| --- | --- |
| 1–20 | 1–20 |
| Inserções LoRA | 21–23 |
| 21–26 | 24–29 |
| Inserções diagnóstico | 30–32 |
| 27–29 | 33–35 |

### Conteúdo e rastreabilidade das inserções

- **21 — Localização da LoRA:** esquema vetorial próprio de atenção e MLP. Fundamentação: [Hu et al., §4.2 e §7.1](https://arxiv.org/html/2106.09685) e Dettmers et al. O esquema omite normalizações, conexões residuais e detalhes das cabeças, explicitamente; destacar Q e V não significa liberar seus pesos originais.
- **22 — Contagem total:** derivação própria para 32 camadas com dois alvos quadrados de 4096 por camada, rank 8, fatores independentes e nenhum outro parâmetro treinável. Total de 4.194.304 parâmetros; BF16 ocupa 8 MiB somente em valores dos fatores. Dobrar apenas o rank dobra esses valores. Não é uma arquitetura identificada nem uma medição de memória total.
- **23 — Orçamento fixo:** comparação hipotética própria entre dois alvos com rank 16 e quatro alvos com rank 8, resultando em 8.388.608 parâmetros em ambos. Hu et al., §7.1 e Tabela 5, motivam a questão de distribuir um orçamento entre módulos. O slide não reproduz os resultados experimentais dessa tabela nem atribui superioridade a qualquer configuração.
- **30 — Loss e tarefa:** estudo de caso hipotético criado para a aula. A investigação separa validade de formato, classificação, qualidade de rótulos e generalização. Nenhum desempenho medido é apresentado; taxa de sucesso completo usa todos os chamados como denominador.
- **31 — Regressão:** caso hipotético de classificação versus resumo. Fonte científica: Dong et al. (2024), *How Abilities in Large Language Models are Affected by Supervised Fine-tuning Data Composition*, ACL, pp. 177–198. [Artigo](https://aclanthology.org/2024.acl-long.12/) e [PDF](https://aclanthology.org/2024.acl-long.12.pdf). O trabalho motiva investigar composição e sequência de treinamento; não prova que toda regressão observada seja esquecimento. As opções de diagnóstico e o exemplo são elaboração didática própria.
- **32 — Comparação experimental:** protocolo proposto para a aplicação da aula, distinguindo efeito de uma escolha e melhor solução dentro de um orçamento. Não constitui benchmark executado. A discussão da tabela de QLoRA refere-se agora ao slide **28**, ainda identificado como Tabela 4 do arXiv v1; na publicação final da NeurIPS, os números correspondem à Tabela 3.

As falas literais, explicações de contas e transições estão em `../falas_aula.txt`; objetivos, dúvidas e fontes por slide estão em `../apoio_docente.txt`. Os exemplos são conduzidos pela docente. Não foi acrescentado um bloco autônomo de avaliação por macro-F1.

## Análise do artigo enviado em 17/09/2026

O [PDF indicado](https://arxiv.org/pdf/2305.14314) é o artigo original de QLoRA, já incluído na bibliografia. Sua relevância é central para o bloco de quantização e adaptação eficiente. A consulta retornou a versão v1, de 23/05/2023; para rastrear os números desta revisão, usamos o [PDF versionado](https://arxiv.org/pdf/2305.14314v1).

A aula já apresentava o mecanismo; a revisão acrescenta evidência quantitativa ao **slide 25**, com um recorte da **Tabela 4, página 8**. O roteiro literal explica a leitura da tabela e distingue a comparação com LoRA BF16 de uma comparação com Full FT. A referência existente foi mantida, sem duplicação. As 29 páginas e o tempo planejado permanecem.

O recorte mostra as colunas FLAN v2 de 7B e 65B e conserva a média das oito configurações originais, explicitamente identificada. O alerta sobre interpretação da média é uma análise didática própria. Não foram acrescentadas atividades que dependam da turma.

Para atualizar apenas esse slide no LaTeX sem sobrescrever os outros, execute `python code/atualizar_evidencia_qlora.py` na pasta `Aula/template`; depois atualize as falas com `python code/gerar_aula.py --somente-roteiro` e recompile.

## Materiais locais examinados

| Material | Identificação no documento | Uso |
| --- | --- | --- |
| `LLM Finetuning Techniques.pdf` | Tianqi Chen e Zhihao Jia; 15-779, Lecture 17; capa datada de 2025 | Motivar custo, localizar famílias PEFT, distinguir prompting e prompt tuning e contextualizar quantização. |
| `Generative AI – Adapting LLMs with Parameter-Efficient Fine-Tuning.pdf` | Transcrição MIT OCW, Rama Ramakrishnan, 15.773, Spring 2024, Lecture 10 | Progressão didática: exemplos de comportamento → treinamento → custo → matrizes de atualização. |

As extrações `llm_finetuning_extraido.txt` e `peft_extraido.txt` facilitam localizar os trechos. Equações e figuras podem não sobreviver à extração textual; por isso a formalização central foi conferida nas fontes primárias. O PDF do MIT é uma transcrição, não uma coleção de slides.

Não foram reproduzidas generalizações dos materiais didáticos como “sempre cabe em uma GPU”, “fine-tuning só altera poucos pesos” ou “mesmos recursos do treino do zero”. A aula separa custo por passo, número de passos, memória e armazenamento; atualização de baixo rank pode ser densa.

## Fontes científicas

| Fonte | Localizador | Uso na aula |
| --- | --- | --- |
| Hu et al. (2022), *LoRA: Low-Rank Adaptation of Large Language Models*, ICLR; preprint de 2021 | [Artigo](https://arxiv.org/abs/2106.09685), §4.1, Fig. 1 e §7 | Fatores, dimensões, inicialização, escala, merge e limites empíricos da hipótese de baixo rank. Slides 10–21 e síntese. |
| Dettmers et al. (2023), *QLoRA: Efficient Finetuning of Quantized LLMs*, NeurIPS | [Artigo](https://arxiv.org/abs/2305.14314), §2–4 e apêndice G | Gradientes com base congelada, armazenamento/cálculo, NF4, double quantization, paged optimizers e memória. Slides 11–15 e 22–28. |
| Ouyang et al. (2022), *Training language models to follow instructions with human feedback*, NeurIPS | [Artigo](https://arxiv.org/abs/2203.02155), etapa SFT | Demonstrações e adaptação para instruções. SFT é separado de RLHF e da escolha de parâmetros treináveis. Slides 2 e 6–8. |
| Brown et al. (2020), *Language Models are Few-Shot Learners*, NeurIPS | [Artigo](https://arxiv.org/abs/2005.14165) | Contexto autoregressivo e exemplos no prompt sem atualização de pesos. Slides 3–4 e 8. |
| Houlsby et al. (2019), *Parameter-Efficient Transfer Learning for NLP*, ICML | [Artigo](https://proceedings.mlr.press/v97/houlsby19a.html) | Exemplo primário de adapters e base congelada. Slides 13–15. |
| Lewis et al. (2020), *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks*, NeurIPS | [Artigo](https://arxiv.org/abs/2005.11401) | Contextualizar recuperação e geração, sem transformar a aula em exposição sobre RAG. Slides 4 e 28. |
| Kingma e Ba (2015), *Adam: A Method for Stochastic Optimization*, ICLR | [Artigo](https://arxiv.org/abs/1412.6980) | Estados de primeiro e segundo momentos; distinção da equação ilustrativa de SGD. Slides 5 e 11. |
| *The Ultimate Guide to Fine-Tuning LLMs from Basics to Breakthroughs*, versão 1.0 (2024) | [Revisão indicada nas instruções](https://arxiv.org/html/2408.13296v1), seções de preparação de dados e avaliação | Mapa complementar de temas; não substitui os artigos originais. Slide 9 e inventário. |

Os nomes abreviados no arquivo `../apoio_docente.txt` correspondem às entradas acima. As referências dos slides são apresentadas diretamente, com links nas duas páginas finais; não dependem de Biber para aparecer no PDF. Na revisão da abertura, pré-treinamento passou ao slide 2 e motivação ao slide 3. Após a retirada dos antigos slides 26 e 28, a comparação passou ao 26, o fechamento ao 27 e as referências aos slides 28–29. As faixas na tabela acima referem-se à versão original. O arquivo `../falas_aula.txt` contém somente o roteiro oral, com pausas e ações entre colchetes.

## Vídeo indicado: acesso limitado

O acesso direto a [este vídeo](https://www.youtube.com/watch?v=IIvORO248Zs) retornou erro na ferramenta de navegação. Não foi possível verificar seu áudio, suas figuras ou sua transcrição nesta sessão. Foi localizado e consultado o [repositório público do curso codebasics](https://github.com/codebasics/llm-fine-tuning-crash-course), mas ele não substitui assistir ao vídeo e não fundamenta as afirmações técnicas da aula.

Consequentemente, não se afirma que a progressão do vídeo foi analisada. A inspiração pedagógica efetivamente examinada veio da transcrição local do MIT: motivar com um comportamento concreto, recuperar o treino de redes neurais, introduzir o gargalo de memória e construir a intuição das matrizes antes da formalização. Os exemplos e desenhos da apresentação são próprios.

## Contas e figuras próprias

- Slide 5: ciclo de adaptação; desenho vetorial próprio.
- Slide 8: esquema de tokens e máscara, sem IDs reais de tokenizer; loss apenas na resposta é uma escolha explícita da aula.
- Slide 11: 7 bilhões de parâmetros, GB decimais, 2 bytes de pesos + 2 de gradientes + 4 de cópia mestre + 8 de momentos = 16 bytes/parâmetro. Subtotal de 112 GB; não é medição e exclui ativações e buffers.
- Slide 12: dez checkpoints de pesos BF16 de 14 GB = 140 GB de armazenamento.
- Slide 15: caminho de gradiente com camada congelada; desenho próprio, não uma arquitetura literal de Transformer.
- Slides 17–18: dimensões dos fatores e ramos LoRA; desenhos próprios baseados na Fig. 1 e §4.1 de Hu et al. Escala omitida no slide 17 e introduzida no 18.
- Slide 19: matriz 4096×4096 e rank 8; 16.777.216 versus 65.536 parâmetros; 0,390625%; 32 MiB de base e 128 KiB de fatores BF16. São contagens locais, não medições de toda a rede.
- Slide 22: quantização uniforme ilustrativa, explicitamente diferente de NF4.
- Slide 24: 14 GB em BF16 versus carga ideal de 3,5 GB em quatro bits, antes de metadados e partes não quantizadas.
- Slide 25: contém o resultado de viabilidade de 65B em GPU de 48 GB e o recorte da Tabela 4 descrito acima. Resultados relatados por Dettmers et al.; não foram reproduzidos nesta tarefa.
- Antigos slides 26 e 28: retirados na versão expositiva, que não depende de respostas da turma.

## Sugestões de uso dos visuais

Os diagramas já estão implementados em TikZ e permanecem vetoriais no PDF. No slide 17, desenhar também no quadro B de 3×1 e A de 1×4; no slide 18, percorrer as duas rotas com o cursor; no slide 19, desenvolver o c?lculo passo a passo pela docente. Essas dinâmicas substituem animações e dispensam acesso à internet durante a aula.
