### Sumário

>- 1.....................................................Preparação inicial dos dados.
>
>   - 1.1........................................Importação de bibliotecas.
>
>   - 1.2........................................Definições e funções.
>
>   - 1.3........................................Importação dos DataSets.
>
>   - 1.4........................................Tratamento dos dados (tradução e One Hot Encoding).
>    
>- 2.....................................................Planejamento dos Modelos.
>
>   - 2.1........................................O que queremos prever de fato ?
>
>   - 2.2........................................O que será feito, e como ?
>
>   - 2.3........................................Expectativa e próximos passos.
>
>- 3.....................................................Relação da EDA com a escolha das variáveis.
>
>- 4.....................................................Implementação dos Modelos.
>
>   - 4.1........................................Regressão Linear.
>
>   - 4.2........................................Árvore de Decisão.
>
>   - 4.3........................................KNN (K-Vizinhos mais Próximos).
>
>   - 4.4........................................Gradient Boosting.
>
>   - 4.5........................................Light GBM.
>
>- 5.....................................................Resultados e Métricas.

### Imagens

> Imagem 1..........Mapa de Calor - Correlação das notas de Matemática com escola, internet e ingresso em ensino superior.
>
> Imagem 2..........Mapa de Calor - Correlação das notas de Português com escola, internet e ingresso em ensino superior.
>
> Imagem 3..........Tabela - Resultados e métricas dos Modelos treinados.

# 2 - Planejamento dos Modelos
##### Com os dados analisados e algumas conclusões feitas, o próximo passo é utilizar modelos de Machine Learning com o objetivo de prever as notas dos alunos com base em algumas características.

##### Por exemplo, vimos que tempo de estudo e escola estão correlacionadas com as notas, com base nisso, o quão bem podemos prever a nota que um aluno vai ter, se soubermos apenas o quanto tempo ele estuda e qual escola ele estuda ? Esta é o principal questionamento que vamos responder nesta etapa.
### 2.1 - O que queremos prever de fato ?

##### Queremos prever a variável G1 e G2 (nota do 1º e 2º Trimestre, respectivamente) com base em algumas variáveis, e também confirmar o quão bem podemos prever a variável G3 (nota final) com base nas outras 2 notas.

#### Variáveis a serem usadas nos modelos:
- *failures* - Quantas vezes o aluno repetiu de ano.
- *studytime* - Quantas horas o aluno passa estudando.
- *school* - Qual escola o aluno estuda.
- *Fedu* / *Medu* - Nível de educação da mãe e do pai.
- *higher* - Se o aluno deseja ingressar num Ensino Superior.
- *internet* - Se o aluno tem acesso à internet.

#### Variáveis que não serão usadas nos modelos:
- *traveltime* - Tempo que o aluno gasta se deslocando até a escola.
- *famrel* - O quão boa é a relação familiar do aluno.
- *goout* - O quão frequente ele sai com os amigos.
- *health* - Saúde do aluno.
- *absences* - Quantas vezes o aluno faltou.
- *schoolsup* - Se o aluno teve suporte escolar.
- *address* - Tipo de endereço que o aluno mora.
- *famsize* - Tamanho da família.
### 2.2 - O que será feito, e como ?

##### Vamos utilizar Modelos Supervisionados para previsão, isto é, um modelo onde já temos a resposta (no caso as notas), dividiremos os dados em 2 blocos: Treino e Teste, um bloco será usado para treinar o algoritmo, e o outro bloco será usado para testarmos o quão precisa foram as previsões do modelo.

#### Modelos a serem utilizados:
- *Regressão Linear*
- *Árvore de Decisão*
- *K - Vizinhos mais Próximos*
- *Gradient Boosting*
- *Light GBM*
### 2.3 - Expectativa e próximos passos

##### Fazendo tudo isso, esperamos que os modelos identifiquem fatores-chave e apresentem uma precisão razoável na previsão das notas finais. Iremos captar as métricas e medições de acurácia dos modelos, para podermos avaliar qual deles está performando melhor e sendo mais pertinente para a nossa análise.
# 3 - Relação da EDA com a escolha das variáveis
##### Como foi visto na Análise Exploratória anteriormente, podemos fazer algumas seleções de quais features iremos incluir ou remover.

##### No item 2.1 acima, elencamos as variáveis à serem usadas: *failures* / *studytime* / *school* / *Fedu* / *Medu*

##### Vimos que essas variáveis tem uma correlação positiva com as notas, então serão incluídas nos modelos.
### Através das matrizes abaixo, alguns pontos muito importantes devem ser apontados:

- Alunos com o intuito de ingressar em um ensino superior geralmente tem uma nota um pouco maior.
- Alunos da escola Gabriel Pereira geralmente tem uma nota maior do que os alunos da escola Mousinho da Silveira.
- Coincidentemente, a escola Gabriel Pereira tem uma quantidade de alunos com acesso à internet maior do que a escola Mousinho da Silveira.

