# AtividadeMachineLearningMLAM

# Análise de Dados e Modelagem de Regressão com Python

Este repositório contém dois notebooks Jupyter desenvolvidos para coletar, estruturar, analisar e treinar modelos de regressão linear (simples e múltipla) utilizando dados reais de atividades econômicas, fluxo rodoviário e geração de energia solar fotovoltaica.

## Estrutura do Repositório

*   **`Notebook_1_PIB_ABCR.ipynb`**: Estudo da relação entre a atividade econômica brasileira (PIB) e o fluxo de veículos nas rodovias (Índice ABCR) para os estados de São Paulo (SP) e Rio de Janeiro (RJ) entre 2006 e 2025.
*   **`Notebook_2_PVGIS_Energia.ipynb`**: Consumo de API externa (PVGIS), engenharia de recursos (limpeza de dados noturnos) e modelagem preditiva da potência de geração fotovoltaica com base em variáveis climáticas e astronômicas.

---

## Detalhes dos Projetos

### 1. Regressão Linear: PIB Regional vs. Índice ABCR (SP e RJ)
O objetivo deste estudo foi investigar o acoplamento entre o crescimento econômico e o setor de transportes/logística de carga rodoviária nas duas maiores economias do país.

*   **Fontes de Dados:** 
    *   **PIB Regional (Número-Índice):** Extraído da Tabela 1620 do IBGE SIDRA.
    *   **Fluxo de Veículos:** Histórico consolidado do fluxo total do Índice ABCR (Associação Brasileira de Concessionárias de Rodovias).
*   **Abordagem de Modelagem:**
    *   **Divisão Cronológica:** Os primeiros 16 anos (2006-2021) foram mantidos fixos para treino e os 4 últimos anos (2022-2025) foram separados para teste (sem embaralhamento, preservando a série temporal).
    *   **Algoritmo:** `LinearRegression` do *scikit-learn*.
*   **Resultados de Destaque:** 
    *   São Paulo apresentou uma correlação linear positiva extremamente forte (\(r \approx 0.98\)), indicando que a variação do PIB explica quase em sua totalidade a movimentação logística do estado (\(R^2 \approx 0.88\) no teste).
    *   O Rio de Janeiro demonstrou menor previsibilidade linear no conjunto de testes pós-pandemia, evidenciando impactos estruturais distintos na dinâmica logística fluminense.

### 2. Regressão Múltipla: Estimativa de Potência Fotovoltaica (API PVGIS)
Este projeto foca no pipeline completo de dados de energia limpa, desde a requisição automatizada via API até a validação de modelos lineares múltiplos.

*   **Fontes de Dados:** 
    *   **API PVGIS (União Europeia):** Coleta de dados horários de radiação e clima baseados no modelo satelitário PVGIS-SARAH3 para a região de São Paulo.
*   **Engenharia de Dados:**
    *   Filtragem estrita de registros noturnos (onde a Irradiância Solar `G(i) == 0`) para evitar viés artificial de acertos nulos nos algoritmos de machine learning.
*   **Modelos Comparados:**
    *   **Modelo 1 (Simples):** Predição de Potência (`P`) utilizando apenas a Irradiância Solar (`G(i)`).
    *   **Modelo 2 (Múltiplo):** Predição utilizando Irradiância, Temperatura do Ar (`T2m`), Velocidade do Vento (`WS10m`) e Altura Solar (`H_sun`).
*   **Resultados de Validação:**
    *   Ambos os modelos alcançaram um coeficiente de determinação espetacular (\(R^2 > 0.99\)).
    *   O **Modelo 2** sagrou-se vencedor em todas as métricas avaliadas (`MAE` reduzido de 9.89 para 9.17 e `MSE` de 163.50 para 143.95), provando que variáveis como a temperatura e velocidade do vento refinam o cálculo da eficiência térmica das placas solares.

---

## Tecnologias e Bibliotecas Utilizadas

O ecossistema de bibliotecas do Python foi utilizado para garantir a reprodutibilidade dos experimentos:

*   **Manipulação e Coleta de Dados:** `requests`, `json`, `pandas`
*   **Análise Gráfica e Visualização:** `matplotlib`, `seaborn`
*   **Computação Científica:** `numpy`
*   **Machine Learning e Estatística:** `scikit-learn`
    *   `LinearRegression`
    *   `train_test_split`
    *   Métricas: `mean_absolute_error` (MAE), `mean_squared_error` (MSE), `r2_score` (R²)

---

##  Como Executar os Notebooks

1. Clone o repositório ou baixe os arquivos dos notebooks.
2. Certifique-se de possuir o Python 3.x instalado.
3. Instale as dependências necessárias executando o comando abaixo no seu terminal:
   ```bash
   pip install requests pandas numpy notebook scikit-learn matplotlib seaborn
   ```
4. Para o **Notebook 1**, garanta que os arquivos de dados brutos (`dados_pib_abcr_sp.csv` e `dados_pib_abcr_rj.csv`) estejam no mesmo diretório do arquivo ou faça o upload diretamente no ambiente do Google Colab.
5. Abra o terminal e inicie o ambiente de desenvolvimento:
   ```bash
   jupyter notebook
   ```
6. Execute as células sequencialmente para reproduzir os gráficos e tabelas de métricas.

---
### Arquivos de Dados Incluídos (.csv)

Para garantir a execução imediata dos códigos do arquivo CP5_2, as bases de dados consolidadas foram incluídas na pasta raiz:
*   `dados_pib_abcr_sp.csv`: Série histórica de 20 anos (2006-2025) contendo as médias anuais do número-índice do PIB do Estado de São Paulo e o Índice ABCR de fluxo total de veículos nas rodovias paulistas.
*   `dados_pib_abcr_rj.csv`: Série histórica idêntica (2006-2025) com os dados econômicos e rodoviários correspondentes ao Estado do Rio de Janeiro.

*(Nota: Os dados de radiação solar e clima do segundo notebook não necessitam de arquivo CSV local, pois são coletados em tempo real diretamente da API oficial do PVGIS).*
