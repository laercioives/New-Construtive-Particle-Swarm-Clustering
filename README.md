# New Constructive Particle Swarm Clustering (NcPSC)

Este repositório contém a implementação em Python 3 do **New Constructive Particle Swarm Clustering (NcPSC)**, um algoritmo de inteligência de enxames voltado para a classificação de dados baseado em protótipos. O modelo original foi proposto na minha dissertação de mestrado e, posteriormente, adaptado para rodar nativamente com o ecossistema `scikit-learn` (através de estruturas como `BaseEstimator` e `ClassifierMixin`), permitindo validação cruzada e otimização de hiperparâmetros.

---

## 📚 Fundamentação Teórica e Aplicações

O desenvolvimento e a evolução do NcPSC estão documentados em duas publicações principais da minha trajetória acadêmica:

### 1. Proposta Original (Mestrado)
* **Artigo:** *A New Constructive Particle Swarm Clustering Algorithm* (TEMA, 2021)
* **Link:** [scielo.br/j/tema/...](https://www.scielo.br/j/tema/a/syRTxnR9KbH3fgKNBscrPMN/?lang=en)
* **Resumo Simples:** Este trabalho introduz a arquitetura do NcPSC como um algoritmo construtivo baseado em Otimização por Enxame de Partículas (PSO). Em vez de usar uma população estática, o enxame inicia com centros gerados por agrupamento subtrativo e evolui dinamicamente por meio de operadores de **clonagem (mutação)** para cobrir áreas densas de dados e **eliminação** de partículas inativas (sem vitórias). O algoritmo ajusta a classe majoritária e os raios de influência de cada partícula, gerando de forma autônoma protótipos eficientes para representar o espaço de características.

### 2. Extensão e Aplicação (Doutorado)
* **Artigo:** *Swarm intelligence and fuzzy sets for bed exit detection of elderly * (JIFS, 2020)
* **Link:** [https://journals.sagepub.com/doi/abs/10.3233/JIFS-191971)
* **Resumo Simples:** As quedas em idosos são um problema de saúde pública porque essa população tende a ter um tempo de recuperação mais longo e, consequentemente, maior permanência em leitos hospitalares. Estudos mostram que 84% das quedas em quartos de hospital ocorrem perto da cama, o que levou ao estudo de estratégias para prevenir quedas na população idosa. Neste contexto, este artigo apresenta um esquema para a detecção e emissão de alertas de saída de leito em idosos. Este esquema utiliza sinais derivados de sensores RFID processados por um modelo baseado em Inteligência de Enxames e Conjuntos Fuzzy. A principal contribuição deste estudo é o uso de Janelas de Pertencimento (Membership Windows) que reduzem os efeitos de erros de classificação de outras estratégias. O trabalho proposto avaliou um conjunto de dados contendo 14 idosos com idades entre 66 e 86 anos divididos em dois quartos. Os resultados mostram que a abordagem apresentada melhora a precisão e a sensibilidade (recall) em ambientes com maior incerteza de classificação..

---

## ⚡ Vantagens da Abordagem Baseada em Protótipos

A classificação por protótipos (ou centros de massa) gerada pelo NcPSC oferece benefícios significativos quando comparada a classificadores tradicionais:

* **Separação de Problemas Não-Lineares:** Ao contrário de classificadores lineares rígidos, o NcPSC consegue mapear e classificar dados em **problemas que não são linearmente separáveis**. Como o enxame espalha múltiplos protótipos esféricos ou hiperbólicos pelo espaço, ele consegue circundar e isolar fronteiras de decisão complexas e sinuosas.
* **Topologia Dinâmica e Construtiva:** O algoritmo não exige que você adivinhe o número ideal de partículas/regras no início. Ele cria protótipos onde há necessidade (clonagem) e limpa o excesso onde há redundância (eliminação).
* **Interpretabilidade do Modelo:** Cada partícula final representa um "centro de gravidade" real de uma classe. Isso torna o modelo explicável, permitindo analisar visualmente e geometricamente o que cada protótipo aprendeu do problema.
* **Baixo Custo Computacional no Predict:** Após o treino (fase de enxame), a classificação de novas amostras resume-se a um cálculo rápido de distância euclidiana até os poucos protótipos sobreviventes, tornando o modelo ideal para sistemas de tempo real.

---

## 🛠️ Como Executar o Código

A versão atual foi componentizada para suportar buscas em grade (`GridSearchCV` ou `RandomizedSearchCV`) e validação cruzada em 5-fold utilizando o dataset Iris como benchmark.

### Pré-requisitos
```bash
pip install numpy matplotlib scikit-learn
