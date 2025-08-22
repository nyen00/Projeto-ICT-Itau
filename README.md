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

## Resultados e Análise
### Análise Exploratória de Dados (EDA)
A EDA foi conduzida para entender a distribuição dos custos e identificar padrões nos dados de instâncias em nuvem. Os principais resultados são:

- **Distribuições de Custo**:  
- **Custo por Hora**: A maioria das instâncias custa entre 0 e 10 USD/hora, com uma cauda longa de instâncias mais caras (até 134 USD/hora). Isso sugere uma assimetria significativa, com poucos casos de alto custo dominando a distribuição.  
- **Custo por vCPU/hora**: Concentrado entre 0.05 e 0.1 USD, com baixa variabilidade, indicando uma padronização na precificação por vCPU.  
- **Custo por GB RAM/hora**: Varia entre 0.01 e 0.02 USD, com dispersão menor que o custo total, sugerindo que a memória é um recurso mais previsível e acessível.  

- **Custo Médio por Região**:  
- Regiões como `asia-east2` e `us-west3` apresentam custos médios mais baixos, enquanto `southamerica-west1` e `australia-southeast1` são as mais caras. Essa variação reflete fatores como custos operacionais locais e demanda, oferecendo oportunidades de economia ao escolher regiões estratégicas.

- **Boxplot de Custos por Série de Instância**:  
- Séries como `e2` e `n1` têm custos baixos e baixa variabilidade, ideais para workloads padrão.  
- Séries `a2` e `m2` exibem custos médios e máximos mais altos, com outliers, indicando instâncias premium para alta performance.  
- Outliers em várias séries sugerem configurações especiais que elevam os custos dentro de uma mesma família.

Esses insights da EDA fornecem uma base para os modelos, destacando a importância de normalizar custos por recursos (vCPU, memória) e considerar fatores regionais e de tipo de instância.

### Métricas de Avaliação dos Modelos
Os modelos foram avaliados com:
- **MAE** (*Mean Absolute Error*): Erro absoluto médio.  
- **RMSE** (*Root Mean Squared Error*): Erra quadrático médio.  
- **R²** (*Coeficiente de Determinação*): Variância explicada.

| Modelo              | MAE     | RMSE    | R²     |
|----------------------|---------|---------|--------|
| Regressão Linear     | 0.01683 | 0.03553 | 0.6098 |
| XGBoost              | 0.00541 | 0.00947 | 0.9723 |

#### Interpretação das Métricas
- **Regressão Linear**: Com R² de 0.6098, explica 61% da variância, com MAE de 0.01683 e RMSE de 0.03553. O desempenho moderado reflete a dificuldade em modelar a cauda longa e a não-linearidade observada na EDA.
- **XGBoost**: Com R² de 0.9723, explica 97% da variância, com MAE de 0.00541 e RMSE de 0.00947. O modelo captura eficientemente as relações complexas, como a variação regional e os padrões de custo por série.

### Visualizações e Insights
#### Regressão Linear
- **Gráfico Real vs Previsto**: A dispersão mostra uma tendência geral próxima à linha de 45°, mas com desvios em valores entre 0.2 e 0.6. Isso corrobora o R² moderado e a limitação do modelo linear frente à assimetria dos custos por hora identificada na EDA.
- **Top 10 Variáveis Mais Relevantes**: `family_Accelerator-optimized` e `family_General-purpose` têm coeficientes positivos altos, enquanto `northamerica_northeast1` tem impacto negativo. Isso alinha-se com a EDA, onde séries premium e regiões afetam os custos.

#### XGBoost
- **Gráfico Real vs Previsto**: A dispersão é muito mais ajustada à linha ideal, especialmente em valores de 0 a 0.6, refletindo o alto R² e a capacidade de modelar a variabilidade regional e por série da EDA.
- **Top 10 Variáveis Mais Relevantes**: `family_Accelerator-optimized` lidera, seguido por `memoryGB` e `family_Memory-optimized`. A relevância de `asia-southeast1` e `vCpus` reforça os padrões regionais e de recursos observados na EDA.

### Conclusões dos Resultados
- A **EDA** revelou uma distribuição assimétrica de custos, com impacto significativo de regiões e séries de instância, guiando a escolha de features para os modelos.
- O **XGBoost** superou a Regressão Linear, validando sua capacidade de capturar a não-linearidade e a variabilidade regional e por tipo de instância da EDA. Com 97% da variância explicada, é uma ferramenta poderosa para previsão de custos.
- Variáveis como `family_Accelerator-optimized` e `memoryGB` são drivers principais de custo, enquanto regiões como `asia-east2` oferecem potencial de economia, alinhando-se aos achados exploratórios.
