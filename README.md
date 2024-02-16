## Entrega do exercício
- A apresentação contendo uma explicação profunda sobre a AED, escolha e desempenho do modelo e consequências de negócio para a empresa X-Health está contida [aqui](https://docs.google.com/presentation/d/1542K4pz8Kbr7qG_Jjy-2qzCRYUCLSbyuThJcrfvHm6g/edit#slide=id.p).

<br></br>
## Análise exploratória de dados (AED)

- A análise exploratória de dados tem como objetivo analisar a estrutura dos dados para entender sua organização e identificar padrões e tendências nos dados, como distribuições de valores, relações entre variáveis e comportamentos ao longo do tempo.
- Ademais, é possível identificar e lidar com anomalias nos dados, como outliers ou valores faltantes. Essas anomalias podem distorcer nossas análises e modelos, levando a conclusões errôneas.
- Por fim, são selecionadas as features mais relevantes para a criação de um modelo preditivo.
- As variáveis foram separadas em numéricas e categóricas para passarem por análises diferentes:
    - Numéricas: analisei as distribuições de cada variável a partir de histogramas, identifiquei possíveis outliers em algumas colunas a partir de scatterplots, eliminei as colunas cujas distribuições eram de ordens de grandezas muito altas (geralmente, colunas associadas a valores em reais). Ressalto que não havia valores faltantes.
    - Categóricas: analisei as distribuições de cada variável a partir de value counts (quantas vezes o valor em cada coluna aparece), eliminei as variáveis que tinham um número excessivo de opções e realizei um one hot encoding para utilizar as colunas categóricas restantes nos modelos.

<br></br>
## Treinamento dos modelos
- Escolhi os modelos de Regressão Logística, K-Nearest-Neighbours, Random Forest, XGBoost e Multi-Layer Perceptron pois são modelos de machine learning relativamente conhecidos e costumam se dar bem com predições binárias.
- Após excluir as colunas que julguei menos relevantes, separei o dataset completo em datasets de treino e validação.
- Realizei o fitting de cada modelo para o dataset de treino e realizei testes de validação cruzada (5-fold) para obter as métricas de acurácia e recall.
- Criei matrizes de confusão para obter uma melhor visualização dos palpites de cada modelo e verificar qual deles acertava a maior quantidade de defaults/caloteiros.
- Por fim, criei gráficos de comparação para as métricas de acurácia e recall.
- Como o intuito é acertar o maior número de caloteiros, o Random Forest foi o melhor modelo escolhido, pelo fato de obter o maior valor de recall (algo em torno de 0.35 e 0.38, varia conforme a vez que vc roda os kernels) entre os modelos. Caso o objetivo fosse acertar caloteiros e não caloteiros, o modelo escolhido seria o XGBoost, pois possui a maior acurácia e o segundo maior recall.

<br></br>
## Contexto de negócio do exercício

- Contexto geral - A empresa X-Health atua no comércio B2B vendendo dispositivos eletrônicos voltados para saúde com amplo espectro de preços, e de variada sofisticação/complexidade. 
  
- Sobre as vendas - As vendas são feitas à crédito: o cliente B2B faz seu pedido e paga (à vista ou em várias parcelas, conforme o combinado pelo time de vendas) num tempo futuro pré-determinado.
  
- O problema - O time financeiro da X-Health tem observado um número indesejável de não-pagamentos ("default" ou calote, em bom português).

- O objetivo - Querem de alguma forma minimizar esse fenômeno. Desejam uma solução capaz de identificar os clientes podem vir o dar o default (ou "calote").

Antes de iniciar a solução, é fundamental estabelecer premissas que ajudarão a moldar sua abordagem. Isso inclui:

- Compreensão do Negócio: Entender profundamente o contexto no qual a X-Health opera, incluindo o perfil de seus clientes B2B, e como os processos de crédito e pagamento impactam a operação.

- Limitações e Desafios de Dados: Identificar quaisquer limitações nos dados fornecidos, como a representatividade, viés, ou qualidade dos dados. Considerar como esses fatores podem afetar a modelagem e a interpretação dos resultados.

- Aspectos Éticos e Regulatórios: Considerar quaisquer implicações éticas e regulatórias associadas ao uso de dados de crédito e pessoais, especialmente em relação à privacidade e discriminação.

- Impacto do Modelo: Refletir sobre como a implementação do modelo pode impactar a empresa e seus clientes. Isso inclui considerar tanto os benefícios potenciais quanto os riscos associados.


<br></br>
## Sobre o dataset

- Caminho: o dataset disponibilizado pela X-Health encontra-se em 
```
./_data/dataset_2021-5-26-10-14.csv
```
- Estrutura do .csv: para ler o arquivo, use  sep = '\t' e encoding = 'utf-8'.
- O dataset possui tanto variáveis internas (decorrentes do comportamento histórico do cliente B2B junto à X-Health), quanto variáveis externas consultadas em bureaus de crédito, como o Serasa.
- Cada linha do dataset representa um evento de compra de um conjunto de produtos, e tanto as variáveis internas quanto externas representam uma fotografia do cliente naquele instante.
- Valores faltantes estão indicados no dataset como "missing".
- Dicionário de dados:

| nome_coluna                    | desc                                                                                               |
| --------------------------     |----------------------------------------------------------------------------------------- |
| default\_3months               |Quantidade de default nos últimos 3 meses                                                          |
| ioi\_Xmonths                   |Intervalo médio entre pedidos (em dias) nos últimos X meses                                       |
| valor\_por\_vencer             |Total em pagamentos a vencer do cliente B2B, em Reais     |
| valor\_vencido                 |Total em pagamentos vencidos do cliente B2B, em Reais                                              |
| valor\_quitado                 |Total (em Reais) pago no histórico de compras do cliente B2B                |
| quant\_protestos               |Quantidade de protestos de títulos de pagamento apresentados no Serasa|
| valor\_protestos               |Valor total (em Reais) dos protestos de títulos de pagamento apresentados no Serasa|
| quant\_acao_judicial           |Quantidade de ações judiciais apresentadas pelo Serasa|
| acao\_judicial\_valor          |Valor total das ações judiciais (Serasa) |
| participacao\_falencia\_valor  |Valor total (em Reais) de falências apresentadas pelo Serasa |
| dividas\_vencidas\_valor       |Valor total de dívidas vencidas (Serasa)|
| dividas\_vencidas\_qtd         |Quantidade total de dívidas vencidas (Serasa)|
| falencia\_concordata\_qtd      |Quantidade de concordatas (Serasa)|
| tipo\_sociedade                |Tipo de sociedade do cliente B2B |
| opcao\_tributaria              |Opção tributária do cliente B2B |
| atividade\_principal           |Atividade principal do cliente B2B|
| forma\_pagamento               |Forma de pagamento combinada para o pedido |
| valor\_total\_pedido           |Valor total (em Reais) do pedido em questão|
| month                          |Mês do pedido|
| year                           |Ano do pedido|
| default                        |Status do pedido: default = 0 (pago em dia), default = 1 (pagamento não-realizado, calote concretizado)|



<br></br>
## Expectativas do exercício:
1 - Um Jupyter Notebook com uma **análise exploratória** e a **solução de dados** utilizada nos dados do dataset disponibilizado. Use sua criatividade e nos mostre os insights que encontrar, assim como uma solução viável para o problema.

2 - Preparar uma apresentação dos resultados e insights obtidos, destinada a um público de negócios. A apresentação deve comunicar eficazmente as descobertas técnicas de forma compreensível para não especialistas em ML/AI. Aqui estÃo alguns pontos a serem abordados na apresentação:

   - Uma visão geral do problema e da abordagem adotada.
   - Principais insights da análise exploratória de dados.
   - Detalhes sobre o modelo desenvolvido ou solução de dados, incluindo a escolha, justificativa e desempenho.
   - Discussão sobre as implicações de negócios dos resultados, incluindo como eles podem impactar a tomada de decisão na X-Health.
   - Formato: A apresentação pode ser em formato PowerPoint ou similar, com uma duração sugerida de 20-30 minutos.

<br></br>
## Sobre a entrega do exercício:
-  A solução de seu exercício deve ser entregue em um repositório público do tipo git de sua preferência (github, gitlab, bitbucket ou qualquer outro que preferir). 
-  Espera-se tanto um repositório quanto códigos **bem documentados**: faça seu melhor nesse sentido, adotando as melhores práticas que conhece. 
-  Os resultados precisam ser **reprodutíveis**: 
   -  é fundamental estar contido no repositório de entrega um arquivo **requirements.txt** ou **conda yaml file** com as dependências necessárias para rodar todos os Notebooks.
