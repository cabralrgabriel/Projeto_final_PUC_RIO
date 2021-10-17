# Título do Trabalho

#### Aluno: [Gabriel Cabral](https://github.com/cabralrgabriel )
#### Orientadora: [Manoela Kohler](https://github.com/manoelakohler).

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

<!-- para os links a seguir, caso os arquivos estejam no mesmo repositório que este README, não há necessidade de incluir o link completo: basta incluir o nome do arquivo, com extensão, que o GitHub completa o link corretamente -->
- [Link para o código](https://github.com/link_do_repositorio). <!-- caso não aplicável, remover esta linha -->

- [Link para a monografia](https://link_da_monografia.com). <!-- caso não aplicável, remover esta linha -->


---

### Resumo

Definir um modelo que classifique um sinistro de automóvel, com base apenas na sua descrição, entre roubo ou furto.

### 1. Introdução

A partir de uma base com descrições de sinistros de roubo ou furto, iremos definir um modelo de classificação para novos sinistros. Para tanto, iremos explorar algoritmos não supervisionados e supervisionados.

No primeiro momento, através de algoritmos não supervisionados, buscaremos a definição das variáveis independentes que usaremos no nosso segundo modelo.

Após essa definição, iremos, através de algoritmos supervisionados, e com os rótulos que definimos no passo anterior, treinar um modelo de classificação.

Teremos assim, um modelo de classificação para novos sinistros. E isso a partir de uma base não rotulada e tendo como única variável a descrição do evento.

### 2. Modelagem

#### 2.1 Gerando as variáveis independentes

Tendo em vista a ausência de variáveis independentes, não é possível treinar, em um primeiro momento, algoritmos de classificação. Antes dessa etapa, iremos explorar a nossa base e treinar algoritmos não supervisionados de segmentação por tópicos. O nosso objetivo nesse momento é definir, através desses tópicos, quando a descrição se refere a um furto e quando ela se refere a um roubo.

Para essa segmentação, treinamos diversos modelos. Todos eles porém passaram por uma etapa de pré-processamento do texto das descrições. Esses pré-processamentos foram: remoção de acentos, transformação do texto para caixa baixa, remoção de caracteres especiais e remoção de stopwords (stopwords são palavras que não acrescentam conhecimento ao texto).

O segundo passo do pré-processamento foi diferente, de acordo com o modelo. Alguns não passaram por mais nenhuma etapa, outros passaram por uma etapa de stemmer e em um terceiro grupo foi aplicado uma lemmatização.

Não vamos focar, aqui, nos modelos dos dois primeiros grupos. O terceiro grupo, com a lemmatização, apresentou os melhores resultados. A lemmatização nada mais é que transformar cada palavra no seu lema. Esse processo pode ser mais custoso do ponto de vista de processamento, porém, no nosso caso, mesmo sendo mais custoso, ele seguiu sendo viável.

Passada toda a parte de pré-processamento, entramos de fato no treinamento do modelo de segmentação. Aqui, escolhemos fazer a modelagem através de Latent Dirichlet Allocation — LDA. Esse é um dos mais populares modelos de segmentação por tópicos que existem na ciência de dados. Basicamente, ele busca definir a probabilidade de um tópico conter um determinado documento com base nas palavras que compõem esse documento. Ele se baseia em dois princípios, que cada documento é uma mistura de tópicos (com mais ou menos identificação com cada tópico) e cada tópico é uma mistura de palavras.

No nosso caso, após alguns testes, conseguimos definir 4 tópicos como o número ideal. As nuvens de palavras de cada tópico nos ajuda a entender os mesmos.

![image](https://user-images.githubusercontent.com/85505337/137609850-1cb39c51-0295-4848-95fc-6658a4313dd4.png)

Ainda assim, após análise de descrições sorteadas aleatoriamente, conseguimos inferir que os tópicos 0 e 2 se aproximam mais de narrações de roubo enquanto as descrições dos tópicos 1 e 3 mais se parecem com furtos. Conseguimos assim, termos confiança na variável independente que precisamos para realizarmos o treinamento de um modelo de classificação, que nos ajude na inferência de novas descrições.

#### 2.2 Gerando modelo de classificação


### 3. Resultados

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

### 4. Conclusões

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin pulvinar nisl vestibulum tortor fringilla, eget imperdiet neque condimentum. Proin vitae augue in nulla vehicula porttitor sit amet quis sapien. Nam rutrum mollis ligula, et semper justo maximus accumsan. Integer scelerisque egestas arcu, ac laoreet odio aliquet at. Sed sed bibendum dolor. Vestibulum commodo sodales erat, ut placerat nulla vulputate eu. In hac habitasse platea dictumst. Cras interdum bibendum sapien a vehicula.

Proin feugiat nulla sem. Phasellus consequat tellus a ex aliquet, quis convallis turpis blandit. Quisque auctor condimentum justo vitae pulvinar. Donec in dictum purus. Vivamus vitae aliquam ligula, at suscipit ipsum. Quisque in dolor auctor tortor facilisis maximus. Donec dapibus leo sed tincidunt aliquam.

---

Matrícula: 123.456.789

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
