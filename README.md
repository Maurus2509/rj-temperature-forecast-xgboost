# Previsão de Temperatura Média para o Rio de Janeiro com XGBoost

## 📋 Sobre o Projeto
Este repositório contém um pipeline de Machine Learning desenvolvido em Python para a previsão de séries temporais de temperatura média no Rio de Janeiro. Utilizando dados históricos abrangendo mais de três décadas, o projeto aplica engenharia de atributos temporais e estatísticas móveis para treinar e avaliar um modelo preditivo baseado em **XGBoost Regressor**.

## 🛠️ Tecnologias e Bibliotecas Utilizadas
* **Python**
* **Pandas** e **NumPy** (Manipulação e estruturação de dados)
* **Matplotlib** e **Seaborn** (Visualização de dados e análise exploratória)
* **Scikit-Learn** (Métricas de avaliação como R² e MAPE)
* **XGBoost** (Modelo preditivo de gradient boosting)

## 📊 Estrutura dos Dados e Features
O conjunto de dados processado (`dados_preprocessados_temp_rj.csv`) contém registros mensais desde dezembro de 1991 até setembro de 2025, totalizando 406 observações. As principais variáveis utilizadas são:
* **`TAMB`**: Temperatura ambiente de referência.
* **`seno_mes` / `cos_mes`**: Codificação cíclica para capturar a sazonalidade anual dos meses.
* **`media_movel_3m` / `media_movel_12m`**: Médias móveis calculadas em janelas de 3 e 12 meses.
* **`std_movel_3m` / `std_movel_12m`**: Desvios padrão móveis para capturar a volatilidade temporal.
* **`TARGET`**: Variável alvo representando a temperatura a ser prevista.

## ⚙️ Metodologia e Treinamento
1. **Carregamento e Limpeza**: Importação dos dados com indexação temporal (`time`).
2. **Análise Exploratória**: Inspeção estatística e visualização da distribuição e comportamento histórico da variável alvo (`TARGET`).
3. **Divisão Treino/Teste (Train-Test Split)**: 
   * **Treino**: Primeiros 25 anos (1991 – 2015) equivalendo a ~71% dos dados.
   * **Teste**: Últimos 10 anos (2016 – 2025) equivalendo a ~29% dos dados, simulando um cenário real de previsão para o futuro.
4. **Modelagem**: Treinamento do `XGBRegressor` configurado com suporte a features categóricas/estruturadas, taxa de aprendizado de `0.1`, profundidade máxima de árvore (`max_depth = 3`) e amostragem de colunas (`colsample_bytree = 0.8`).[cite: 1]
