# Analisando alguns números sobre mais de 2 milhões de APPS da Google Store
### Dados coletados por Gautham Prakash. Fonte: [Kaggle](https://www.kaggle.com/datasets/gauthamp10/google-playstore-apps/data)

> [!NOTE]
> Um breve esclarecimento dos métodos e passos utilizados nesta análise. O dataset em questão foi baixado diretamente da fonte e tratado por mim até a inserção no RDBMS, utilizando PostgreSQL e pgAdmin 4 para enviar as consultas ao banco de dados. O seguinte schema foi criado:

![image](https://github.com/user-attachments/assets/8395cb4d-8cdb-4304-beb9-3069f0175a21)

### As perguntas a serem investigadas e respondidas são as seguintes:

**Análise sobre a popularidade dos aplicativos**

- Qual é a categoria mais popular?
- Quais são os aplicativos mais baixados por categoria?
- Como varia o número de downloads entre aplicativos gratuitos e pagos?
- Dentre os aplicativos gratuitos, quantos oferecem compras dentro do app?

**Insights sobre Avaliações de Usuários**

- Qual é a distribuição das avaliações de usuários por categoria de aplicativo?
- Quais aplicativos têm as maiores e menores avaliações em cada categoria?
- Qual porcentagem dos aplicativos possui uma avaliação de usuário acima de 4,5?

**Melhores Aplicativos**

 - Quais são os 10 aplicativos com mais downloads e as avaliações mais altas?
 - Quais aplicativos gratuitos possuem as maiores avaliações de usuários?
 - Entre os aplicativos pagos, quais geram mais downloads?

**Potencial de Receita**

- Quais categorias possuem o maior potencial de receita com base nos números de downloads e preço?
- Qual é a receita total estimada para os 10 aplicativos pagos mais bem classificados?

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

![image](https://github.com/user-attachments/assets/91616e1e-8b03-41b1-a22f-870c913c3469)

Algumas conclusões que podemos tirar com base nos dados.

As empresas que lançam aplicativos grátis preferem colocar anúncios dentro de seus aplicativos do que oferecer conteúdo pago dentro deles. 1.15 milhões de aplicativos tem propagandas, enquanto apenas 190 mil oferecem conteúdo pago. Porém com isso surge outra questão, se todos esses aplicativo com propagandas oferecem por meio de pagamento a retirada delas, tornando esse metodo quase que uma compra dentro do app de qualquer maneira, apenas outra estratégia. Infelizmente com os dados que temos não podemos conferir essa opção de retirar os ads com pagamentos.







