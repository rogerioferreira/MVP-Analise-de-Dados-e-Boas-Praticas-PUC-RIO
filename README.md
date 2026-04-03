# MVP: Análise de Dados e Boas Práticas - PUC-RIO

Projeto apresentado como atividade final da Sprint Análise de Dados e Boas Práticas.

## Sumário executivo

Este projeto realiza uma análise exploratória e a preparação de dados do conjunto "Airline Passenger Satisfaction" (Kaggle) com o objetivo de identificar fatores que influenciam a satisfação geral dos passageiros e preparar os dados para treinamento de modelos de classificação binária (`satisfied` versus `neutral or dissatisfied`). O conjunto final utilizado contém 129.880 registros e 24 atributos, incluindo variáveis sócio demográficas, características de viagem e avaliações de serviços.

As principais etapas executadas foram: obtenção e unificação dos arquivos de treino e teste, limpeza inicial (remoção da coluna `id`), engenharia de atributos com a criação de `Age Group`, análise exploratória de dados para identificação de distribuições, outliers e multicolinearidade, transformação de variáveis (aplicação de `log(1 + x)` em `Departure Delay in Minutes`), construção de pipeline de pré processamento (RobustScaler para numéricas, OrdinalEncoder para binárias, OneHotEncoder para categóricas múltiplas e PCA preservando 95% da variância) e avaliação comparativa de modelos de classificação via validação cruzada.

Dos testes estatísticos realizados, os testes de Qui Quadrado não rejeitaram a hipótese de independência para algumas associações categóricas quando considerados os níveis de significância formais; contudo, a análise visual das tabelas de contingência e mapas de calor indicou associações relevantes, em particular entre `Class` e `satisfaction` e entre `Type of Travel` (viagens a negócios) e `satisfaction`.

A avaliação de importância e correlação entre as variáveis de satisfação do serviço e a variável alvo apontou os seguintes serviços como os mais correlacionados com a satisfação geral: `Online boarding` (correlação aproximada de 0.55), `Inflight entertainment` (0.40), `Seat comfort` (0.36), `On-board service` (0.33), `Leg room service` (0.32) e `Cleanliness` (0.31). A variável `Arrival Delay in Minutes` foi removida devido a forte correlação com `Departure Delay in Minutes` (coeficiente cerca de 0.97) e ocorrência de valores ausentes.

A etapa de modelagem comparou os seguintes classificadores: Random Forest, Logistic Regression, AdaBoost, ExtraTrees e HistGradientBoosting. As métricas consideradas no leaderboard técnico foram acurácia, precisão, recall e F1 score. O melhor modelo, segundo F1 score média em validação cruzada, foi selecionado e ajustado no conjunto de treino completo para avaliação final no conjunto de teste.

Em síntese, o trabalho entregou um pipeline reprodutível de análise e pré processamento, forneceu evidências acerca dos determinantes da satisfação do passageiro e preparou os dados e modelos base para avanços posteriores em produção ou aprofundamento das análises.

## Descrição sucinta do conteúdo

- **Objetivo**: Identificar fatores que impactam a satisfação de passageiros e treinar modelos de classificação binária.
- **Dataset**: "Airline Passenger Satisfaction" (Kaggle). 129.880 registros, 24 atributos após criação de `Age Group`.
- **Hipóteses**:
  - A classe da viagem influencia a satisfação.
  - O objetivo da viagem influencia a satisfação.
  - Existem diferenças por gênero ou faixa etária.
  - Determinar quais serviços influenciam mais a satisfação.

## Metodologia

1. Aquisição e união dos arquivos de treino e teste.
2. Limpeza inicial: remoção da coluna `id` e tratamento de valores ausentes.
3. Engenharia de atributos: criação de `Age Group` com cinco faixas etárias.
4. Análise exploratória: verificação de duplicatas, distribuição das variáveis e identificação de outliers.
5. Tratamento de multicolinearidade: remoção de `Arrival Delay in Minutes` em razão de alta correlação com `Departure Delay in Minutes` e valores ausentes.
6. Transformações: aplicação de `log1p` em `Departure Delay in Minutes` e escalonamento robusto para variáveis numéricas.
7. Pipeline de pré processamento: `RobustScaler`, `OrdinalEncoder` para variáveis binárias, `OneHotEncoder` para variáveis categóricas múltiplas e PCA (n_components=0.95).
8. Divisão de dados: treino e teste com estratificação (test_size=0.2).
9. Modelagem e avaliação: comparação de múltiplos classificadores via validação cruzada (cv=3) e métricas `accuracy`, `precision`, `recall` e `f1`.

## Principais resultados e interpretações

- A variável alvo apresentou desbalanceamento leve, com a classe minoritária representando aproximadamente 43% do total, condição que não exigiu intervenção obrigatória para balanceamento.
- A análise de contingência e mapas de calor indicaram associação visível entre `Class` e `satisfaction`, com maior satisfação observada na classe Business e maior insatisfação em Economic.
- Não foram identificadas diferenças relevantes de percepção de satisfação por `Gender` ou por `Age Group` nas análises estatísticas realizadas.
- Serviços que mais influenciam a satisfação: `Online boarding`, `Inflight entertainment`, `Seat comfort`, `On-board service`, `Leg room service` e `Cleanliness`.

## Conclusões e recomendações

A análise indica que intervenções focadas em melhorar o processo de embarque online, o entretenimento a bordo, o conforto do assento e a limpeza da aeronave tendem a contribuir de forma significativa para o aumento da satisfação dos passageiros. Recomenda-se priorizar ações de melhoria nessas frentes, considerando o retorno potencial em termos de percepção do cliente.

Do ponto de vista metodológico, recomenda-se manter o pipeline de pré processamento implementado neste projeto em etapas futuras, com monitoramento de performance e testes de robustez. Para implantação em produção, sugere-se estudo adicional sobre calibração do modelo, análise de custo de decisões erradas e implementação de monitoramento de deriva de dados.

## Reprodutibilidade

Requisitos principais:

```bash
pip install pandas numpy seaborn matplotlib scipy scikit-learn
```

Execução sugerida:

1. Clonar o repositório.
2. Colocar os arquivos CSV originais em `dados/originais/` ou permitir o fallback para os arquivos remotos conforme implementado no notebook.
3. Abrir e executar o notebook `notebooks/mvp-analise de dados e boas praticas.ipynb` em Jupyter ou Google Colab.

## Estrutura do repositório

- `dados/`  : dados originais
- `notebooks/` : notebook de análise e relatórios
- `modelos/` : artefatos de modelos treinados
- `resultados/` : gráficos e tabelas geradas
- `src/` : código auxiliar

## Referências selecionadas

Lista de referências bibliográficas e recursos utilizados para fundamentação teórica e procedimentos metodológicos conforme o notebook original.
