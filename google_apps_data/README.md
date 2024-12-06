# Analisando alguns números sobre mais de 2 milhões de APPS da Google Store
### Dados coletados por Gautham Prakash. Fonte: [Kaggle](https://www.kaggle.com/datasets/gauthamp10/google-playstore-apps/data)
### Estudo para praticar :)

> [!NOTE]
> Um breve esclarecimento dos métodos e passos utilizados nesta análise. O dataset em questão foi baixado diretamente da fonte e tratado por mim até a inserção no RDBMS, utilizando PostgreSQL e pgAdmin 4 para enviar as consultas ao banco de dados. Visualizações criadas no Power BI. O seguinte schema foi criado:

![image](https://github.com/user-attachments/assets/8395cb4d-8cdb-4304-beb9-3069f0175a21)

### As perguntas a serem investigadas e respondidas são as seguintes:

**Análise sobre a popularidade dos aplicativos**

- Qual é a categoria mais popular?
- Quais são os aplicativos mais baixados por categoria?
- Como varia o número de downloads entre aplicativos gratuitos e pagos?
- Dentre os aplicativos gratuitos, quantos oferecem compras dentro do app?

**Insights sobre Avaliações de Usuários**

- Quais são as categorias que recebem a maior e menor média de avaliações dos usuários?
- Qual porcentagem dos aplicativos possui uma avaliação de usuário acima de 4,5?

**Potencial de Receita**

- Quais categorias possuem o maior potencial de receita com base nos números de downloads e preço?

## Respostas

### :mag: Qual é a categoria mais popular?

Para saber qual a categoria mais popular, foi somado o número total de instalações de todas as categorias e resolvemos mostrar em um rank as 15 categorias com maior número de downloads. A seguinte consulta foi realizada:

```
SELECT category, SUM(maximum_installs) as highest_total 
FROM google_apps
WHERE minimum_installs IS NOT NULL
GROUP BY category
ORDER BY highest_total DESC
LIMIT 15;
```

E criamos a visualização no PowerBI, com ela fica bem nítido ver que a categoria mais popular com mais de 120 bilhões de downloads é a de Ferramentas.

![image](https://github.com/user-attachments/assets/079949f8-986e-47fc-a7d8-ff3987f06426)

### :mag: Quais são os aplicativos mais baixados por categoria?

Após vermos quais categorias são mais populares, vamos descobrir quais aplicativos são os mais populares por categoria. Para isso a seguinte consulta foi lançada:

```
SELECT g1.app_name, g1.category, g1.maximum_installs AS total_installs
FROM google_apps AS g1
	INNER JOIN
	(SELECT category, MAX(maximum_installs) AS max_install
	FROM google_apps
	GROUP BY category) AS g2
	ON g1.category = g2.category AND g1.maximum_installs = g2.max_install	
ORDER BY total_installs DESC
LIMIT 15;
```

Como se era esperado por se tratar da loja de aplicativos da Google, os aplicativos mais baixados são da própria empresa, com exceção do Facebook na categoria Social.

![image](https://github.com/user-attachments/assets/903a5739-e385-4f3e-97b7-6a598a091744)

### :mag: Como varia o número de downloads entre aplicativos gratuitos e pagos?

Uma consulta relativamente simples no SQL porém revelando uma diferença gigantesca entre os downloads entre aplicativos gratuitos e pagos.

```
SELECT free AS gratuito_ou_pago, SUM(maximum_installs)
FROM google_apps
GROUP BY gratuito_ou_pago
```

![image](https://github.com/user-attachments/assets/c4f00548-7015-436d-994e-e5c46c026060)

Podemos concluir superficialmente que uma escolha interessante para uma empresa que desenvolve aplicativos é buscar o modelo de preço gratuito com compras dentro do aplicativo. Mas para termos mais certeza disso, a nossa próxima pergunta vai se aprofundar nessa informação.

### :mag: Dentre os aplicativos gratuitos, quantos oferecem compras dentro do app?

Para responder a próxima pergunta foi efetuado a separação dos aplicativos que tem e não tem propaganda dentro deles, e os que oferecem compras dentro do aplicativo como, planos premium, desativar conteúdo específico, remover propagandas de dentro do app entre outros. Para extraiar essa informação a consulta a seguir foi utilizada:

```
SELECT free AS gratuito,
		SUM(CASE WHEN ad_supported = TRUE THEN 1 ELSE 0 END) AS tem_ads,
		SUM(CASE WHEN ad_supported = FALSE THEN 1 ELSE 0 END) AS n_tem_ads,
		SUM(CASE WHEN in_app_purchases = TRUE THEN 1 ELSE 0 END) AS tem_compras_no_app,
		SUM(CASE WHEN in_app_purchases = FALSE THEN 1 ELSE 0 END) AS n_tem_compras_no_app,
		COUNT(free) AS total_apps_gratuitos
FROM google_apps
WHERE free = TRUE
GROUP BY gratuito;
```

![image](https://github.com/user-attachments/assets/d0f303b1-6415-4308-9a4e-ddf5f6ae33b2)


Algumas conclusões que podemos tirar com base nos dados.

As empresas que lançam aplicativos grátis preferem colocar anúncios dentro de seus aplicativos do que oferecer conteúdo pago dentro deles. 1.15 milhões de aplicativos tem propagandas, enquanto apenas 190 mil oferecem conteúdo pago. Porém com isso surge outra questão, se todos esses aplicativo com propagandas oferecem por meio de pagamento a retirada delas, tornando esse metodo quase que uma compra dentro do app de qualquer maneira, apenas outra estratégia. Infelizmente com os dados que temos não podemos conferir essa opção de retirar os ads com pagamentos.

### :mag: Quais são as categorias que recebem a maior e menor média de avaliações dos usuários?

Entrando em um assunto voltado para os insights que os usuários podem nos dizer, vamos mostrar dois ranks, um com as categorias que recebem as melhores avaliações e outro rank com as piores. Para isso fizemos duas consultas em SQL, sendo elas:

```
SELECT category, ROUND(AVG(rating),2) as avg_rating
FROM google_apps
WHERE rating > 0
GROUP BY category
ORDER BY avg_rating DESC
LIMIT 5;
```

&

```
SELECT category, ROUND(AVG(rating),2) as avg_rating
FROM google_apps
WHERE rating > 0
GROUP BY category
ORDER BY avg_rating ASC
LIMIT 5;
```

![image](https://github.com/user-attachments/assets/1ff138cf-5532-48bc-a30a-872473a80534)

![image](https://github.com/user-attachments/assets/6e60a842-c3e5-4946-a450-6f7a3b9aecf6)


Interessante entender que mesmo as piores médias que ficam entre 3.89 e 3.8 não estão tão distantes das melhores que batem 4.29 e 4.25. Mas diria muito de um aplicativo que tem nota abaixo das piores médias, pois nos mostra que as pessoas avaliam notas baixas quando realmente algum app está muito ruim ou algo incomodou elas.

### :mag: Qual porcentagem dos aplicativos possui uma avaliação de usuário acima de 4.5?

Para conseguirmos obter os números de quantos aplicativos estão acima da nota de 4.5 a seguinte consulta foi efetuada:

```
SELECT total_above,
	ROUND((total_above * 100.0) / total_apps) AS porcentage
FROM
	(SELECT 
	SUM(CASE WHEN rating > 4.5 THEN 1 ELSE 0 END) AS total_above	
	FROM google_apps) AS sub_total_above,
	(SELECT COUNT(*) AS total_apps
	FROM google_apps) AS sub_total_apps;
```
Com isso podemos notar dentre os mais de 2 milhões de aplicativos disponíveis aos usuários, um total de 346 mil apps ficam com avaliações muito positivas o que representa 15% do total de apps na Google Store.

![image](https://github.com/user-attachments/assets/b5b2690c-824a-4911-a65a-1c66d854ee73)

### :mag:  Quais categorias possuem o maior potencial de receita com base nos números de downloads e preço?

Para identificarmos a receita total, que nossos dados podem nos oferecer para cada categoria, extraimos do database as informações de preço médio de cada categoria e o total de instalações. Com isso podemos observar a receita média que cada categoria já proporcionou.

```
SELECT category, SUM(maximum_installs) AS installs, ROUND(AVG(price),2) as avg_price
FROM google_apps
WHERE price > 0
GROUP BY category
ORDER BY installs DESC
```

![image](https://github.com/user-attachments/assets/5fbc7e8e-c757-448c-98b4-daf0d0ad9a4b)

Notamos que entre as 10 categorias com maior potencial de receita, 8 são categorias relacionadas a jogos, sendo elas (Arcade, Ação, RPG, Quebra-cabeça, Aventura, Simulação, Educação e Estratégia), e com uma boa margem a frente de todas os jogos Arcades faturaram mais de 500 milhões de dolares, quase 200 milhões a mais que a segunda colocação (jogos de ação).

















