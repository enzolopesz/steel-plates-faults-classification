# Steel Plates Faults Classification

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Machine Learning](https://img.shields.io/badge/Machine%20Learning-Classification-orange)
![Status](https://img.shields.io/badge/Status-MVP-green)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

Projeto de Machine Learning aplicado à classificação de defeitos em chapas de aço a partir de atributos numéricos de inspeção industrial.

O objetivo do MVP é comparar modelos supervisionados de classificação multiclasse e selecionar uma abordagem inicial capaz de apoiar a identificação automática do tipo de falha em um cenário de controle de qualidade.

---

## Visão geral

A base utilizada é a **Steel Plates Faults**, disponibilizada pela UCI Machine Learning Repository. Ela contém registros de defeitos em chapas de aço, com variáveis numéricas extraídas do processo de inspeção e sete classes possíveis de falha.

O problema foi tratado como uma tarefa de **classificação multiclasse supervisionada**, onde a variável-alvo foi criada a partir das colunas originais de defeito em formato one-hot.

---

## Objetivo do projeto

Desenvolver um MVP de Machine Learning capaz de:

- carregar e preparar os dados de inspeção;
- transformar as classes originais em uma variável-alvo única;
- avaliar a distribuição das classes;
- evitar vazamento de dados durante a preparação;
- comparar modelos de classificação;
- otimizar hiperparâmetros do melhor candidato;
- avaliar o desempenho final com métricas adequadas para classes desbalanceadas.

---

## Dataset

**Fonte:** UCI Machine Learning Repository  
**Base:** Steel Plates Faults  
**Tipo de problema:** Classificação multiclasse  
**Quantidade de registros:** 1.941  
**Atributos de entrada:** 27 variáveis numéricas  
**Classes de saída:** 7 tipos de defeito

Classes avaliadas:

- Pastry
- Z_Scratch
- K_Scatch
- Stains
- Dirtiness
- Bumps
- Other_Faults

---

## Metodologia

O desenvolvimento foi estruturado em etapas:

1. Importação das bibliotecas e definição da seed.
2. Download e carregamento automático da base pública.
3. Análise inicial dos dados.
4. Conversão das colunas one-hot em uma única variável-alvo.
5. Análise da distribuição das classes.
6. Separação entre treino e teste com estratificação.
7. Criação de baseline com `DummyClassifier`.
8. Treinamento de modelos candidatos.
9. Validação cruzada com múltiplas métricas.
10. Otimização com `GridSearchCV`.
11. Avaliação final em dados de teste.
12. Análise de matriz de confusão e importância das variáveis.

---

## Modelos avaliados

Foram comparados os seguintes modelos:

| Modelo | Papel no MVP |
|---|---|
| DummyClassifier | Baseline mínimo |
| Logistic Regression | Modelo linear interpretável |
| Random Forest | Modelo de árvores para dados tabulares |
| HistGradientBoosting | Modelo baseado em boosting |

A métrica principal adotada foi **F1 macro**, pois o dataset possui desbalanceamento entre classes e a acurácia isolada poderia mascarar baixo desempenho em classes menores.

---

## Resultado final

O melhor modelo selecionado foi o **Random Forest**.

| Métrica em teste | Resultado |
|---|---:|
| Accuracy | 0.8046 |
| Balanced Accuracy | 0.7942 |
| F1 Macro | 0.8264 |
| F1 Weighted | 0.8041 |

O modelo superou o baseline e apresentou desempenho consistente para um MVP inicial, principalmente considerando a natureza multiclasse e o desbalanceamento das classes.

---

## Principais aprendizados

- A separação correta entre variáveis preditoras e variável-alvo foi essencial para evitar vazamento de dados.
- A distribuição das classes mostrou desbalanceamento relevante.
- Métricas como **F1 macro** e **balanced accuracy** foram mais adequadas que apenas acurácia.
- Modelos baseados em árvores tiveram desempenho superior aos modelos lineares neste conjunto de dados.
- A base é útil para um MVP, mas uma aplicação real exigiria validação com dados atuais do processo produtivo.

---

## Limitações

Este projeto representa um MVP e possui algumas limitações:

- a base é pública e não necessariamente representa um processo industrial atual;
- não há informação sobre custo operacional de cada tipo de erro;
- o modelo ainda não foi validado em ambiente produtivo;
- não foi feita análise de drift ou monitoramento pós-deploy;
- a otimização de hiperparâmetros foi limitada para manter o escopo do MVP.

---

## Próximos passos

Possíveis evoluções do projeto:

- testar o modelo com dados reais de produção;
- avaliar custo por tipo de erro;
- criar uma API simples para inferência;
- salvar o modelo treinado com `joblib`;
- montar um dashboard de monitoramento;
- acompanhar métricas em produção;
- validar o modelo com especialistas do processo industrial.

---

## Estrutura do repositório

```text
steel-plates-faults-classification/
├── steel_plates_faults_mvp.ipynb
├── requirements.txt
├── .gitignore
├── LICENSE
└── README.md
```

---

## Como executar

Clone o repositório:

```bash
git clone https://github.com/enzolopesz/steel-plates-faults-classification.git
cd steel-plates-faults-classification
```

Crie um ambiente virtual:

```bash
python -m venv .venv
```

Ative o ambiente virtual:

```bash
# Windows
.venv\Scripts\activate

# Linux/Mac
source .venv/bin/activate
```

Instale as dependências:

```bash
pip install -r requirements.txt
```

Abra o notebook:

```bash
jupyter notebook steel_plates_faults_mvp.ipynb
```

---

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

---

## Autor

**Enzo de Sousa Lopes**

Projeto desenvolvido como MVP de Machine Learning & Analytics, com foco em aplicação de modelos supervisionados para classificação de defeitos industriais.

---

## Licença

Este projeto está sob a licença MIT.
