# 🏠 Projeto de Insights: House Rocket

O objetivo desse projeto é fornecer para o time de negócios a seleção de imóveis dada algumas condições pré-estabelecidas para dar um suporte para a empresa de quais imóveis deverão ser comprados ou vendidos. Outro aspectos que realizamos é a validação de hipótestes de negócios das quais visam demonstrar um valor de lucro máximo que a empresa pode obter dado as condições que a mesma pode definir num segundo momento.

Além da nossa análise contida através da ferramenta "Jupyter notebook", iremos gerar uma outra ferramenta de visualização utilizada nesse projeto, chamada de "Streamlit", gerando no final um link que permitirá a empresa visualizar a base de dados selecionada, para que esta possa pesquisar e explorar os dados de maneira dinâmica, contendo nesta tanto tabelas como mapas.

O resultado geral obtido foi uma seleção de __12.975 imóveis__ que corresponde a quase 50% dos imóveis do banco de dados disponibilizado.

Assumindo definiu os percentuais de 30% e 10% de margem de lucro(conforme detalhes nos tópicos 1.4 e 2.2b, o lucro máximo que poderá ser obtido com as operações é de __US$ 977.825.261,30__

| __Número de imóveis__ | __Custo total__ | __Receita de vendas__ | __Lucro (profit)__ |
| ----------------- | ----------------- | ----------------- | ----------------- |
| 12.975 | US$ 5.345.126.211,00 | US$ 6.322.951.472,29 | US$ 977.825.261,30 |
___
### 👨‍💼 Contexto do negócio:

A House Rocket é uma plataforma digital que tem como modelo de negócio, a compra e a venda de imóveis usando a tecnologia para analisar suas melhores oportunidades.

O objetivo do case é fornecer insights para a empresa encontrar as melhores oportunidades de negócio no mercado de imóveis. O CEO da House Rocket gostaria de ***maximizar*** a receita da empresa encontrando ***boas oportunidades*** de negócio.

Sua principal estratégia é ***comprar boas casas*** em ótimas localizações com preços baixos e depois revendê-las posteriormente a preços mais altos. Quanto maior a diferença entre a compra e a venda, maior o lucro da empresa.

Entretanto, as casas possuem muitos atributos que as tornam mais ou menos atrativas aos compradores e vendedores, e a localização e o período do ano também podem influenciar os preços.
___
### 👨‍💼 Questão do negócio:

O objetivo desse projeto é fornecer uma seleção de imóveis, dadas algumas premissas pré-estabelecidas por nós, tendo o intuito de dar um melhor embasamento para a empresa  realizar a compra e venda de imóveis. Com isso  realizaremos o planejamento que seria demonstrar quais as melhores oportunidades e qual resultado (lucro) máximo que pode ser alcançado, tendo o projeto o objetivo principal de responder às seguintes perguntas de negócio:

- ___Quais são os imóveis que a empresa deveria comprar e por qual preço ?___
- ___Uma vez a casa comprada, qual o melhor momento para vendê-las e por qual preço ?___
___
### 📚 Dados:

Os dados foram extraídos da plataforma "Kaggle", usando o link abaixo:

https://www.kaggle.com/harlfoxem/housesalesprediction

Contendo os seguintes atributos:

|***Atributo*** | ***Descrição*** |
| -------- | --------- |
|**id** | Numeração única de identificação de cada imóvel |
|**date** | Data da venda da casa |
|**price** | Preço de venda da casa |
|**bedrooms** | Número de quartos |
|**bathrooms** | Número de banheiros (0.5 = banheiro em um quarto, mas sem chuveiro) |
|**sqft_living** | Medida (em pés quadrado) do espaço interior dos apartamentos |
|**sqft_lot** | Medida (em pés quadrado)quadrada do espaço terrestre |
|**floors** | Número de andares do imóvel | 
|**waterfront** | Variável que indica a presença ou não de vista para água (0 = não e 1 = sim) | 
|**view** | Um índice de 0 a 4 que indica a qualidade da vista da propriedade. Varia de 0 a 4, onde: 0 = baixa 4 = alta | 
|**condition** | Um índice de 1 a 5 que indica a condição da casa. Varia de 1 a 5, onde:1 = baixo 5 = alta | 
|**grade** | Um índice de 1 a 13 que indica a construção e o design do edifício. Varia de 1 a 13, onde: 13 = baixo, 7 = médio e 1113 = alta | 
|**sqft_basement** | A metragem quadrada do espaço habitacional interior acima do nível do solo | 
|**yr_built** | Ano de construção de cada imóvel | 
|**yr_renovated** | Ano de reforma de cada imóvel (0 = nunca foram reformadas) | 
|**zipcode** | CEP da casa | 
|**lat** | Latitude | 
|**long** | Longitude | 
|**sqft_livining15** | Medida (em pés quadrado) do espaço interno de habitação para os 15 vizinhos mais próximo | 
|**sqft_lot15**| Medida (em pés quadrado) dos lotes de terra dos 15 vizinhos mais próximo | 
___
### 💼 Premissas do negócio:

Com o entendimento dos negócios e dados, exploração dos dados e decisão para fornecer os insights finais, foram adotadas as seguintes premissas:

- O valor igual a 33 na coluna *bathroom* foi considerada um erro e por isso foi delatada das análises. Possivelmente poderia ser um erro de digitação, mas por falta dessa clareza, a exclusão foi optada;
- A coluna *price* é referente ao preço em que a casa foi ou será comprada pela empresa House Rocket;
- Dado que a __localidade__ e a __condição__ são os principais fatores que influenciam na valorização ou desvalorização dos imóveis, essas foram características decisivas na seleção ou não dos imóveis.
- Os anos de construção (yr_built) igual a 0, foram substituídos pela data 01-01-1970.

Como a sazonalidade também influencia diretamente a demanda por investimento em imóveis, a estação do ano foi a característica decisiva para a época da venda do imóvel (*https://blog.loft.com.br/sazonalidade/*)

___Premissa relevante: Com o nosso conhecimento sobre o negócio aplicaremos um percentual de 30% sobre o valor dos imóveis compradas no valor abaixo do valor mediano da região + sazonalidade, e de 10% nos imóveis comprados acima do valor mediano da região + sazonalidade___
___
## Planejamento da solução:

### 🗺️ Exploração e Alteração de dados:

A primeira etapa do projeto foi realizar a coleta, tratamento e exploração dos dados. Nessa etapa foi possível realizar identificar necessidades de limpeza e transformação dos dados, sendo que neste projeto, realizamos uma análise estatística descritiva do conjunto de dados assim como também a criação de novas *features* para facilitar e proporcionar as visualizações e criações dos insights gerados a partir de hipótese de negócios que serão apresentados. A motivação da criação das novas features serão explanadas em outro momento.

  - *season:* estação do ano da venda do imóvel
  - *yr_life:* anos de vida do imóvel.
  - *level:* separa o preço dos imóveis em quartis, classificando  

### 📑 Hipóteses de negócios:

No intuito de melhor entender o negócio assim como auxiliar na análise exploratória, realizamos algumas hipóteses:

| __Hipótese__ | __Resultado__ | __Tradução para negócio__ |
| ------------ | ------------ | ------------ |
| __H1__ -Imóveis com vista para a água são em média mais caros se sim em quantos %? | Verdadeira | Imóveis com vista para água são aproximadamente 50% mais caros. Procurar investir em imóveis sem vista para água, por terem custo de negócio menor |
| __H2__ - Imóveis antigos são mais baratos, se sim em quantos %? | Falsa | A idade dos imóveis não contribui para a diminuição do preço dos imóveis |
| __H3__ - Quais são os atributos que mais contribuem para o aumento do preço? | - | Os atributos que contribuem para o aumento do preços são: ***quantidade de banheiros***, ***design do edifício*** e a ***área do imóvel*** |
___
### Seleção dos imóveis:

Para iniciar a resposta para as perguntas de negócio, foram realizados os seguintes passos:

__Quais são os imóveis que a House Rocket deveria comprar e por qual preço ?__
- Agrupar os imóveis por região ( *zipcode* );
- Cálculo da mediana dos preços pelo cep.
- Com a mediana calculada estabelecemos a seguintes cenários para realizar a compra de um imóvel: <br><br>
    - ***Cenário 1:***  Iremos comprar (Buy) se o preço do imóvel for menor que a média dos preços e a condição for maior que 3: <br>
    -    Compra = ( Preço < Média dos preços ) & (Condição >= 3)<br><br>
    - ***Cenário 2:***  Iremos comprar (Buy) se o preço do imóvel for menor que a média dos preços e a avaliação do design do edifício for maior que 7:<br>
    -    Compra = ( Preço < Média dos preços ) & (Design Edifício >= 7)<br><br>
    - ***Cenário 3:*** Iremos comprar (Buy) se o preço do imóvel for menor que a média dos preços, a condição for maior que 3 e a avaliação do design do edifício for maior que 7:<br>
    -    Compra = ( Preço < Média dos preços ) & (Condição >= 3) & (Design Edifício >= 7)

__Uma vez a casa comprada, qual o melhor momento para vendê-las e por qual preço ?__
- Com os dados selecionados da questão anterior, vemos que estes variam o preço conforme a temporada, com isso iremos agrupa-los por região ( *zipcode* ) e também por temporada (*season*);
- Dentro de cada região e temporada, calculamos a mediana do preço do imóvel em cada sazonalidade.
- Em seguida, calculamos o preço de venda dos imóveis levando em consideração as seguintes condições:

   1. Se o preço da compra for maior que a mediana da região + sazonalidade. O preço da venda será igual ao preço da compra + 10%
       - Preço Venda = Preço > Mediana Sazonalidade x 1,10
   2. Se o preço da compra for menor que a mediana da região + sazonalidade. O preço da venda será igual ao preço da compra + 30%
       -  Preço Venda = Preço < Mediana Sazonalidade x 1,30

## 📈 Resultados financeiros:

O objetivo desse projeto era responder as questões de negócio e fornecer uma lista de imóveis com opções de compra e venda, e consequentemente o __lucro máximo__ que poderá ser obtido se todas as transações ocorrerem. Sendo que o resultado financeiro previsto caso todas essas transações ocorram seria de acordo com a tabela abaixo

| __Número de imóveis__ | __Custo total__ | __Receita de vendas__ | __Lucro (profit)__ |
| ----------------- | ----------------- | ----------------- | ----------------- |
| 12.975 | US$ 5.345.126.211,00 | US$ 6.322.951.472,29 | US$ 977.825.261,30 |

## 😄 Conclusão:

O projeto tem como princípio responder a questão de negócio assim como gerar insights baseados em hipóteses de negócios que formulamos ou que foram trazidas pela empresa. Com esse problema respondido geramos o lucro total que seria gerado em nossa análise caso as nossas pré condições fossem estabelecidas.
