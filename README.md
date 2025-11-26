# 📊 Monitor de Liquidez Global & Bitcoin

> **Análise de Engenharia de Dados sobre a correlação entre a Base Monetária Global (M2) e o preço do Bitcoin.**

![Status](https://img.shields.io/badge/Status-Concluído-success)
![Stack](https://img.shields.io/badge/Stack-Databricks%20|%20PySpark%20|%20PowerBI-blue)

## 🖼️ Visão Geral do Dashboard

<img width="1919" height="1079" alt="Image" src="https://github.com/user-attachments/assets/21a56880-f09b-4aca-a110-759d960438e4" />
---

## 💼 O Problema de Negócio

É consenso no mercado financeiro que o Bitcoin funciona como uma **"esponja de liquidez global"**. No entanto, utilizar apenas agregados monetários (M2) como indicador único de compra/venda pode ser fatal para o investidor.

O desafio deste projeto foi quantificar essa relação matematicamente para entender:
1.  **Quando** a liquidez dita o preço (tendência macro).
2.  **Quando** fatores internos do criptomercado predominam (ruído e divergência).

---

## 🛠️ A Solução Técnica (Lakehouse)

Construí um pipeline de dados ponta a ponta (**End-to-End**) para cruzar dados macroeconômicos com a ação de preço do Bitcoin, garantindo governança e performance.

### Arquitetura do Pipeline
* **🐍 Ingestão:** Scripts Python conectando nas APIs oficiais do **FRED** (Federal Reserve Economic Data) e **Yahoo Finance**.
* **⚙️ Engenharia:** Processamento no **Databricks (PySpark)** utilizando a **Arquitetura Medalhão**:
    * *Bronze:* Dados brutos.
    * *Silver:* Tratamento de séries temporais e **interpolação de dados** (conversão de frequência mensal para diária).
    * *Gold:* Agregação analítica.
* **📊 Analytics:** Dashboard no **Power BI** com medidas **DAX** avançadas para cálculos de correlação dinâmica e KPIs.

---

## 💡 Insights & Conclusões (A "Verdade" dos Dados)

### 1. A Força da Maré (Correlação 0.62)
O estudo revelou uma correlação de Pearson de **0.62** no longo prazo.
> **Conclusão:** Isso confirma que a Liquidez Global define a **tendência primária** (o "Beta" do mercado). Quando os Bancos Centrais expandem o balanço, o Bitcoin tende a performar positivamente.

### 2. O Perigo da Correlação Cega (Distorções)
Os dados evidenciaram momentos claros de **desacoplamento**.
* **Exemplo Prático:** Em Maio de 2021, a linha de Liquidez (M2) continuou subindo, mas o Bitcoin sofreu uma correção severa de ~50%.
* **Causa:** Fatores exógenos (Banimento da mineração na China) superaram a força da liquidez momentaneamente.

### 🏁 Conclusão Crítica
A Liquidez Global é o **"combustível"**, mas não é o **"piloto"**.
O projeto demonstra que modelos preditivos baseados unicamente em M2 são insuficientes para *market timing* de curto prazo, servindo melhor como indicadores de ciclos macroeconômicos de longo prazo.

---

## 💻 Tech Stack

* **Cloud & Processing:** Azure Databricks, Apache Spark (PySpark).
* **Storage:** Delta Lake (Unity Catalog).
* **Languages:** Python, SQL, DAX.
* **Visualization:** Microsoft Power BI.

