# 🌊 Global Liquidity vs. Bitcoin: Correlation Monitor

![Status](https://img.shields.io/badge/Status-Concluído-success)
![Stack](https://img.shields.io/badge/Stack-Databricks%20|%20PySpark%20|%20PowerBI-blue)

> **"O Bitcoin é apenas uma esponja de liquidez dos Bancos Centrais?"**

Este projeto de **Business Intelligence & Data Engineering** investiga matematicamente a correlação entre a impressão de dinheiro global (M2 Money Supply) e a valorização do Bitcoin.

Mais do que um dashboard, este projeto demonstra como resolver problemas complexos de **modelagem de séries temporais** (frequências diferentes de dados) utilizando um pipeline robusto no Databricks.

---

## 🖼️ Resultado Final (Dashboard)

O painel permite identificar divergências macroeconômicas (quando o preço descola da liquidez) para apoiar teses de investimento.

<img width="1919" height="1079" alt="Dashboard Liquidez vs BTC" src="https://github.com/user-attachments/assets/21a56880-f09b-4aca-a110-759d960438e4" />

---

## 🧠 O Problema de Negócio

Analistas de mercado debatem se o Bitcoin sobe por mérito próprio ou apenas pela desvalorização das moedas fiduciárias. Para responder isso, precisamos cruzar:
1.  **Preço do Bitcoin:** Dados diários/segundo.
2.  **Oferta Monetária (M2):** Dados mensais divulgados pelo FED.

**A dor:** Tentar cruzar esses dados no Excel ou Power BI direto gera lacunas (nulls) ou agregações erradas que distorcem a correlação.

---

## 🛠️ A Solução Técnica (Pipeline & Time Series)

Construí um pipeline **End-to-End** focado na integridade da série temporal.

### 1. Ingestão Automatizada (Bronze)
* Conexão via Python com APIs do **FRED (Federal Reserve Economic Data)** e **Yahoo Finance**.
* [Ver código Bronze](bronze.ipynb)

### 2. O Pulo do Gato: Tratamento de Granularidade (Silver)
Aqui está o diferencial técnico do projeto. Para cruzar dados diários com mensais, utilizei **PySpark Window Functions** para realizar uma interpolação técnica (*Forward Fill*).
* **Técnica:** O valor do M2 de janeiro é repetido para todos os dias de janeiro até que saia o dado de fevereiro.
* **Resultado:** Uma série contínua e correlacionável, sem "buracos" no gráfico.
* [Ver código Silver](silver.ipynb)

### 3. Normalização e Performance (Gold)
* **Base 100:** Criação de índices normalizados (Index = 100) para comparar a *taxa de crescimento* dos dois ativos na mesma escala.
* **Otimização:** Uso de `ZORDER BY (data)` para garantir que o Power BI filtre os dados históricos instantaneamente.
* [Ver código Gold](gold.ipynb)

---

## 💡 Insights Extraídos

* **Correlação de Longo Prazo:** O estudo apontou uma correlação positiva forte (> 0.6), confirmando que o Bitcoin tende a seguir a expansão monetária global.
* **Momentos de Ruído:** O dashboard evidenciou que eventos exógenos (como o banimento de mineração na China em 2021) quebram essa correlação temporariamente, criando oportunidades de arbitragem.

---

## 💻 Tech Stack

* **Processamento:** Azure Databricks (PySpark)
* **Análise de Séries Temporais:** Window Functions, Interpolation
* **Fontes de Dados:** FRED API, Yahoo Finance API
* **Visualização:** Power BI (DAX)
