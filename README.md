# 🏠 Previsão de Preços de Arrendamento nos EUA com Apache Spark

## Objetivo
Construir e comparar modelos de regressão para prever o preço mensal de
arrendamento de imóveis nos EUA, com base em características físicas,
geográficas e de serviços. Pipeline completa de Big Data desde o
pré-processamento até à otimização de modelos com Cross-Validation.

## Ferramentas e tecnologias
- Apache Spark / PySpark (processamento distribuído)
- Spark MLlib (modelação)
- Python (pandas, matplotlib, seaborn)
- Dataset: USA Housing Listings — Craigslist (Kaggle)
- ~380.000 registos | 22 variáveis

## Pipeline do projeto

### 1. Pré-processamento
- Carregamento com TRY_CAST para conversão robusta de tipos
- Tratamento de valores omissos (mediana para sqfeet, moda para beds/baths)
- Remoção de outliers com intervalos plausíveis para o mercado residencial
- Remoção de colunas irrelevantes (URLs, identificadores, texto livre)

### 2. Feature Engineering
- Codificação de variáveis categóricas com StringIndexer + OneHotEncoder
- Normalização de variáveis numéricas com StandardScaler
- Combinação de features num único vetor para Spark MLlib
- Exportação do dataset final em formato Parquet

### 3. Modelação e avaliação
- Divisão treino/teste: 80% / 20% (seed=42)
- Métricas: RMSE, MAE, R², MAPE

## Modelos comparados

| Modelo             | RMSE (USD) | MAE (USD) | R²     | MAPE   |
|--------------------|------------|-----------|--------|--------|
| Regressão Linear   | 416,75     | 256,23    | 0,4959 | 23,40% |
| Random Forest      | 433,09     | 282,16    | 0,4556 | 27,01% |
| GBT                | 398,01     | 253,31    | 0,5402 | 23,46% |
| **GBT + CV**       | **384,80** | **243,27**| **0,5702** | **22,43%** |

## Resultados
- **Melhor modelo:** GBT com Cross-Validation (3 folds, Grid Search)
- RMSE de 384,80 USD e R² de 0,57 no conjunto de teste
- Hiperparâmetros ótimos: maxDepth=5, maxIter=20

## Principais insights
- Localização geográfica (longitude) é o segundo fator mais determinante
- Opções de lavandaria são o preditor com maior importância relativa
- Tipo de imóvel (house, condo) tem impacto relevante no preço
- Variáveis beds e state apresentaram baixo poder preditivo neste dataset

## Autores
Projeto desenvolvido em grupo no âmbito do Mestrado em Análise de Dados.
- Joana Tomé
- Gonçalo Conceição
