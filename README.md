# Classificando Descrições de Roubo e Furto

#### Aluno: [Gabriel Cabral](https://github.com/cabralrgabriel )
#### Orientadora: [Manoela Kohler](https://github.com/manoelakohler).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- [Link para o código](https://github.com/cabralrgabriel/Projeto_final_PUC_RIO). 


---

### Resumo

Definir um modelo que classifique um sinistro de automóvel, com base apenas na sua descrição, entre roubo ou furto. 

Abrangeremos algoritmos de Machine Learning, tanto os que comumente chamamos de aprendizado não supervisionado quanto os chamados de aprendizado supervisionado. Importante ressaltar que as duas técnicas não serão concorrentes na resolução do nosso problema. Aqui, elas são complementares. Através da união delas chegamos no nosso resultado.

Como veremos no decorrer do presente trabalho, obtivemos bons resultado para as duas abordagens. Fazendo, assim, com que obtivéssemos uma solução adequada para o problema proposto.


### 1. Introdução

A partir de uma base com descrições de sinistros de roubo ou furto, iremos definir um modelo de classificação para novos sinistros. Para tanto, iremos explorar algoritmos não supervisionados e supervisionados.

No primeiro momento, através de algoritmos não supervisionados, buscaremos a definição das variáveis independentes que usaremos no nosso segundo modelo.

Após essa definição, iremos, através de algoritmos supervisionados, e com os rótulos que definimos no passo anterior, treinar um modelo de classificação.

Teremos assim, um modelo de classificação para novos sinistros. E isso a partir de uma base não rotulada e tendo como única variável a descrição do evento.

### 2. Modelagem

#### 2.1 Gerando as variáveis independentes (modelagem não supervisionada)

Tendo em vista a ausência de variáveis independentes, não é possível treinar, em um primeiro momento, algoritmos de classificação. Antes dessa etapa, iremos explorar a nossa base e treinar algoritmos não supervisionados de segmentação por tópicos. O nosso objetivo nesse momento é definir, através desses tópicos, quando a descrição se refere a um furto e quando ela se refere a um roubo.

Para essa segmentação, treinamos diversos modelos. Todos eles porém passaram por uma etapa de pré-processamento do texto das descrições. Esses pré-processamentos foram: remoção de acentos, transformação do texto para caixa baixa, remoção de caracteres especiais e remoção de stopwords (stopwords são palavras que não acrescentam conhecimento ao texto).

O segundo passo do pré-processamento foi diferente, de acordo com o modelo. Alguns não passaram por mais nenhuma etapa, outros passaram por uma etapa de stemmer e em um terceiro grupo foi aplicado uma lemmatização.

Não vamos focar, aqui, nos modelos dos dois primeiros grupos. O terceiro grupo, com a lemmatização, apresentou os melhores resultados. A lemmatização nada mais é que transformar cada palavra no seu lema. Esse processo pode ser mais custoso do ponto de vista de processamento, porém, no nosso caso, mesmo sendo mais custoso, ele seguiu sendo viável.

Passada toda a parte de pré-processamento, entramos de fato no treinamento do modelo de segmentação. Aqui, escolhemos fazer a modelagem através de Latent Dirichlet Allocation — LDA. Esse é um dos mais populares modelos de segmentação por tópicos que existem na ciência de dados. Basicamente, ele busca definir a probabilidade de um tópico conter um determinado documento com base nas palavras que compõem esse documento. Ele se baseia em dois princípios, que cada documento é uma mistura de tópicos (com mais ou menos identificação com cada tópico) e cada tópico é uma mistura de palavras.

Veremos melhor os resultados dessa etapa do trabalho na sessão 3.1.

#### 2.2 Gerando modelo de classificação (modelagem supervisionada)

Após o sucesso na definição das variáveis independentes para cada descrição, podemos treinar um modelo de classificação e assim conseguirmos inferir novas descrições.

