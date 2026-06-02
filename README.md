# 📈 Machine Learning com Ações da Bolsa

Projeto de previsão do preço de fechamento das ações do **Banco do Brasil (BBAS3.SA)** utilizando redes neurais artificiais com dados históricos do Yahoo Finance.

---

## 🎯 Objetivo

Treinar um modelo de Machine Learning capaz de prever o preço de fechamento diário da ação BBAS3 com base em médias móveis de curto, médio e longo prazo.

---

## 🗂️ Estrutura do Projeto

```
📁 ml-acoes-bbas3/
└── MachineLearningComAcoes_comentado.ipynb   # Notebook principal com comentários
```

---

## 🔧 Tecnologias Utilizadas

| Biblioteca | Finalidade |
|---|---|
| `yfinance` | Download de dados históricos do Yahoo Finance |
| `pandas` | Manipulação e análise de dados |
| `numpy` | Operações numéricas |
| `matplotlib` | Geração de gráficos |
| `scikit-learn` | Pré-processamento e modelo de ML |

---

## 📊 Metodologia

### 1. Coleta de Dados
Dados históricos dos últimos **10 anos** da ação **BBAS3.SA** obtidos via `yfinance`.

### 2. Engenharia de Features
Criação de três médias móveis do preço de fechamento como variáveis de entrada do modelo:

| Feature | Descrição |
|---|---|
| `mm5d` | Média móvel dos últimos 5 dias |
| `mm14d` | Média móvel dos últimos 14 dias |
| `mm21d` | Média móvel dos últimos 21 dias |

### 3. Divisão dos Dados

| Conjunto | Proporção | Finalidade |
|---|---|---|
| Treino | ~70% | Ajustar os pesos da rede neural |
| Validação | ~15% | Monitorar overfitting |
| Teste | 15% | Avaliação final do modelo |

> ⚠️ `shuffle=False` é utilizado para preservar a ordem cronológica — essencial em séries temporais.

### 4. Modelo
`MLPRegressor` (rede neural multicamada para regressão) do `scikit-learn`, com até **2000 épocas** de treinamento.

### 5. Duas Abordagens de Normalização

| Abordagem | Normalização X | Normalização y | R² obtido |
|---|---|---|---|
| Abordagem 1 | `MinMaxScaler` | ❌ Não normalizado | **95,52%** |
| Abordagem 2 | `StandardScaler` | ✅ `StandardScaler` | **90,18%** |

---

## 📉 Resultados

A **Abordagem 1** obteve melhor desempenho (**R² = 95,52%**) por um motivo direto: as features (médias móveis) e o alvo (`Close`) já estão naturalmente na mesma escala — todos são preços em R$. Normalizar o alvo `y` neste contexto introduziu uma transformação extra desnecessária, reduzindo a performance do modelo.

---

## ⚠️ Limitações

- O modelo utiliza **apenas médias móveis** como features, sendo cego a eventos externos (notícias, indicadores macroeconômicos, etc.)
- Um R² alto em séries temporais pode ser enganoso — o modelo aprende que *"o preço de amanhã será próximo ao de hoje"*, o que falha em movimentos bruscos
- **Não recomendado para decisões reais de investimento** sem análises complementares


---

## 📄 Licença

Este projeto está sob a licença MIT. Sinta-se livre para usar, modificar e distribuir.
