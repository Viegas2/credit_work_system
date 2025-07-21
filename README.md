# 🧠 Credit Score Case – Análise e Modelagem Preditiva

Este projeto foi desenvolvido com o objetivo de responder a um case prático sobre análise de dados e modelagem preditiva para risco de crédito. O foco é avaliar a qualidade da base de dados, construir uma variável alvo (`Target`) representando o comportamento de pagamento dos clientes, e analisar a viabilidade de prever esse comportamento com um modelo supervisionado.

---

## ❓ Perguntas do Case

1. **Faça uma análise descritiva da base de dados.**

2. **Construa uma variável target, que classifique o cliente de forma binária como "bom" ou "mau" pagador. Considere as seguintes variáveis para construção do seu target:**
   - `Delay_from_due_date`
   - `Num_of_Delayed_Payment`
   - ➤ Justifique a lógica adotada.

3. **A partir da variável target construída, seria possível construir um modelo para predizer este target considerando as demais variáveis do dataset?**
   - ➤ Explique se seria possível e justifique seu raciocínio.

---

## 📊 1. Análise Descritiva

A base de dados inicial contém:

- **50.000 registros**
- **27 colunas**, sendo:
  - 19 categóricas (`object`)
  - 4 numéricas inteiras
  - 4 numéricas contínuas (float)

### Principais problemas identificados:
- Outliers severos (ex: idades > 8000 anos, saldos mensais bilionários)
- Valores nulos em colunas relevantes (`Monthly_Inhand_Salary`, `Credit_History_Age`, etc.)
- Inconsistências de formatação em colunas numéricas
- Distribuições distorcidas e assimétricas

### Após tratamento:
- Redução para **46.095 registros válidos**
- Limpeza de outliers
- Normalização de variáveis numéricas
- Conversão de colunas para tipos apropriados

---

## 🎯 2. Construção da Variável Target

A variável `Target` foi construída com base em dois critérios de risco de crédito:

- **Atraso elevado:** `Delay_from_due_date > 15 dias`
- **Frequência de atraso:** `Num_of_Delayed_Payment > 5`

### Regras:
- Se o cliente **atendeu a qualquer um desses critérios**, ele foi classificado como **"mau pagador" (1)**.
- Caso contrário, foi classificado como **"bom pagador" (0)**.

### Justificativa:
Esses critérios refletem **comportamento financeiro repetido e relevante**, indo além de atrasos pontuais. São amplamente utilizados em análises de crédito para definir perfis de risco.

### Distribuição:
- **Mau pagador**: 89,46%
- **Bom pagador**: 10,54%

> A alta concentração de maus pagadores se justifica pelos próprios critérios adotados, alinhados com a distribuição real dos dados (mediana e quartis de atraso e inadimplência estão acima dos limites definidos).

---

## 🔍 3. É possível construir um modelo preditivo?

Sim, é possível — **desde que algumas condições sejam respeitadas**:

### ✅ Requisitos atendidos:
- As variáveis utilizadas na modelagem são **anteriores ao evento de inadimplência**.
- Foi evitado **data leakage** (ex: `Delay_from_due_date` não foi usada, já que é usada para construir o target).
- Variáveis categóricas foram tratadas adequadamente.
- Foi feita seleção de variáveis relevantes e exclusão de colunas com viés direto.

### 🔧 Modelo Utilizado:
- **Random Forest Classifier**
- Métricas de avaliação: Acurácia, Curva ROC e **Índice KS (Kolmogorov-Smirnov)**

### Resultados:
- O modelo apresentou **boa capacidade discriminatória**, com índice KS considerado alto.
- A visualização de árvores de decisão foi usada para interpretar os critérios de classificação.
- A desbalanceamento da base foi levado em consideração na avaliação.

---