Antes de treinar o modelo em si, fizemos alguns processos para estruturar a base. No caso, repetimos as primeiras etapas de pré-processamento do texto que fizemos na primeira parte do trabalho. São eles: : remoção de acentos, transformação do texto para caixa baixa, remoção de caracteres especiais e remoção de stopwords.

Além desses, uma última etapa de pré-processamento foi realizada. Após a divisão das bases de treino e teste, geramos uma matriz de contagem de palavras. Essa matriz desconsidera a ordem e a gramática das palavras, porém respeita as ocorrências de cada palavra em cada documento.

Tendo gerado essa matriz, podemos então treinar o modelo de classificação. No nosso trabalho, definimos o modelo conhecido como Random Forest. Esses modelos, amplamente utilizados na ciência dos dados, geram n árvores de decisão ao longo do seu treinamento. No final, a resposta da floresta será justamente a classe mais selecionada dentre todas as árvores. Um bom exemplo do funcionamento desse tipo de algoritmo pode ser visto na imagem abaixo:

![image](https://user-images.githubusercontent.com/85505337/137637156-bc8c3166-01c9-41dc-b31f-67a862813e57.png)

Tão logo encerrado o processo de treinamento do modelo, podemos analisar o seu desempenho. O resultado, mais uma vez, se encontra em sessão posterior, na 3.2.


### 3. Resultados

#### 3.1 Resultado da modelagem não supervisionada

No nosso caso, após alguns testes, conseguimos definir 4 tópicos como o número ideal. Esses testes, inevitavelmente passam por tentativa e erro. Como o número de tópicos é arbitrário, embora a literatura aponte algumas possíveis métricas para a definição do melhor número de tópicos, por vezes realizamos a modelagem com alguns números diferentes para esses tópicos e posteriormente devemos analisar os resultados. 

Feito a modelagem conforme algumas configurações e chegando no nosso numero ideal, vamos entender os nossos tópicos. Para tanto, as nuvens de palavras de cada tópico pode nos ajudar.

![image](https://user-images.githubusercontent.com/85505337/137609850-1cb39c51-0295-4848-95fc-6658a4313dd4.png)

Ainda assim, após análise de descrições sorteadas aleatoriamente, conseguimos inferir que os tópicos 0 e 2 se aproximam mais de narrações de roubo enquanto as descrições dos tópicos 1 e 3 mais se parecem com furtos. Conseguimos assim, termos confiança na variável independente que precisamos para realizarmos o treinamento de um modelo de classificação, que nos ajude na inferência de novas descrições.

#### 3.2 Resultado da modelagem supervisionada

Para analisar o resultado dessa etapa, a literatura nos disponibiliza diversas métricas. Aqui, temos quatro possíveis: acurácia, precisão, recall e f1-score.

Dentre eles, podemos destacar a acurácia. Ela é a eficiência geral do modelo, de acordo com a base de teste. Com ela, sabemos quantas previsões corretas foram feitas, diante de todas as previsões feitas.

Abaixo o report com o detalhamento do desempenho do modelo, seguido as métricas citadas:

![image](https://user-images.githubusercontent.com/85505337/137637283-95604b01-fc1e-4438-9ec5-d3cfe3beda4c.png)


### 4. Conclusões

Durante o presente trabalho, pudemos explorar algoritmos de aprendizado não supervisionado, esse num primeiro momento, e também supervisionado. Conseguimos assim, abrangendo ambas as técnicas, gerar um modelo de classificação em uma base a priori sem uma variável independente.

Utilizamos um  algoritmo de Latent Dirichlet Allocation para segmentar em tópicos as nossas descrições. Dessa forma, conseguimos ter confiança em termos uma base classificada, com descrições de roubo e de furto.

Após isso, treinamos um modelo de classificação, agora usando um algoritmo de Random Forest. Conseguimos então, um modelo de classificação para predizer, no momento do recebimento de uma nova descrição, se ela se trata de um roubo ou de um furto.

---

Matrícula: 192.671.181

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
