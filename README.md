# Projeto Roof Imóveis:
### Índice

- [1.0 - Business Understanding](#10---business-understanding)
  - [1.1 - Meta](#11---meta)
  - [1.2 - O Caminho Para o Resultado](#12---o-caminho-para-o-resultado)
- [2.0 - O Entendimento do Negócio](#20---o-entendimento-do-negócio)
  - [2.1 - Avaliando a Situação](#21---avaliando-a-situação)
  - [2.2 - Os Dados Disponibilizados](#22---os-dados-disponibilizados)
  - [2.3 - A Relevância dos Dados](#23---a-relevância-dos-dados)
  - [2.4 - A Solução do Problema com os Dados](#10---business-understanding)
- [3.0 - A Coleta dos Dados](#30---a-coleta-dos-dados)
  - [3.1 - Análise dos Dados](#31---análise-dos-dados)
  - [3.2 - Formatação dos Dados](#32---formatação-dos-dados)
  - [3.3 - Exploração de Informações](#33---exploração-de-informações)
- [4.0 - Limpeza dos Dados](#40---limpeza-dos-dados)
  - [4.1 - Remoção de Valores Ausentes](#41---remoção-de-valores-ausentes)
  - [4.2 - Remoção de Outliers](#41---remoção-de-outliers)
- [5.0 - A Exmploração dos Dados](#50---a-exploração-dos-dados)
  - [5.1 - As Métricas Essenciais](#51----as-métricas-essenciais)
- [6.0 - Resultado Da Pesquisa](#60---resultado-da-pesquisa)
  - [6.1 - Os 5 Melhores Imóveis para Investimento](#61---os-5-melhores-imóveis-para-investimento)
  - [6.2 - Os 5 Piores Imóveis para Investimento](#62---os-5-piores-imóveis-para-investimento)



## 1.0 - Business Understanding:

### 1.1 - Meta:
  A meta estabelecida para este Deliverable é indicar para a empresa os cinco melhores imóveis para investimento e indicar os cinco imóveis nos quais eles não devem comprar
  
### 1.2 - O Caminho para o Resultado:
Para obtermos o resultado solicitado pela empresa, será necessário realizarmos uma análise de mercado com base nas informações que temos sobre as vendas dos imóveis

## 2.0 - O Entendimento do Negócio:

### 2.1 - Avaliando a Situação:
A empresa ROOF IMÓVEIS solicitou para analisarmos os melhores imóveis para venda com base em um dataset disponibilizado. Neste contém a base de venda de diversos imóveis do Condado de King – Washington. O dataset disponibilizado nos trás as vendas dos imóveis e suas características no período de Maio de 2014 à Maio de 2015, possuindo um total de 21.613 registros de venda.

### 2.2 - Os Dados Disponibilizados:
Após uma análise inicial dos dados disponibilizados, podemos verificar que o dataset possui as seguintes informações da imagem abaixo.

![DF-Detalhado](/main/imgs/01.png)

### 2.3 - A Relevância dos Dados
Os dados apresentados no dataset disponibilizado apresentam bastante características dos imóveis vendidos, possuindo bastante dados relevantes para a solução proposta.

### 2.4 - A Solução do Problema com os Dados
Apesar de termos bastante informações sobre os imóveis, eles não trazem uma solução direta
para o problema proposto. É necessário realizarmos uma análise mais minuciosa dos dados, para
identificarmos as melhores opções de investimento

## 3.0 - A Coleta dos Dados

### 3.1 - Análise dos Dados
Após importarmos o dataset para o nosso colab, iremos verificar a objetividade de cada
informação contida no dataset.

![Importação dos Dados](/main/imgs/02.png)

Após a importação dos dados, o dataframe nos retornou os dados abaixo.

![DF Importado](/main/imgs/03.png)

### 3.2 - Formatação dos Dados

  Apenas em verificarmos os cinco primeiros registros já é possível observar dados inconsistentes com o proposto da coluna. A coluna ‘DATE’, que era para nos retornar a data da venda do imóvel não está com a formatação de data.
  Com base nesta informação, será necessário verificarmos as colunas do dataset.

![DF-INFO](/main/imgs/04.png)

Verificando os dados das colunas acima, é possível verificar que a coluna DATE está como um **Object**. As colunas **BATHROOMS** e **FLOORS** estão como Float64, o que caracteriza que há números fracionados.

Apesar das colunas BATHROOMS e FLOORS estarem como Float, o padrão americano de considerar ANDAR e BANHEIRO é diferente do padrão Brasileiro. Os Americanos consideram um andar fracionado quando há questão de sótão ou apenas uma parte da casa possui o segundo dar com(ou sem) sacada.

No caso da coluna BATHROOMS, o padrão americano considera cada item como 0.25 da fração de um banheiro, ou seja, uma pia equivale a 0,25 do banheiro, assim como o vaso sanitário, chuveiro e banheira, que completam o 1.0 do banheiro.

Constatado esses dados, é o momento de alterarmos a coluna DATE para uma variável do tipo DATE_TIME

![Transformando Coluna Date para DATE_TIME](/main/imgs/05.png)


### 3.3 - Exploração de Informações

Com os atuais dados do nosso dataset, verificamos que é possível extrair mais informações
sobre os imóveis, tais como:

1. Preço por ft² do terreno
2. Preço por ft² da área habitável do imóvel
3. A cidade do Imóvel

Para o item 1, iremos realizar a adição da coluna **price_sqft_lot** conforme abaixo.
![Item1 - Adição da coluna price_sqft_lot](/main/imgs/06.png)


Para o item 2, iremos realizar a adição da coluna *price_sqft_living*, conforme abaixo.
![Item2 - Adição da coluna price_sqft_living](/main/imgs/07.png)

Para o item 3, iremos realizar a adição da coluna **city**, mas para obter a cidade de cada imóvel, foi necessário criarmos uma função que retorne a cidade conforme o seu **zipcode**.

![Item3 - Adição da coluna city](/main/imgs/08.png)

E por fim, a parte do código que irá preencher a nova coluna com a informação da cidade de cada imóvel.

![Codigo que Adiciona o valor da City](/main/imgs/09.png)


## 4.0 - Limpeza dos Dados

### 4.1 - Remoção de Valores Ausentes

Apesar de ser um dataset com exatos 21.613 registro, o mesmo não possui valores em branco/ausente, conforme a imagem abaixo.

![DF-INFO](/main/imgs/10.png)

Ou seja, não será necessário o tratamento de dados nulos e/ou em branco

### 4.1 - Remoção de Outliers
  Neste tópico, iremos realizar a remoção de alguns dados que não são relevantes para a nossa
análise, conforme abaixo.

![Remoção Outliers](/main/imgs/11.png)


## 5.0 - A Exploração dos Dados

Após removermos alguns outliers da nossa análise, iremos partir para a analise dos dados restantes do nosso dataset.

Nos primeiros passos, iremos realizar algumas filtragens no nosso dataset para prepará-lo para a nossa primeira análise.

![Exploração dos Dados](/main/imgs/12.png)

![Histograma Colunas](/main/imgs/13.png)

Com base nesses dados, iremos aplicar o heatmap para verificar a correlação entre as variáveis.

![Heat Map](/main/imgs/14.png)

Após analisarmos o heatmap acima, podemos constatar que as seguintes colunas possuem uma boa correlação com o **PRICE**, neste caso, iremos fazer uma análise em cima dos dados que possuem maior correlação com o **PRICE**

![Heat Map Price](/main/imgs/15.png)

Através desse novo heatmap, iremos verificar as variáveis que podem influenciar diretamente no valor do imóvel e como o aumento de tal variável fluência no **PRICE**

![Plot Scatter](/main/imgs/16.png)

![Plot Scatter](/main/imgs/17.png)


Com essa Análise acima, podemos verificar que:
1. As Casas com o maior valor de Venda Possuem **4-6 Quartos.** 
2. As Casas com até **4 banheiros** possuem uma relação de maior preço de venda 
3. As Casas com até **5.000ft²** possuem uma melhor volatilidade no preço 
4. As Casas com ft² Acima do solo possui uma influência positiva e uma menor dispersão em até **4000ft²** 
5. As Casas possuem uma boa influência com até **$400/ft²**, após esse valor a dispersão é alta


Na nossa próxima análise, iremos verificar as questões de Condição e Qualidade do material utilizado na casa (campos: **condition** e **grade**)

![Condition & Grade Plot](/main/imgs/18.png)

1. Podemos verificar que a MEDIANA dos Preços com relação a Condition(Condição) da Casa há pouca variação, porém há muitos outliers quando a Condição da casa é de "Mediana" para "Boa" 
2. A variavel **grade** influencia positivamente no preço de venda da Casa, embora que haja muitos outilers das grades de 5 até 11, a qualidade da Casa aumenta a mediana do valor conforme a grade da casa

No próximo passo, iremos analisar a relação do ano de construção da casa com o preço de venda.

![Ano x Valor Venda](/main/imgs/19.png)

Ao analisarmos o valor de venda de cada imóvel conforme o ano de construção do mesmo, conseguimos verificar que as casas construídas no final da década de **30** e as construídas no início década de **40** possuem uma forte desvalorização e as casas construídas partir da década de **70**, as mesmas começam a ser valorizadas 

Nossa próxima etapa foi separar os imóveis por uma categoria com base no material utilizado na construção (**grade**)

Separamos em quatro grupos: 1-3, Bad. 4-6, Average. 7.10, Good. E 11-13, Very Good
![Separação por grade](/main/imgs/20.png)

Podemos verificar que a maioria das casas estão no agrupamento GOOD, grade 7, 8 e 9, e boa parte estão no agrupamento Average.
De forma para melhor visualizarmos o total de cada grupo, iremos aplicar um gráfico de pizza,
podermos analisar cada grupo.

![Pizza por grade](/main/imgs/21.png)


Agora, iremos criar mais um grupo de imóveis, para analisarmos as casas que foram reformadas e as que não passaram por nenhuma reforma.

Com este campo criado, iremos mensurar a quantia de casas reformadas e se a mesma possui relação positiva com o valor de venda.

![Plot Casa Renovada x Não Renovada](/main/imgs/22.png)

Conforme os gráficos acima, há poucas casas que foram reformadas, mas o segundo gráfico indica que a mesma possui uma forte relação com o preço, onde, após uma reforma, o preço da casa tende a subir.

Para melhor analisarmos essa informação, iremos separar essa diferença de valores com os demais grupos conforme a qualidade do material utilizado na casa.

![Plot Casa Renovada x Não Renovada](/main/imgs/23.png)


O gráfico acima indica essa maior relação de preço após a reforma nas casas que possuem a qualidade **GOOD** e **VERY GOOD**. Porém, nas casas do grupo **VERY GOOD**, apresenta uma volatilidade maior dos preços


### 5.1  - As Métricas Essenciais

Após as análises realizadas. Concluímos que:

1. **As casas construídas a partir do ano de 1995**, houve uma melhora no preço de venda das casas;
2. **As casas que não possuem reforma**, tentem a subir o seu preço de venda após uma reforma;
3. **As casas do grupo grade GOOD**, tendem a possuir os melhores preços de venda e uma volatilidade menor no preço após a venda;
4. **As casas com 4 quartos** tendem a possuir os melhores preços de venda
5. **As casas com 3 banheiros** tendem a possuir os melhores preços de venda
6. **As casas com até dois andares** tendem a possuir os melhores preços de venda
7. **As casas com até 3.000ft² acima do solo** tendem a possuir os melhores preços de venda
8. **As casas com até o valor de $400/ft²** tendem a possuir os melhores preços de venda

Com base nessas análises, iremos buscar as melhores opções para investimento, filtrando o nosso dataset.

## 6.0 - Resultado da Pesquisa


### 6.1 - Os 5 Melhores Imóveis para Investimento:

Após aplicar os filtros, ele nos retorna 11 possíveis melhores investimentos para compra.

![Plot Casa Renovada x Não Renovada](/main/imgs/27.png)

Agora, iremos pegar as melhores GRADES que se encaixam no grupo **GOOD** As 2 melhores opções:

![Plot Casa Renovada x Não Renovada](/main/imgs/24.png)

Os ouros 3 melhores imóveis para investir, considerando as casas mais novas. Totalizando os 5 melhores imóveis para investir

![Plot Casa Renovada x Não Renovada](/main/imgs/25.png)

### 6.2 - Os 5 Piores Imóveis para Investimento

Agora iremos analisar os 5 piores imóveis para investimento Com base nas análises, os piores imóveis estão nos seguintes quesitos:
1. Casas com mais de **5 quartos** 
2. Casas com mais de **5 banheiros** 
3. Casas com área habitável **acima de 4000ft²**
4. Casas com o sqft_above **acima de 4500ft²** 
5. Casas com o preço por ft² Acima de **$300/ft²**

![Plot Casa Renovada x Não Renovada](/main/imgs/26.png)

---
Portfólio:  <https://sites.google.com/view/portfoliorafaelzurawski>
Linkedin: <https://www.linkedin.com/in/rafaelzurawski/> 
