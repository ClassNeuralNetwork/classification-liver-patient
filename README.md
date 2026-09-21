# 🔬 Diagnóstico de Doenças Hepáticas com Multilayer Perceptron (MLP) e Interpretabilidade por SHAP

![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Latest-green.svg)
![License](https://img.shields.io/badge/License-MIT-brightgreen.svg)

Este repositório contém a implementação completa de um modelo de **Redes Neurais Artificiais (RNA)** do tipo **Perceptron Multicamadas (MLP)** para o auxílio no diagnóstico prévio de doenças hepáticas, utilizando dados clínicos e exames laboratoriais do *Indian Liver Patient Dataset* (ILPD).

Além da classificação binária, o projeto integra a técnica de **SHAP (*SHapley Additive exPlanations*)** para promover a interpretabilidade do modelo, superando o desafio do comportamento "caixa-preta" em aplicações médicas.

---

## 📌 Informações Acadêmicas

* **Instituição:** Universidade Federal Rural do Semi-Árido (UFERSA)
* **Disciplina:** Redes Neurais Artificiais
* **Docente:** Profª. Drª. Rosana Cibely Batista Rego

---

## 📊 Visão Geral do Projeto

O objetivo principal é classificar indivíduos entre **Saudável** (classe 0) e **Doente** (classe 1) a partir de 10 atributos clínicos e demográficos.

### Principais Resultados Obtidos
* **Acurácia Geral:** **77.78%** no conjunto de teste.
* **Recall (Classe Doente):** **0.86 (86%)**, garantindo alta sensibilidade na captura de pacientes enfermos (fator crítico para triagem médica).
* **F1-Score Ponderado:** **0.78**.

---

## 🛠️ Arquitetura e Pipeline do Modelo

1. **Pré-processamento:**
   * Imputação de dados ausentes na variável `alkphos` utilizando a mediana.
   * Codificação da variável categórica `gender` (Male = 1, Female = 0).
   * Mapeamento da variável alvo `is_patient` (Doente = 1, Saudável = 0).
   * Divisão estratificada dos dados (80% treino / 20% teste).
   * Padronização das *features* via `StandardScaler`.

2. **Arquitetura da Rede Neural (Keras / TensorFlow):**
   * **Camada de Entrada:** 10 neurônios (atributos clínicos).
   * **1ª Camada Oculta:** 32 neurônios com ativação `ReLU`.
   * **2ª Camada Oculta:** 16 neurônios com ativação `ReLU`.
   * **Camada de Saída:** 1 neurônio com ativação `Sigmoid` (probabilidade do diagnóstico).
   * **Otimizador:** Adam.
   * **Função de Perda:** Binary Crossentropy.

3. **Interpretabilidade (SHAP):**
   * Utilização do `KernelExplainer` para mapear a relevância individual e o impacto positivo/negativo de cada exame no diagnóstico gerado pela rede.

---

## 🔍 Interpretabilidade com SHAP

A análise via SHAP revelou que:
* **Idade (`age`):** Atributo de maior impacto no modelo, onde idades mais avançadas impulsionam a previsão para a classe **Doente**.
* **Enzimas Hepáticas (`sgpt` e `sgot`) e Bilirrubinas:** Níveis alterados atuam como indicadores fundamentais na tomada de decisão da rede neural, alinhando as previsões matemáticas com a prática médica real.
