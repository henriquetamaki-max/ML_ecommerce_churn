###Grave uma apresentação técnica de até 7 minutos compartilhando a tela do seu código, respondendo objetivamente:

1. Qual base de dados foi escolhida e qual o objetivo de negócio do modelo?

OPÇÃO B: E-commerce Churn (Setor de Varejo)



O Problema: Um aplicativo de vendas precisa prever quais clientes estão prestes a abandonar a plataforma (alvo: Churn = 1) para oferecer cupons preventivos de retenção.

Desafio de Negócio: O que custa mais caro para o aplicativo: dar um cupom de desconto para quem já ia continuar comprando normalmente (Falso Positivo) ou perder um cliente em definitivo sem tentar retê-lo (Falso Negativo)?


2. Quais insights visuais e estatísticos mudaram sua visão na Análise Exploratória (EDA)?

Fase 1

media (mean) de NumberOfDeviceRegistered e NumberOfAddress	

Dispositivo de login favorito - precisa ser ajustado (phone e mobile phone)

Nota de satisfacao: mesmo com notas altas acontece churn

Quem reclama dá churn = 50%

Tempo de relacionamento (tenure) quanto menor maior a chance de churn

No heatmap os maiores fatores foram tempo de relacionamento e reclamacao

3. Como você tratou os nulos e os outliers, considerando os impactos específicos no KNN e na Árvore?

Nulos: mostrar colunas. usando o skew analisamos a distribuicao dos valores e como ha outliers optamos por inputar a mediana em todas as colunas

Outliers: utilizado a tecnica do clipping para nao eliminar os poucos dados para o modelo. Ele limita os extremos pelo IQR para o Q1 e Q3

Impacto - Final da fase 2:
KNN:sem o tratamento dos outliers haveria muito erro no modelo, pois ele calcula as distancias entre os varios dados e um outliers iria enganar o modelo. Já com os nulos teriamos erro pela biblioteca exigir valores para os calculos.

A arvore: teriamos menos impacto sem o tratamento dos nulos e outliers. Nao sofreria com os outliers pois é um processo condicional impacto pelos outliers. Ja os nulos poderiamos ter impacto no resultado geral do modelo ja que talvez uma coluna pudesse ser ignorada ou rebaixada pelos nulos.


4. Como você identificou e evitou a ocorrência de overfitting ao mudar os parâmetros do KNN (K) e da Árvore (max_depth)?

Fase 5

KNN: preferi nao usar a acuracia para o criterio, os dados do treino foram balanceados pelo SMOTE, mas o teste permaneceu intacto, desta forma os resultados podem ser distorcidos, portanto usamos o recall (identificar o falso negativo = cliente com churn). No grafico de acuracia quando a linha de treino e teste comecam a se distanciar (k = 5) sinal de overfitting. Tambem fizemos a validacao cruzada com 5 grupos de dados diferentes e usamos o menor desvio de recall(%)

Arvore: no recall de treino o none = 100% pois ela se divide ate ir ao nivel de cada dado detalhando ao extremo, ja os dados de testes nao acompanham a partir do max_depth=14. Fizemos a avaliacao cruzada para ver qual o menor desvio nos 5 grupos de dados e apesar do max_depth=13 ter tido o melhor recall o max_depth=12 teve o menor desvio padrao.

Mostrar conclusao da fase 5


5. Olhando para a Matriz de Confusão, qual modelo você recomenda para a diretoria da empresa e por quê?

Fase 6

Analisando o relatorio de classificacao com o olhar o churn vemos o recall do knn melhor que da arvore 94 contra 83%

Na matriz de confusao fica claro qual modelo escolher. KNN erro 11 e a arvore errou 32. em contrapartida o falso positivo a arvore apontou apenas 39 contra 115 do knn.

Falar do histograma de pedidos para detalhar que cliente pode retornar a comprar varias vezes e ele dando churn no pedido 2 prejudica o negocio.

Alem do modelo é necessario ter acoes paralelas de marketing, relacionamento com cliente para buscar a fidelizacao do cliente como percebemos no heatmap que devemos resolver os problemas e reclamacoes dos clientes.

