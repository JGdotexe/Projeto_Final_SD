# Projeto_Final_SD


# README – Pipeline de Preparação, Treinamento e Avaliação do Modelo de Detecção de Fraude

Este projeto implementa um pipeline completo para preparar dados, treinar um modelo de classificação binária, avaliar desempenho e gerar gráficos de análise. Todo o fluxo é automatizado por meio do arquivo `run.py`.

---

## 1. Estrutura do Pipeline

O pipeline executa as seguintes etapas, sempre na mesma ordem:

### 1.1. Preparação dos Dados

Arquivo: `prep_credit_data.py`

* Carrega o dataset original `creditcard.csv`.
* Remove outliers com IsolationForest.
* Normaliza atributos numéricos com robust scaling.
* Divide o conjunto em treino e teste.
* Gera os arquivos:

  * `data/train.csv`
  * `data/test.csv`
  * `data/cleaned_full.csv`

---

### 1.2. Treinamento do Modelo

Arquivo: `train_credit_model.py`

* Treina um modelo **LogisticRegression** com ajuste para desbalanceamento.
* Aplica **SMOTE** apenas no conjunto de treino.
* Realiza validação cruzada com 5 folds.
* Calcula métricas como Balanced Accuracy e ROC-AUC.
* Salva o modelo final em:

  * `models/credit_lr_smote.joblib`

---

### 1.3. Avaliação no Conjunto de Teste

Arquivo: `evaluate_test.py`

* Carrega o modelo treinado.
* Avalia no conjunto `data/test.csv`.
* Calcula métricas: Accuracy, Balanced Accuracy, ROC-AUC, PR-AUC e Classification Report.
* Salva:

  * `reports/test_metrics.csv`
  * `reports/confusion_matrix.csv`

---

### 1.4. Busca de Threshold Ideal

Arquivo: `threshold_search.py`

* Utiliza `cleaned_full.csv` para calcular o threshold que maximiza F1.
* Gera um arquivo com o melhor threshold:

  * `reports/best_threshold.csv`

---

### 1.5. Geração de Gráficos

Arquivo: `plot_results.py`

* Gera visualizações usando o modelo treinado e o conjunto de teste:

  * Curva ROC
  * Curva Precision-Recall
  * Histograma dos scores do modelo
  * Matriz de confusão no melhor threshold

Os arquivos gerados são salvos em `reports/`:

* `roc_curve.png`
* `pr_curve.png`
* `score_hist.png`
* `confusion_matrix.png`

---

## 2. Automação com run.py

O arquivo `run.py` executa automaticamente todas as etapas acima:

1. Preprocessamento
2. Treinamento
3. Avaliação
4. Seleção do melhor threshold
5. Geração dos gráficos

Para executar o pipeline completo:

```
python3 run.py
```

---

## 3. Requisitos

Instale as dependências:

```
pip install -r requirements.txt
```

O arquivo inclui:

* pandas
* numpy
* scikit-learn
* imbalanced-learn
* matplotlib
* joblib

---

## 4. Estrutura Final do Projeto

```
project/
├── creditcard.csv
├── prep_credit_data.py
├── train_credit_model.py
├── evaluate_test.py
├── threshold_search.py
├── plot_results.py
├── run.py
├── requirements.txt
├── data/
│   ├── cleaned_full.csv
│   ├── train.csv
│   └── test.csv
├── models/
│   └── credit_lr_smote.joblib
└── reports/
    ├── test_metrics.csv
    ├── confusion_matrix.csv
    ├── best_threshold.csv
    ├── roc_curve.png
    ├── pr_curve.png
    ├── score_hist.png
    └── confusion_matrix.png
```

---

## 5. Objetivo

O objetivo deste pipeline é disponibilizar uma solução completa para detecção de fraude em transações, cobrindo:

* Tratamento automático dos dados
* Treinamento de modelo com técnicas para lidar com desbalanceamento
* Avaliação rigorosa com diversas métricas
* Seleção do threshold ideal
* Visualização final dos resultados

---

Se desejar, posso gerar um README mais formal, técnico ou acadêmico.
