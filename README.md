# Projeto: Previsão de Customer Churn (Telco Dataset)

## Contexto
A retenção de clientes é um dos maiores desafios em empresas de telecomunicações.  
Identificar **quais clientes estão propensos a cancelar o serviço (churn)** permite que a empresa atue de forma proativa, oferecendo incentivos e estratégias de fidelização.  

Este projeto aplica **técnicas de ciência de dados e machine learning** para prever o churn de clientes da Telco.  

---

## Objetivos
- Explorar e entender o dataset **Telco Customer Churn**.  
- Tratar dados faltantes e variáveis categóricas corretamente.  
- Corrigir o **desbalanceamento de classes** (muito mais clientes que ficam do que os que saem).  
- Criar e avaliar modelos preditivos, priorizando **recall na classe churn** (identificar quem vai sair).  
- Apresentar métricas de classificação e matriz de confusão para interpretação prática.  

---

## Tecnologias Utilizadas
- **Python 3.10+**  
- Bibliotecas principais:  
  - `pandas`, `numpy` → manipulação de dados  
  - `matplotlib`, `seaborn` → visualização  
  - `scikit-learn` → pré-processamento, modelos, métricas  
  - `imbalanced-learn` → técnica de balanceamento **SMOTE**  
- Ambiente: **Jupyter Notebook / VS Code**  

---

## Análise Exploratória (EDA)
1. **Distribuição do Churn**  
   - Aproximadamente **26% dos clientes cancelaram** (classe minoritária).  
   - Forte **desbalanceamento**, exigindo técnicas de oversampling.  

2. **Valores Faltantes**  
   - Coluna `TotalCharges` apresentou valores como string com espaços.  
   - Corrigida para tipo numérico, com imputação de valores nulos.  

3. **Relações simples**  
   - Clientes com contrato **Month-to-month** apresentaram maior taxa de churn.  
   - Métodos de pagamento automáticos correlacionaram-se com menor churn.  

---

## Pré-Processamento
- **Numéricas**: imputação (mediana) + padronização (`StandardScaler`).  
- **Categóricas**: imputação (mais frequente) + codificação (`OneHotEncoder`).  
- **Balanceamento**: aplicado **SMOTE** somente no treino (via `imblearn.Pipeline`).  
- **Split**: 80% treino / 20% teste, estratificado.  

---

## Modelagem
Foram comparados dois modelos:

1. **Logistic Regression (baseline)**  
   - Modelo linear e interpretável.  
   - Bom para entender pesos/coeficientes das variáveis.  

2. **Random Forest**  
   - Modelo não-linear baseado em árvores.  
   - Captura interações complexas entre variáveis.  

---

## Resultados (com SMOTE)

### Logistic Regression
- **ROC AUC**: **0.84**  
- **Recall (churn=1)**: 79%  
- **Precisão (churn=1)**: 59%  
- **Matriz de Confusão**:
      Predito
      0     1
  
---
  ## Avaliação
  
O modelo acerta a maioria dos clientes que saem (**alto recall**), mas gera falsos alarmes (FP = 293).  
Isso é aceitável em churn, pois é melhor oferecer benefícios extras para alguns clientes que **não sairiam** do que **perder clientes reais** que iriam sair.  

---

## Interpretação de Negócio
- O modelo consegue identificar **~8 em cada 10 clientes que dariam churn**.  
- Embora alguns clientes fiquem classificados erroneamente como churn (falsos positivos), isso pode ser vantajoso para o negócio: campanhas de retenção são geralmente menos custosas do que a perda de clientes.

---

## Autor
   **Marcus Nogueira**  
Estudante de Ciência da Computação | Desenvolvedor de Software | Aspirante a Engenheiro de Dados  

