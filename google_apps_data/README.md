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

![image](https://github.com/user-attachments/assets/feee5c9e-5971-4e5a-bc17-810f3e8f5b80)





