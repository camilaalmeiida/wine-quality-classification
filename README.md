# Tech Challenge — Classificação de Qualidade de Vinhos

<a href="https://colab.research.google.com/github/camilaalmeiida/wine-quality-classification/blob/main/notebookfinal.ipynb" target="_parent">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
</a>

## 📌 Objetivo do Projeto
O objetivo deste projeto é desenvolver um modelo de Machine Learning capaz de prever se um vinho é de **alta qualidade** (nota ≥ 7) ou de **baixa/média qualidade** (nota < 7), com base nas suas características físico-químicas.

Esta solução visa automatizar o processo de triagem em tempo real na linha de produção, otimizando o controle de qualidade e priorizando a análise sensorial humana apenas nos casos em que houver maior incerteza ou fronteira de decisão.

---

## 🗺️ Pipeline de Desenvolvimento

O projeto foi conduzido seguindo um pipeline estruturado de Ciência de Dados:

1. **Compreensão do Problema** e modelagem da variável alvo.
2. **Análise Exploratória de Dados (EDA)** para entender distribuições, correlações e desbalanceamento.
3. **Pré-processamento de Dados** e Engenharia de Funcionalidades (*Feature Engineering*).
4. **Desenvolvimento de Modelos** preditivos utilizando diferentes algoritmos.
5. **Avaliação e Comparação** robusta através de múltiplas métricas de classificação.
6. **Interpretação dos Resultados** e insights de negócios para produção.

---

## 📊 O Conjunto de Dados (`WineQT.csv`)

O dataset original possui **1143 linhas e 12 colunas** com medições químicas de amostras de vinho.

### Variável Alvo (Target)
A variável original `quality` foi transformada em uma classificação binária (`high_quality`):
* **Classe 0 (Baixa/Média Qualidade):** Nota original < 7 (Represanta **86.1%** dos dados - 984 amostras).
* **Classe 1 (Alta Qualidade):** Nota original ≥ 7 (Representa **13.9%** dos dados - 159 amostras).

*Nota: O desbalanceamento severo de classes foi identificado na EDA e considerado nas estratégias de modelagem e avaliação.*

---

## 🧪 Engenharia de Funcionalidades (*Feature Engineering*)

Buscando melhorar o poder preditivo do modelo, foram criadas **4 novas features** baseadas no domínio do problema:

1.  **`alcohol_acidity_ratio`**: Razão entre o teor alcoólico e a acidez (mede o equilíbrio na percepção sensorial do vinho).
2.  **`sulphate_chloride_ratio`**: Razão entre sulfatos e cloretos (mede o balanço entre conservantes e salinidade).
3.  **`total_acidity`**: Soma da acidez fixa e acidez volátil (métrica consolidada da acidez total).
4.  **`so2_ratio`**: Proporção entre o dióxido de enxofre livre (*free sulfur dioxide*) e o total (indica a eficiência do conservante ativo).

---

## 🤖 Modelos Desenvolvidos e Resultados

Três algoritmos foram testados utilizando validação cruzada estratificada em 5 fatias (*5-Fold Stratified Cross-Validation*) para garantir a robustez das métricas:

### Tabela Comparativa de Desempenho

| Modelo | Accuracy | Precision | Recall | F1-Score | ROC-AUC | F1 CV (Média) | F1 CV (Std) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Regressão Logística** | 0.7991 | 0.3793 | 0.6875 | 0.4889 | 0.8610 | 0.8386 | 0.0172 |
| **Random Forest** | 0.8777 | 0.5556 | 0.6250 | 0.5882 | 0.8970 | 0.9261 | 0.0096 |
| **Gradient Boosting** | **0.9039** | **0.6667** | **0.6250** | **0.6452** | **0.8936** | **0.9416** | **0.0047** |

---

## 🏆 Modelo Escolhido e Análise Final

O modelo **Gradient Boosting** apresentou o melhor desempenho geral, com uma **Acurácia de 90.39%** e o maior **F1-Score (64.52%)** para a classe minoritária. 

### Principais Conclusões e Insights Práticos:
1.  **Álcool**: Foi identificada como a variável mais preditiva. Processos fermentativos que maximizam e equilibram o teor alcoólico tendem a gerar vinhos com maior pontuação.
2.  **Acidez Volátil**: Deve ser rigorosamente controlada e mantida em níveis baixos, pois valores elevados estão fortemente associados a vinhos classificados como de baixa qualidade.
3.  **Sulfatos**: Dentro dos limites regulatórios e seguros, adições controladas contribuem de forma positiva para a elevação da nota percebida do vinho.

---

## 🛠️ Pré-requisitos e Como Executar

Se preferir rodar o projeto localmente em vez do Google Colab, instale as seguintes dependências:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
