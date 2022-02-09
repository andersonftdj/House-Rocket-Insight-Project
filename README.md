# House-Rocket-Insight-Project
Este é um projeto de insight de uma empresa fictícia do ramo imobiliário.


## 1. Questão de negócio
A House Rocket é uma empresa do ramo imobiliário que tem como modelo de negócio a compra e revenda de casas.

O desafio deste projeto é conseguir identificar bons negócios dentro do portfólio disponível para compra: Casas com preço baixo e um alto potencial de revenda por um preço mais alto. Isso será feito respondendo duas perguntas deixadas pelo CEO:

   1. Quais são os imóveis que a House Rocket deveria comprar e por qual preço?
   2. Uma vez o imóvel foi comprado, qual o melhor momento para vendê-lo e por qual preço?

## 2. Premissa do Negócio
 - Valores de "ID" duplicados foram removidos.
 - Foi criada uma nova coluna para representar as estações do ano, de acordo com as estações  dos Estados Unidos.
 
As variáveis do dataset original são:

Variável | Descrição
---------|----------
|id | Identificador de cada propriedade.|
|date | Data em que a propriedade ficou disponível.|
|price | O preço que cada imóvel foi comprado.|
|bedrooms | Número de quartos.|
|bathrooms | O número de banheiros, o valor 0,5 indica um quarto com banheiro, mas sem chuveiro. O valor 0,75 ou 3/4 banheiro representa um banheiro que contém uma pia, um vaso sanitário e um chuveiro ou banheira.|
|sqft_living | Pés quadrados do interior das casas.|
|sqft_lot | Pés quadrados do terreno das casas.|
|floors | Número de andares.|
|waterfront | Uma variável fictícia para saber se a casa tinha vista para a orla ou não, '1' se a propriedade tem uma orla, '0' se não.|
|view | Vista, Um índice de 0 a 4 de quão boa era a visualização da propriedade.|
|condition | Um índice de 1 a 5 sobre o estado das moradias, 1 indica propriedade degradada e 5 excelente.|
|grade | Uma nota geral é dada à unidade habitacional com base no sistema de classificação de King County. O índice de 1 a 13, onde 1-3 fica aquém da construção e design do edifício, 7 tem um nível médio de construção e design e 11-13 tem um nível de construção e design de alta qualidade.|
|sqft_above | Os pés quadrados do espaço habitacional interior acima do nível do solo.|
|sqft_basement | Os pés quadrados do espaço habitacional interior abaixo do nível do solo.|
|yr_built | Ano de construção da propriedade.|
|yr_renovated | Representa o ano em que o imóvel foi reformado. Considera o número ‘0’ para descrever as propriedades nunca renovadas.|
|zipcode | Um código de cinco dígitos para indicar a área onde se encontra a propriedade.|
|lat | Latitude.|
|long | Longitude.|
|sqft_living15 | O tamanho médio em pés quadrados do espaço interno de habitação para as 15 casas mais próximas.|
|sqft_lot15 | Tamanho médio dos terrenos em metros quadrados para as 15 casas mais próximas.|


## 3. Planejamento da Solução
### 3.1 Produto Final
Será entregue 2 relatórios:
 - Relatório .csv com a sugestão de compra ou não compra de cada um dos imóveis disponíveis
 - Relatório .csv com recomendação do preço de venda das casas.
### 3.2 Ferramentas utilizadas
 - Jupyter Notebook
 - Python 3.8.1

### 3.2 Processo
#### 3.2.1 Estratégia de Solução
 Usando como base a metodologia cíclica do CRISP-DM e adaptando para as necessidades do projeto, a estratégia adotada foi a seguinte:
  1. Entendimento do modelo de negócio da empresa
  2. Entendimento do problema de negócio
  3. Coleta dos Dados
  4. Limpeza dos dados
  5. Análise Exploratória dos Dados
  6. Levantamento de hipóteses
  7. Validação das hipóteses e Insights gerados


#### 3.2.2 Detalhamento da Solução

Recomendação de compra:
  - Coletar os dados.
  - Agrupar os imóveis por região através do zipcode e obter a mediana do preço de cada região.
  - Comparar o preço do imóvel com a mediana do preço da sua região, se for inferior e a condição do imóvel for igual a 4 ou 5, recomendar a compra.
  - Colunas para o relatório:
    - ID
    - zipcode
    - condition
    - price_median_region
    - price   
    - recomendation

Recomendação de venda:
  - Coletar os dados.
  - Agrupar os imóveis por região através do zipcode e obter a mediana do preço da região.
  - Criar uma coluna para as estações do ano.
  - Agrupar os imóveis por estações do ano e obter a mediana do preço.
  - Se o preço do imóvel for menor que a mediana da região e menor que a mediana da estação, recomendar um preço de venda 30% maior.
  - Se o preço do imóvel for maior que a mediana da região e maior que a mediana da estação, recomendar um preço de venda 10% maior.
  - Colunas para o relatório:
    - ID
    - zipcode
    - season
    - price
    - price_median_region
    - price_median_season
    - price_sell_recommendation   
    - profit

## 4. Os 4 Principais Insights de Negócio
### Hipótese 1 -  Imóveis com vista para a água são, na média, 30% mais caros.
  Falso, Na verdade imóveis com vista para o mar são **212% mais caros.**
  * Insight: Prospectar imóveis que tenham vista para a água tem grandes chances de ser mais rentável do que os imóveis sem vista para água.

### Hipótese 2 - Imóveis não reformados são 10% mais baratos que a média dos imóveis reformados por região
  Falso, na verdade, os imóveis não reformados são até 17% mais baratos.
   * Insight: Procurar imóveis não reformados e reformá-los aumentará a valorização do imóvel.

### Hipótese 3 - Imóveis com 3 banheiros ou mais são 20% mais caros do que imóveis com menos que 3 banheiros.
  Falso, não verdade são **105% mais caros.**
  * Insight: Comprar imóveis com menos que 3 banheiros e adicionar banheiros pode ajudar na valorização do imóvel.
 
### Hipótese 4 - Imóveis com 3 quartos ou mais são 20% mais caros do que imóveis com menos que 3 quartos.
  Falso, não verdade são **42% mais caros.**
  * Insight: Comprar imóveis com menos que 3 quartos e adicionar novos quartos também podem ajudar na valorização do imóvel


## 5. Resultados Financeiros Para o Negócio
  De acordo com os critérios estabelecidos, dos 21.435 imóveis disponíveis no portfólio, foram sugeridos a compra de 3.777 imóveis.
 
  Caso se concretize a venda de todos os imóveis sugeridos, será movimentando um total de quase $2 bilhões, gerando um lucro de $463.628.964, isso sem contar nenhuma reforma eventual que agregaria aumentaria mais ainda os lucros.
   
## 6. Conclusão
O objetivo do projeto foi alcançado com sucesso visto que foram gerados dois produtos de dados propostos respondendo às perguntas do CEO da empresa. Os relatórios, disponibilizados através de um arquivo ".csv" estão disponíveis e estes produtos podem servir de apoio para as tomadas de decisão da empresa.


## 7. Próximos Passos
Algumas melhorias podem ser incrementadas no futuro:
 - Disponibilizar os produtos, ao invés de arquivos, dashboards online visando a facilidade do uso e acesso a esses conteúdos.
 - Verificar se a distância da água influencia no preço do imóvel.
