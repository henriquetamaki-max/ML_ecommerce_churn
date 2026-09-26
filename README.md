# Curso: Machine Learning e Visão Computacional T3

# Autor: Henrique Tamaki

# Churn Prediction - E-commerce

Modelo de Machine Learning para identificar clientes com risco de cancelamento (*churn*) em um aplicativo de e-commerce.

O projeto compara **KNN** e **Árvore de Decisão** e recomenda o modelo mais adequado para uma ação de retenção.

## Objetivo

Prever quais clientes podem cancelar ou deixar de comprar para que a empresa possa agir antes do cancelamento, por exemplo, com um cupom de retenção.

Neste projeto, o **Falso Negativo** é considerado o erro mais prejudicial, pois representa um cliente em risco que não foi identificado.

## Desafio de Negócio

O que custa mais caro para o aplicativo: dar um cupom de desconto para quem já ia continuar comprando normalmente (Falso Positivo) ou perder um cliente em definitivo sem tentar retê-lo (Falso Negativo)?

## Referencias
- Github repositorio: https://github.com/henriquetamaki-max/ML_ecommerce_churn.git
- Video com apresentação do projeto: https://youtu.be/SHoZKEbG4Us
- Dataset original: https://drive.google.com/file/d/1Nbmt6Y_P1TjdFxsfTxfKQxKLkaNDJrT9/view?usp=sharing


Baixado e salvo em: dados/E Commerce Dataset - E Comm.csv

## Dados

- 5.630 clientes;
- 20 colunas;
- 16,8% de clientes com churn;
- sem linhas duplicadas;
- valores nulos tratados com a mediana.

As variáveis incluem comportamento de compra, uso do aplicativo, satisfação e informações cadastrais.

## Metodologia

- análise exploratória dos dados;
- tratamento de valores nulos e outliers pelo método IQR;
- criação da variável `cashback_por_pedido`;
- codificação de variáveis categóricas com One-Hot Encoding;
- divisão estratificada em treino e teste, na proporção 80/20;
- aplicação do SMOTE somente nos dados de treino;
- padronização das variáveis numéricas usadas pelo KNN;
- ajuste dos hiperparâmetros com validação cruzada;
- comparação dos modelos com métricas de classificação.

## Principais insights

- `Tenure` apresentou a maior correlação com o churn, aproximadamente -0,35. Clientes mais novos tendem a cancelar mais.
- Clientes que registraram reclamações também apresentaram maior risco de churn.
- Nenhuma variável isolada explicou o cancelamento de forma forte.
- Alguns clientes chegaram a realizar até 16 pedidos, mostrando que a perda de um cliente pode representar várias compras futuras.

## Modelos avaliados

Foram comparados:

- KNN com `K=3`;
- Árvore de Decisão com `max_depth=12`.

Na Árvore de Decisão, profundidades maiores apresentaram acurácia alta no treino, mas também sinais de *overfitting*. A profundidade 12 apresentou um resultado mais estável na validação cruzada.

## Resultado final - Resumo executivo para a diretoria

No conjunto de teste, entre os 190 clientes que realmente apresentaram churn:

- o KNN deixou de identificar 11 clientes;
- a Árvore de Decisão deixou de identificar 32 clientes.

O KNN apresentou mais Falsos Positivos, mas identificou melhor os clientes que realmente cancelaram. Como o objetivo principal é evitar a perda de clientes, o modelo recomendado para produção é o **KNN com `K=3`**.

Essa recomendação representa uma análise inicial. O retorno financeiro dos cupons não foi calculado porque o projeto não possui dados sobre CAC ou sobre o efeito das ações de retenção. Esse impacto poderia ser medido posteriormente com um teste A/B.

## Dicionário atualizado de Dados

 #   Column                       Non-Null Count  Dtype  
---  ------                       --------------  -----  
 0   CustomerID                   5630 non-null   int64  
 1   Churn                        5630 non-null   int64  
 2   Tenure                       5366 non-null   float64
 3   PreferredLoginDevice         5630 non-null   str    
 4   CityTier                     5630 non-null   int64  
 5   WarehouseToHome              5379 non-null   float64
 6   PreferredPaymentMode         5630 non-null   str    
 7   Gender                       5630 non-null   str    
 8   HourSpendOnApp               5375 non-null   float64
 9   NumberOfDeviceRegistered     5630 non-null   int64  
 10  PreferedOrderCat             5630 non-null   str    
 11  SatisfactionScore            5630 non-null   int64  
 12  MaritalStatus                5630 non-null   str    
 13  NumberOfAddress              5630 non-null   int64  
 14  Complain                     5630 non-null   int64  
 15  OrderAmountHikeFromlastYear  5365 non-null   float64
 16  CouponUsed                   5374 non-null   float64
 17  OrderCount                   5372 non-null   float64
 18  DaySinceLastOrder            5323 non-null   float64
 19  CashbackAmount               5630 non-null   int64  
 20  Cashback_por_pedido		  5630 non-null   float64



## Como executar

### Pré-requisitos

- Python 3;
- Jupyter Notebook ou VS Code.

### Instalação

Instale as dependências com:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn jupyter
```

### Execução

1. Clone este repositório.
2. Abra `Henrique_tamaki_churn_ecommerce.ipynb` no Jupyter Notebook ou no VS Code.
3. Confirme se o arquivo de dados está em:

```text
dados/E Commerce Dataset - E Comm.csv
```

4. Execute as células em ordem usando **Restart + Run All**.

## Tecnologias

- Python;
- Pandas;
- NumPy;
- Matplotlib;
- Seaborn;
- Scikit-learn;
- Imbalanced-learn;
- Jupyter Notebook.

## Observação

Este é um projeto educacional. Os resultados podem mudar conforme a divisão dos dados e não devem ser usados diretamente em produção sem novos testes, monitoramento e avaliação financeira.