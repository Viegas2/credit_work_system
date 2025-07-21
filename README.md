#Credit Score Case — Análise e Modelagem de Risco de Crédito
Este projeto foi desenvolvido como resposta a um estudo de caso envolvendo análise de dados e modelagem preditiva de risco de crédito. O objetivo principal é avaliar a base de dados, construir uma variável alvo representando o comportamento de pagamento dos clientes e testar a viabilidade de prever esse comportamento por meio de um modelo supervisionado.

1. Análise Descritiva da Base
A base original conta com 50 mil registros e 27 colunas. As variáveis se distribuem da seguinte forma:

19 variáveis categóricas (tipo object)

4 variáveis numéricas inteiras

4 variáveis numéricas contínuas (float)

Principais problemas encontrados:
Valores extremos fora da realidade (por exemplo, idades superiores a 8000 anos e saldos mensais bilionários)

Presença de valores nulos em colunas importantes, como Monthly_Inhand_Salary e Credit_History_Age

Inconsistências de formatação e escalas

Distribuições assimétricas nas variáveis numéricas

Após o tratamento:
Redução da base para 46.095 registros válidos

Remoção de outliers extremos

Normalização e padronização de variáveis numéricas

Ajustes de tipo e limpeza de dados categóricos

2. Construção da Variável Alvo (Target)
A variável Target foi construída para classificar os clientes em dois grupos: bons e maus pagadores. Para isso, foram considerados dois critérios principais:

Atrasos significativos no pagamento: Delay_from_due_date > 15 dias

Frequência de atrasos: Num_of_Delayed_Payment > 5

Regras adotadas:
Clientes que atendem a pelo menos um desses critérios foram classificados como maus pagadores (1)

Clientes que não atendem a nenhum dos dois critérios foram classificados como bons pagadores (0)

Justificativa:
Os critérios escolhidos refletem comportamentos consistentes de inadimplência e são comumente utilizados em análises de risco de crédito. Buscou-se ir além de atrasos pontuais, focando em padrões relevantes de comportamento financeiro.

Distribuição da variável:
Maus pagadores: 89,46%

Bons pagadores: 10,54%

A concentração maior de maus pagadores está de acordo com a própria distribuição dos dados, que já indicava tendência elevada de inadimplência com base na mediana e nos quartis das variáveis relacionadas.

3. Viabilidade de um Modelo Preditivo
Sim, é possível construir um modelo de machine learning para prever a variável Target, desde que algumas precauções sejam seguidas:

Aspectos considerados:
Todas as variáveis utilizadas como preditoras estão disponíveis antes do evento de inadimplência, evitando vazamento de dados.

A variável Delay_from_due_date, por ser usada na construção do target, não foi usada como preditora no modelo.

Variáveis categóricas foram tratadas com codificação adequada (ex: one-hot encoding ou label encoding).

Foi feita uma seleção criteriosa de variáveis, excluindo colunas com risco de viés direto.

Modelo utilizado:
Random Forest Classifier

Métricas de avaliação:
Acurácia

Matriz de confusão

Curva ROC

Índice KS (Kolmogorov-Smirnov), que indicou boa capacidade discriminatória do modelo

Observações finais:
O desbalanceamento da base foi considerado durante a modelagem e avaliação.

O modelo conseguiu identificar padrões relevantes com bom desempenho, mesmo diante do desequilíbrio da variável alvo.

A visualização das árvores de decisão contribuiu para a interpretação dos principais critérios utilizados pelo modelo.
