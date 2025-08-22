# ICT Itaú - Projeto Trilha A: Dados & IA

## Autor
- **Nome:** Nguyen Thi Hoang Yen

## Trilha e Tarefa
- **Trilha:** A – Dados & IA  
- **Tarefa Principal:** Criar um pipeline simples de ingestão e processamento de dados (em Python), a partir de dados públicos de custo de nuvem (ex: AWS pricing, Azure calculator API, etc.).  
- **Desafio Adicional:** Implementar um modelo de machine learning (regressão, clustering ou outro) para prever custos ou identificar padrões de uso.  

## Entrega Esperada
- Código-fonte comentado (disponível no notebook principal).  
- Notebook com explicação do pipeline (arquivo Jupyter Notebook ou script Python).  
- Print ou gráfico do resultado do modelo (incluídos na seção de Análise Exploratória e Modelo).  
- Arquivo `.csv` com os dados tratados e resultados (gerado como `cloud_pricing_processed.csv` e `cloud_pricing_results.csv`).  

## Descrição do Projeto
Este projeto desenvolve um pipeline de ingestão, processamento e modelagem de dados de custos de instâncias em nuvem, utilizando dados públicos do Google Cloud. O foco inclui análise exploratória (EDA), processamento de dados e a implementação de modelos de machine learning (Regressão Linear e XGBoost) para prever o custo por vCPU/hora com base em características como vCPUs, memória, família de instância, região e localização.

O objetivo é apoiar decisões estratégicas de otimização de custos no contexto do ICT Itaú.

## Objetivos
1. Ingestão e limpeza de dados de custo de nuvem.  
2. Análise exploratória para identificar padrões.  
3. Treinamento de modelos de machine learning para previsão de custos.  
4. Exportação de resultados em CSV e visualizações.

## Requisitos
### Bibliotecas Python
- `pandas`, `numpy` (manipulação de dados)  
- `matplotlib`, `seaborn` (visualizações)  
- `scikit-learn` (pré-processamento e Regressão Linear)  
- `xgboost` (modelo de gradient boosting)  

### Ambiente
- Python 3.8 ou superior.  
- Jupyter Notebook (recomendado).

## Pipeline e Modelagem
### Ingestão e Pré-processamento
- Dados carregados de `cloud_pricing_processed.csv`.  
- Features: `vCpus`, `memoryGB`, `family`, `region`, `location`.  
- Target: `cost_per_vcpu_hour`.  
- Pré-processamento: One-hot encoding para variáveis categóricas.

### Modelos
- **Regressão Linear**: Baseline simples com Pipeline.  
- **XGBoost**: Modelo avançado com hiperparâmetros otimizados (n_estimators=500, max_depth=4, etc.).

### Métricas de Avaliação
| Modelo              | MAE     | RMSE    | R²     |
|----------------------|---------|---------|--------|
| Regressão Linear     | 0.01683 | 0.03553 | 0.6098 |
| XGBoost Regressor    | 0.00541 | 0.00947 | 0.9723 |

- XGBoost supera a Regressão Linear, explicando 97% da variância.

### Visualizações
- **Real vs Previsto**: Dispersão mostrando a acurácia das previsões.  
- **Importância das Variáveis**: Gráficos de barras para Regressão Linear (coeficientes) e XGBoost (importância).  
- Top variáveis: `family_Accelerator-optimized`, `memoryGB`, `vCpus`, etc.

