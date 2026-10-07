# CP2_Modelagem_linear

Grupo:
Lucas Furquim 568690
Gustavo Torres de Oliveira 572952
Diogo Chiaradia 570246

**Recorte geográfico:** Brasil  
**Período analisado:** 2006 a 2025

# Regressão Linear com PIB e Índice ABCR

## Sobre o projeto

Este projeto investiga a relação entre a atividade econômica brasileira e o fluxo de veículos nas rodovias no período de 2006 a 2025.

Para representar a atividade econômica, foi utilizado o índice de volume do Produto Interno Bruto (PIB). Para representar o fluxo de veículos, foi utilizado o Índice ABCR de fluxo total.

Além da análise da correlação entre os indicadores, foi desenvolvido um modelo de regressão linear simples para estimar o Índice ABCR a partir do índice de volume do PIB.

## Fontes dos dados

### IBGE

Os dados do PIB foram obtidos na Tabela 1620 do Sistema IBGE de Recuperação Automática (SIDRA).

Foi considerada a série sem ajuste sazonal do PIB a preços de mercado, utilizando o índice de volume cuja média de 1995 corresponde a 100.

Fonte:
https://sidra.ibge.gov.br/tabela/1620

### Índice ABCR

Os dados referentes ao fluxo de veículos foram obtidos no Índice ABCR, considerando o fluxo total de veículos no Brasil e a série original, sem ajuste sazonal.

Fonte:
https://melhoresrodovias.org.br/indice-abcr_2/

## Preparação dos dados

Foram utilizados 20 anos completos em comum, de 2006 a 2025.

Como o PIB possui dados trimestrais e o Índice ABCR possui dados mensais, os indicadores foram transformados em médias anuais:

- PIB_indice: média dos quatro índices trimestrais do PIB;
- ABCR_indice: média dos doze índices mensais do Índice ABCR.

A base final possui as colunas:

- Ano
- PIB_indice
- ABCR_indice

## Análise exploratória

Foi calculada a correlação de Pearson entre o índice de volume do PIB e o Índice ABCR.

A correlação encontrada foi de:

**0,9725**

O resultado indica uma associação linear positiva muito forte entre os indicadores no período analisado.

Uma correlação elevada, entretanto, não demonstra uma relação de causa e efeito.

## Modelo de regressão linear

Foi utilizada a classe `LinearRegression` da biblioteca scikit-learn.

A divisão dos dados foi realizada de forma cronológica:

- Treinamento: 2006 a 2021 (16 anos);
- Teste: 2022 a 2025 (4 anos).

Os registros não foram embaralhados.

A variável de entrada (`X`) foi `PIB_indice` e a variável estimada (`y`) foi `ABCR_indice`.

## Resultados

O modelo foi avaliado no conjunto de teste utilizando MAE, MSE e R².

| Métrica | Resultado |
|---|---:|
| Correlação de Pearson | 0,9725 |
| MAE | 3,2934 |
| MSE | 12,6215 |
| R² | 0,7474 |

O MAE indica que as previsões ficaram, em média, aproximadamente 3,29 pontos do Índice ABCR distantes dos valores observados.

O R² de 0,7474 indica que, no conjunto de teste, o modelo explicou aproximadamente 74,74% da variação observada do Índice ABCR.

## Dificuldades encontradas

Uma das principais dificuldades foi garantir a utilização da série original do Índice ABCR, uma vez que também existem informações referentes à série dessazonalizada.

Outra dificuldade foi compatibilizar as diferentes frequências dos indicadores. O PIB possui dados trimestrais, enquanto o Índice ABCR possui dados mensais. A solução adotada foi transformar ambas as séries em médias anuais.

Também foi preservada a ordem cronológica dos dados durante a divisão entre treinamento e teste.

## Conclusão

Os resultados mostram uma forte associação positiva entre o índice de volume do PIB e o fluxo de veículos representado pelo Índice ABCR.

O modelo de regressão linear simples apresentou estimativas relativamente próximas dos valores observados no período de teste.

Entretanto, o PIB não explica sozinho todas as alterações no fluxo de veículos. Outros fatores econômicos, logísticos e relacionados à mobilidade também podem influenciar o Índice ABCR.

Por fim, a elevada correlação encontrada não deve ser interpretada como evidência de uma relação causal.

## Arquivos do repositório

- `README.md` — descrição do projeto e principais resultados;
- `regressao_pib_abcr.ipynb` — notebook contendo preparação dos dados, gráficos, regressão e avaliação;
- `dados_anuais_pib_abcr_2006_2025.csv` — base utilizada na análise.

## Tecnologias utilizadas

- Python
- Pandas
- Matplotlib
- Scikit-learn
- Google Colab
