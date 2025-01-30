### Análise de concorrentes para empresa de Marketing

-----------
### Sumário

[Dashboard Final](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#dashboard-final)  

[Propósito](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#prop%C3%B3sito)

[Contexto do Projeto](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#Contexto-do-Projeto)  

* [Dataset](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#dataset)
     - [Extração dos dados](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#extração-dos-dados)
     - [Schema](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#schema)
     - [Visualização dos Anúncios](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#visualização-dos-anúncios)
     - [Power Query](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#power-query)
 
* [Exploração dos Dados](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#exploração-dos-dados)
     - [Métricas Gerais](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#métricas-gerais)
     - [Principais anunciantes](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#principais-anunciantes)
     - [Se aprofundando nas publicações](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#se-aprofundando-nas-publicações)
 
* [Conclusão e Criação do Dashboard](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#conclusão-e-criação-do-dashboard)
     
[Notas e Advertências](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#notas-e-advertências)

[Demo Dashboard](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/README.md#demo-dashboard)

## Dashboard Final

> [!NOTE]  
> Caso queira visualizar o resultado final, o link para o Dashboard se encontra aqui -> [Dashboard v1.0](https://app.powerbi.com/view?r=eyJrIjoiNjY4ODQ1ZjEtZDUxNS00MGZmLWFlYzctZDExZDQ0NjhhYWJmIiwidCI6ImU3ODllZDJmLWQ3YTUtNDJlMy1iODllLWJlOGE4YjJjZTY5YSJ9)
> 
> Se houver interesse em saber mais a respeito do processo de criação do projeto, as informações a seguir documentam partes da realização do mesmo. Obrigado.

## Propósito

Criar um dashboard interativo para a empresa conseguir visualizar informações sobre os anúncios publicados nas plataformas do Google.

## Contexto do Projeto

A agência de marketing que solicitou o serviço me autorizou utilizar o projeto para eu mostrar no meu portfólio porém pediu que utilizassemos outro nome, com isso vou chama-la de M1 (marketing 1). A princípio eu entrei em contato com eles para vender uma ideia que tive sobre um dashboard que pudesse auxilia-los em observar métricas de propagandas do google.
O objetivo principal é criar um dashboard que forneça à agência informações detalhadas sobre as propagandas utilizadas por outras empresas e indivíduos. O dashboard deve possibilitar a filtragem do conteúdo e exibir visualizações que ajudem na tomada de decisões para futuros anúncios.
Isso é possível por que o Google o *Ads transparency Center* que é uma ferramenta que oferece maior transparência sobre os anúncios exibidos na plataforma. Ele permite que os usuários visualizem informações detalhadas sobre os anúncios que são exibidos, por exemplo como quem está por trás deles e qual anúncio foi publicado.
Isso se torna uma informação importante para eles analisarem o que a concorrência faz e como as fazem. Tipos de anúncios, se foi em texto, vídeo ou imagem, se foi utilizado critérios na postagem desses anúncios etc.

## Dataset

Os dados foram extraídos do BigQuery da Google que é um serviço de armazenamento e análise de dados em grande escala oferecido pela plataforma Google Cloud. Ele foi projetado para processar grandes volumes de dados de forma rápida e eficiente, utilizando a infraestrutura de computação em nuvem do Google.

## Extração dos dados

A extração foi feita com apenas 1 query, essa escolha foi a melhor opção pois o BigQuery é um serviço pago e você pode pagar por demanda da banda que for consumindo. Com isso extrair tudo e depois preparar os dados diretamente no Power Query foi o ideal nesse contexto, caso contrário cada query geraria consumo da banda.

![img001](https://github.com/user-attachments/assets/751860a9-c25f-42cb-b801-969624d64a74)


Aqui vemos que a query irá processar 83GB de dados para nos dar o resultado final que irá ficar com um tamanho bem menor, pois foi pedido pela agência a filtragem de anunciantes do Brasil. Assim ficamos com a seguinte query.

```
SELECT *
FROM `bigquery-public-data.google_ads_transparency_center.creative_stats`
WHERE advertiser_location = 'BR'
```

## Schema

O BigQuery nos fornece algumas informações sobre o dataset e o schema é uma delas.

![img002](https://github.com/user-attachments/assets/e6c6fcfe-25e6-404d-89fd-fde5c648b20e)

## Visualização dos Anúncios

![img003](https://github.com/user-attachments/assets/ed465d85-6c19-421c-819b-64116742a617)

Na coluna [creative_page_url] é aonde fica a informação do link para a central de transparência de ads da Google para a pessoa visualizar qual propaganda foi publicada e assim olhar o conteúdo do anúncio, ao clicar em um link nós temos a seguinte tela.

![img004](https://github.com/user-attachments/assets/dd81587a-f45e-4462-a69a-bfceaae182c6)

Nesse caso do anúncio da Decolar, temos as informações que foi o anúncio foi mostrado no **Brasil**, a última vez publicado no dia **24/01/2025** no formato **Texto** e a anúncio em si que é mostrado ao usuário.

## Power Query

Essa etapa vamos limpar e corrigir, se necessário, algumas informações do dataset. As mudanças realizadas foram a correção do tipo de dado nas datas para *Data Type Date*, remoção de algumas colunas que não iremos utilizar e por fim a tradução de algumas colunas que estavam em Inglês e foi feito a tradução para o Português.
Um exemplo de coluna traduzida é a de qual categoria a propaganda foi selecionada, para traduzi-la criamos uma *Custom Column* com a seguinte fórmula na linguagem M:

```
= Table.AddColumn(#"Removed Duplicates", "topic_translated", each if [topic] = "Apparel" then "Vestuário" else if [topic] = "Hobbies, Games & Leisure" then "Hobbies, jogos e lazer" else if [topic] = "Business & Industrial" then "Negócios e Indústria" else if [topic] = "Autos & Vehicles" then "Automóveis e veículos" else if [topic] = "Food & Groceries" then "Alimentos e mercearia" else if [topic] = "Travel & Tourism" then "Viagem e Turismo" else if [topic] = "Sports & Fitness" then "Esportes e Fitness" else if [topic] = "Real Estate" then "Imóveis" else if [topic] = "Commercial" then "Comercial" else if [topic] = "Beauty & Personal Care" then "Beleza e cuidados pessoais" else if [topic] = "Family & Community" then "Família & Comunidade" else if [topic] = "News, Books & Publications" then "Notícias, livros e publicações" else if [topic] = "Food & Groceries" then "Alimentos e mercearia" else if [topic] = "Internet & Telecom" then "Internet e telecomunicações" else if [topic] = "Dining & Nightlife" then "Restaurantes e vida noturna" else if [topic] = "Arts & Entertainment" then "Artes e Entretenimento" else if [topic] = "Law & Government" then "Direito e Governo" else if [topic] = "Occasions & Gifts" then "Ocasiões e presentes" else if [topic] = "Health" then "Saúde" else if [topic] = "Mobile App Utilities" then "Utilitários de Aplicativo Móvel" else if [topic] = "Luggage & Bags" then "Bagagens & Bolsas" else if [topic] = "Electronics" then "Eletrônicos" else if [topic] = "Health & Beauty" then "Saúde e Beleza" else if [topic] = "Apparel & Accessories" then "Roupas e Acessórios" else if [topic] = "Books, Movies & Music" then "Livros, Filmes & Música" else if [topic] = "Furniture" then "Móveis" else if [topic] = "Toys & Games" then "Brinquedos & Jogos" else if [topic] = "Home Improvement" then "Melhorias domésticas" else if [topic] = "Baby & Kids" then "Bebês e Crianças" else if [topic] = "Automotive" then "Automóveis e veículos" else if [topic] = "Household Supplies" then "Suprimentos domésticos" else if [topic] = "Sporting Goods" then "Artigos esportivos" else if [topic] = "Pet Supplies" then "Suprimentos para animais domésticos" else if [topic] = "Religious & Ceremonial" then "Religioso & Cerimônias" else if [topic] = "Office Supplies" then "Suprimentos para escritórios" else if [topic] = "Animals & Pet Supplies" then "Suprimentos para animais domésticos" else if [topic] = "Office & School Supplies" then "Suprimentos para escritórios" else if [topic] = "Grocery" then "Mercearia" else if [topic] = "Vehicles & Parts" then "Automóveis e veículos" else if [topic] = "Media" then "Mídia" else if [topic] = "Musical Instruments" then "Instrumentos Musicais" else if [topic] = "Food, Beverages & Tabacco" then "Comida, Bebida & Tabacco" else if [topic] = "Baby & Toddler" then "Bebês e Crianças" else if [topic] = "Sports & Outdoors" then "Esportes ao ar livre" else if [topic] = "Arts & Crafts & Party Supplies" then "Arte, Artesanato & Suprimentos para Festas" else [topic])
```
## Exploração dos Dados

Vamos começar a explorar os dados e extrair algumas informações básicas. A Google fornece dados como, o nome jurídico de quem pagou pelo anúncio, o formato utilizado, a plataforma onde o anúncio foi publicado, a categoria a qual ele pertence, além do link do anúncio para podermos verificar como ele é apresentado.

As informações cobrem o período de 01/03/2023 até o dia em que o dataset foi coletado, em 22/01/2025. *(Obs: O dataset foi atualizado e está com datas até o dia 26/01/2025)*

A imagem a seguir mostra as plataformas nas quais os anúncios podem ser publicados.

![Screenshot_1](https://github.com/user-attachments/assets/068ea40c-2da0-4e8b-98c2-5a55569de3ff)

## Métricas gerais

Fizemos algumas medidas DAX para visualizarmos algumas métricas gerais. São números bastante expressivos, vemos que há mais de 4 milhões de anúncios nesse período e um total de 37 mil e 653 anunciantes. Lembrando que cada anúncio mesmo tendo o mesmo *[creative_id]* ele pode ser postado em diferentes plataformas como mencionado anteriormente. Isso quer dizer que podemos ter o mesmo conteúdo porém ele apareceu uma vez no google maps e outra vez no google search, mas é considerado dois anúncios e o google cobra pelo número total de aparições, além de serem postados na mesma plataforma mas em dias diferentes, isso tudo vai agregando a esse número total de publicações.

![img006](https://github.com/user-attachments/assets/14e29376-2672-45f5-90c6-9a86b1ff8924)

## Principais anunciantes

A imagem a seguir contém os 15 anunciantes que mais publicaram anuncios nas plataformas da Google. O grande vencedor é o Booking.com com mais de 100 mil anúncios, porém além de empresas grandes como a booking.com, magazine luiza, 123 viagens, são empresas especializadas em marketing digital, como o CityAds, que no caso seria um dos serviços que a M1 oferece, a parte de publicações e controle dessa parte para os clientes.

![img007](https://github.com/user-attachments/assets/40dd513d-4794-4fcd-8290-2e7156ccc458)

## Se aprofundando nas publicações

O anunciante tem a opção de escolher em qual categoria seu anúncio vai ser colocado, isso e outros filtros são possíveis para que cada vez mais o anunciante tenha a possibilidade de aumentar seu engajamento pois está escolhendo o público alvo correto ou que ele julga ser o mais correto.

Podemos ver que as categorias que mais publicam anúncios são de Viagem e Turismo, Negócios e Indústria, Vestuário e Artes e Entretenimento.

![img008](https://github.com/user-attachments/assets/1fdbdfbb-d2a5-45fa-8865-2a6fe0907c02)

Ao ser publicada, uma propaganda pode sofrer a influência de alguns critérios. Retirado do BigQuery da Google, as seguintes informações sobre essas categorias são:

- Informações Demográficas: Descreve se e como informações demográficas foram usadas para selecionar o público do anúncio
- Localização Demográfica: Descreve se e como informações de localização geográfica foram usadas para selecionar o público do anúncio
- Sinais Contextuais: Descreve se e como sinais contextuais foram utilizados para selecionar o público do anúncio
- Lista de Clientes: Descreve se e como listas de clientes foram usadas para selecionar o público do anúncio
- Tópicos de Interesse: Descreve se e como tópicos de interesse foram usados para selecionar o público do anúncio

E analisando alguns desses números vemos o contraste que existem entre as categorias.

![img009](https://github.com/user-attachments/assets/3d42389f-5745-44d1-b969-a6a5013354f9)

Enquanto mais de 77% da publicações conseguiram ter critérios aplicados na categoria de **Informações Demográficas**, 82% das publicações não conseguiram ter critérios de **Tópicos de Interesse** aplicados ao mostrar um anúncio aos usuários.

Outro fator de escolha em cada publicação é a escolha do formato em que a informação será transmitida pelo anunciante. O dataset nos mostra que essa escolha é feita através de 3 tipos de informação, a textual, por imagem e por fim vídeos.

![img010](https://github.com/user-attachments/assets/44192244-fe92-4800-8a6d-59ab3eb6cf4a)

Uma última informação sobre as publicações que gostaria de mostrar é a data na qual as propagandas foram mostradas pela última vez. 

![img011](https://github.com/user-attachments/assets/077dacbc-bb24-4259-a847-3b00f1e0cf90)

Para entendermos esse gráfico é importante ter em mente que muitos anúncios podem ter sido criados em meses anteriores mas ainda estarem ativos na plataforma e sendo republicados. Por isso nota-se um número bem maior no último mês da coleta dos dados, podemos considerar ele o mês vigente, por assim dizer. Assim concluir que em janeiro de 2025 temos mais de 1 milhão de anúncios ativos sendo mostrados nas diversas plataformas da Google, provenientes de anunciantes que estão cadastrados como país **Brasil** em sua localidade.

## Conclusão e Criação do Dashboard

Durante a análise dos dados e ao conversar com a M1, foi decidido que a ideia inicial de criar o dashboard apenas para filtragem e checagem de conteúdo publicitário de terceiros poderia ser expandida. Assim, o dashboard final incluirá, além da análise e filtragem de anunciantes concorrentes, outra página com informações relevantes extraídas durante a exploração dos dados.

Por exemplo, ao identificar os principais temas dos anúncios, a empresa pode compreender quais mercados estão em alta para prospectar novos clientes. Como vimos anteriormente, a categoria Viagem e Turismo possui mais de meio milhão de anúncios. A agência poderia focar na prospecção de agências de viagem, oferecendo seus serviços e demonstrando a competitividade do cenário publicitário dessa categoria. O contrário também é valido, explorar mercados que não estão investindo tanto, e demonstrar a eles o potêncial que podem atingir contratando serviços especializados de marketing.

O fato de o texto ser o formato mais popular entre as propagandas também mostra que habilidades em trabalhar com tipografia, cores, estrutura, hierarquia de texto, entre outras, são habilidades que, por mais antigas que pareçam, por ora têm um apelo e um espaço sólidos na era digital.

Outra descoberta interessante foi sobre os critérios utilizados nas publicações das propagandas. Saber que mais de 80% dos anúncios não foram segmentados por Tópico de Interesse evidencia o motivo pelo qual, muitas vezes, os usuários recebem propagandas irrelevantes para suas necessidades no momento. Embora o Google busque obter informações precisas sobre os interesses de seus usuários, nem sempre isso é possível. Além disso, é comum que os anunciantes deixem de configurar critérios importantes, optando apenas por segmentações mais gerais, como região e faixa etária, sem explorar outras opções valiosas de segmentação.

Com todas essas informações em mãos, avançamos para a etapa final do projeto: a criação do dashboard interativo que será entregue à M1. Uma versão final será disponibilizada com o logotipo da M1 substituindo a marca original. O link para o dashboard será incluído no início desta documentação.

## Notas e Advertências

Um esclarecimento a respeito dos critérios que podem ser escolhidos para atingir o público-alvo é o fato de que o Google não fornece quais opções específicas foram utilizadas, apenas as 4 categorias e suas respectivas explicações de acordo com a plataforma:

- Critério Utilizado: Critérios desta categoria foram incluídos no público do anúncio
- Critério Utilizado e Excluído: Alguns critérios desta categoria foram incluídos e outros foram excluídos do público do anúncio
- Critério Não utilizado: Critérios dessas categorias não foram usados para a seleção do público
- Critério Excluído: Critérios desta categoria foram excluídos no público do anúncio

As informações, como nome jurídico e quaisquer outros dados pessoais, estão disponíveis ao público em geral através do serviço BigQuery da Google. Nenhuma informação contida nos dados utilizados tanto no dashboard quanto nesta documentação foi retirada de outras fontes.

Como uma última observação, a página 1, denominada Visão Geral, foi adicionada durante o projeto com o intuito de ser utilizada pela empresa na prospecção de clientes. Essa página contém informações gerais apresentadas ao longo desta documentação, que servirão como base para demonstrar aos clientes benefícios e maneiras de anunciar com a Google.

## Demo Dashboard

E assim finalizamos essa documentação com uma pequena demonstração e exemplos de aplicações do projeto final. Na primeira página podemos filtrar os conteúdos para vermos por exemplo, clicando em Imagem, quais assuntos utilizam mais esse formato para fazer suas propagandas? Na imagem vemos que a categoria Vestuário utiliza mais Imagens, Viagem e Turismo explora muito o formato Texto e assim por diante.

![sample001](https://github.com/user-attachments/assets/024c3e07-d52e-44d0-8377-bcaeb336e2ab)

No exemplo a seguir, selecionamos as categorias primeiro para filtrar as outras informações, então podemos ver que na categoria Finanças no mês de Janeiro de 2025 foram feitas mais de 54 mil publicações, e um total de 1302 anunciantes diferentes. Já a Categoria Vestuário tem 2502 anunciantes e houveram mais de 79 mil publicações.

![sample002](https://github.com/user-attachments/assets/08c087e2-e9dc-4fa2-a761-70444dd709bc)

Passando para a página 2 no qual sua função é filtrar os anúncios baseado em interesses prévios ou não, e verificar as propagandas criadas e utilizadas pelas outras pessoas ou empresas.

Vamos imaginar que uma empresa de cosméticos queira anunciar com a agencia M1 e eles querem anunciar imagens no Youtube. A M1 pode utilizar o deashboard para analisar as publicações de concorrentes e de pessoas da área, como no exemplo a seguir:

![exemplo2](https://github.com/leandrobvs/SQL-PowerBI-Excel/blob/main/powerbi_m1_marketing/exemplo2.gif)

Algo interessante é o fato do link te leva para o site da Google com isso temos informações atualizadas em tempo real, por mais que o dataset tem atualizações até o dia 26 de janeiro, vimos que ao navegar entre as publicações podemos encontrar propagandas que foram utilizadas no dia em que a pessoa estiver utilizando o dashboard.

Outra função primordial para a M1 é o fato de pesquisar por nome do anunciante. Vamos imaginar a necessidade de filtrar utilizando palavras chaves como **ACADEMIA** ou **FITNESS**.

![sample004](https://github.com/user-attachments/assets/b1cf9b15-8899-4a61-a93a-2d945acc7b40)





















