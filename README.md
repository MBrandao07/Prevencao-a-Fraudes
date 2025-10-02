# Entendimento do Negócio

Com o aumento das transações eletrônicas em pontos de venda físicos, o uso de cartões de crédito tornou-se essencial no cotidiano. No entanto, essa facilidade também trouxe um aumento nas fraudes, incluindo transações fraudulentas em terminais físicos comprometidos e ataques direcionados a esses locais.

Fraudes em terminais físicos prejudicam financeiramente as instituições e afetam a confiança dos consumidores, além de impactar negativamente a reputação das empresas envolvidas. Por isso, a PoDShield enfrenta uma demanda crescente por soluções automatizadas que possam examinar rapidamente grandes volumes de transações e identificar padrões de fraude em terminais físicos.


**Objetivo:**

Desenvolver um modelo de machine learning para detecção de fraudes em cartões de crédito, focado exclusivamente em transações realizadas em terminais físicos.

---------------------------------------------------------------

# Entendimento dos Dados

Temos 4 tabelas que serão utilizadas como base de dados, sendo elas:

- Terminal

- Train

- Test

- Customer

Essas tabelas se relacionam da seguinte maneira:

![imagem](Imagens/relacao_planilhas_fraude.jpg)


----------------------------------------------------------------

# Análise Exploratória dos Dados

Essas são algumas das informações que foram extraídas das bases:

- As bases não possuem valores nulos

- A base de treino tem 291231 transações

- A base de teste tem 226731 transações

- Temos um total de 998 clientes diferentes

- Temos um total de 1994 terminais diferentes

- A taxa de fraude média é de 2,26%

- Temos 5 meses de histórico na base treino

- O mês com a maior taxa de fraude apresentou um valor de 2,42% 

- O mês com a menor taxa de fraude apresentou um valor de 2,07%

- Existe um terminal onde a taxa de fraude é de 41,49% e foram realizadas 94 transações

- O terminal com mais transações fez 495 transações e apresentou apenas 0,81% de taxa de fraude

- Cerca de 75,15% dos clientes já esteve envolvido em uma transação fraudulenta


Além disso, também foi verificada a distribuição dos clientes e dos terminais em um mapa global (Essa distribuição pode ser conferida no primeiro notebook do caso).

---------------------------------------------------------------------

# Preparação dos dados

Na etapa de preparação dos dados foram realizadas algumas etapas, sendo a primeira o join das bases Train e Test com as bases Customer e Terminal para colocar todas as informações juntas.

Foi realizada uma etapa de Feature Engineering, onde foram criandas diversas novas variáveis, como:

- Periodo do dia

- Hora do dia

- Dia da semana

- Dia do mês

- Mês

- Ano

- Flag fim de semana

- Diferença de tempo entre duas transações

- Distância do cliente ao terminal

- Valor movimentado nas últimas X horas

- Média do valor movimentado nas últimas X horas

- Mediana do valor movimentado nas últimas X horas

- Mínimo valor movimentado nas últimas X horas

- Máximo valor movimentado nas últimas x Horas

- Quantidade total de transações realizadas pelo cliente nas últimas X horas

- Tempo desde a última transação

- Flag para transações consecutivas no mesmo terminal

- Proporção de transações em períodos de alto risco

- Flag de transação acima da média do cliente

- Contagem de quantidade de terminais distintos utilizados por cliente

- Razões entre as features

Após a criação de todas as variáveis as novas bases foram salvas em um arquivo CSV.


------------------------------------------------------------------------------------

# Modelagem - Modelo Baseline

Nesta etapa foram criadas pipelines para tratamento das variáveis numéricas e categóricas, além do tratamento de valores nulos (caso existam futuramente).

- Nas variáveis numéricas os valores nulos foram substituídos pela mediana dos valores da base de treino e após isso foram padronizados utilizando o StandardScaler

- Nas variáveis categóricas os valores nulos foram substituídos pela moda dos valores da base de treino e após isso foram tratados utilizando o TargetEncoder

Então foram criados novos dataframes que seriam utilizados para o treinamento do modelo.

Foram treinados diversos algoritmos para verificar qual apresentaria o melhor resultado.

Os algoritmos foram avaliados utilizando as seguintes métricas:

- Accuracy

- Precision

- Recall

- ROC-AUC

- Gini

- KS

O algoritmo que apresentou o melhor resultado foi o XGBoost, conseguindo um valor de 71% no ROC-AUC na base teste.

Também foi avaliada a performance do modelo vigente, onde o mesmo apresenta um ROC-AUC de 50,09%.

O modelo baseline foi salvo para ser comparado posteriormente com o modelo aperfeiçoado.

------------------------------------------------------------------------------------

# Modelagem - Aperfeiçoando o modelo utilizando o Optuna

Nesta etapa foram verificadas diversas métricas do modelo baseline, antes dele ser melhorado pelo Optuna, como:

- Taxa de evento

- Importância das variáveis

- Curva ROC

- Índice Gini e Estatística KS

- Matriz confusão de treino e teste

- Histograma de treino e teste

Também foi verificada a Curva Precision-Recall e verificado os valores com o threshold padrão e o threshold melhorado.

Então o modelo recebeu uma tunagem dos hiperparâmetros através do Optuna, onde conseguiu subir o valor de ROC-AUC para 77,58%.

Após a tunagem dos hiperparâmetros o modelo foi avaliado novamente utilizando todas as métricas citadas acima.

Por fim, a título de análise exploratória, o modelo também foi treinado com um conjunto reduzido de variáveis, apresentando igualmente um desempenho satisfatório.

Esse modelo também foi avaliado utilizando todas as métricas de avaliação citadas acima, mas além disso também foi verificado o desempenho dele no decorrer das safras.


Os resultados foram salvos em uma planilha de excel, onde foi realizado um estudo sobre os resultados.

-------------------------------------------------------------------------------------------------------

# Conclusão




