### Por causa destas observações, as variáveis *higher* / *internet* também serão inclusas nos modelos.

> ![cd78dbe8-7bf8-4054-914a-caca03d8a522](https://github.com/user-attachments/assets/f1b3e75f-208d-4e64-b0be-9146fc4e872f)
>
> Imagem 1 - Mapa de Calor - Correlação das notas de Matemática com escola, internet e ingresso em ensino superior.

<br><br>

> ![16b7e370-107b-40d5-961e-b9fb7fcaf585](https://github.com/user-attachments/assets/f26f7de5-e9e2-47d6-bb68-c9ec3e3157c5)
>
> Imagem 2 - Mapa de Calor - Correlação das notas de Português com escola, internet e ingresso em ensino superior.

# 4 - Implementação dos Modelos
##### Os modelos a serem treinados são os que já foram mencionados no item 2.2

##### Abaixo contem o código que os executa

##### Importante observar que em cada execução, é gerada um resultado e métricas de cada um, que são adicionados em uma tabela.

##### Essa tabela será o principal objeto de estudo na próxima etapa desta análise, onde iremos dar uma olhada mais afundo nessas métricas, o que elas significam, saber qual algoritmo conseguiu performar melhor e fazer as melhores previsões, assim como o oposto.

# 5 - Resultados e Métricas

> | Matéria     | Modelo             | Features                                           | Variávael Alvo | MSE     | R²   |
> | ----------- | ------------------ | -------------------------------------------------- | -------------- | ------- | ---- |
> | Matemática  | Regressao Linear   | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 12.64	 | 0.08 |
> | Português   | Regressao Linear   | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 7.14	   | 0.17 |
> | Matemática  | Regressao Linear   | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G2             | 12.26	 | 0.14 |
> | Português   | Regressao Linear   | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G2             | 7.43	   | 0.17 |
> | Matemática  | Regressao Linear   | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | ['G1', 'G2']   | 12.45	 | 0.11 |
> | Português   | Regressao Linear   | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | ['G1', 'G2']   | 7.28	   | 0.17 |
> | Matemática  | Regressao Linear   | ['G1', 'G2']                                       | G3             | 4.21	   | 0.79 |
> | Português   | Regressao Linear   | ['G1', 'G2']                                       | G3             | 1.37	   | 0.86 |
> | Matemática  | Arvore de Decisao  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 17.56	 | -    |
> | Português   | Arvore de Decisao  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 8.85	   | -    |
> | Matemática  | Arvore de Decisao  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G2             | 22.97	 | -    |
> | Português   | Arvore de Decisao  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G2             | 10.27	 | -    |
> | Matemática  | Arvore de Decisao  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | ['G1', 'G2']   | 19.47	 | -    |
> | Português   | Arvore de Decisao  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | ['G1', 'G2']   | 9.00	   | -    |
> | Matemática  | Arvore de Decisao  | ['G1', 'G2']                                       | G3             | 4.76	   | -    |
> | Português   | Arvore de Decisao  | ['G1', 'G2']                                       | G3             | 2.10	   | -    |
> | Matemática  | KNN                | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 13.92	 | -    |
> | Português   | KNN                | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 7.71	   | -    |
> | Matemática  | KNN                | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 13.92	 | -    |
> | Português   | KNN                | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 7.71	   | -    |
> | Matemática  | KNN                | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | ['G1', 'G2']   | 15.15	 | -    |
> | Português   | KNN                | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | ['G1', 'G2']   | 7.60	   | -    |
> | Matemática  | KNN                | ['G1', 'G2']                                       | G3             | 5.04	   | -    |
> | Português   | KNN                | ['G1', 'G2']                                       | G3             | 1.79	   | -    |
> | Matemática  | Gradient Boosting  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 13.80	 | -    |
> | Português   | Gradient Boosting  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 7.31	   | -    |
> | Matemática  | Gradient Boosting  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G2             | 14.34	 | -    |
> | Português   | Gradient Boosting  | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G2             | 7.59	   | -    |
> | Matemática  | Gradient Boosting  | ['G1', 'G2']                                       | G3             | 4.76	   | -    |
> | Português   | Gradient Boosting  | ['G1', 'G2']                                       | G3             | 2.10	   | -    |
> | Matemática  | Light GBM          | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 12.12	 | -    |
> | Português   | Light GBM          | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G1             | 7.32	   | -    |
> | Matemática  | Light GBM          | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G2             | 13.25	 | -    |
> | Português   | Light GBM          | ['failures', 'studytime', 'Medu', 'Fedu', 'sch...  | G2             | 7.55    | -    |
> | Matemática  | Light GBM          | ['G1', 'G2']                                       | G3             | 5.39    | -    |
> | Português   | Light GBM          | ['G1', 'G2']                                       | G3             | 1.90    | -    |
>
> Imagem 3 - Tabela - Resultados e métricas dos Modelos treinados.
