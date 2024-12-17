![brazil-e-commerce](https://github.com/user-attachments/assets/d7e4ff27-c95f-4add-9be1-44a19ac23fac)

# Dataset sobre o e-commerce brasileiro
### Dados provenientes da Olist. A Olist é uma plataforma de e-commerce que ajuda lojistas a venderem em marketplaces, como Americanas, Mercado Livre, Submarino, Casas Bahia, Pontofrio, entre outros.
### [Olist](https://olist.com/)


Resolvi nesse estudo faze-lo como uma espécie de jornal, vou escrevendo um passo a passo o que vem em mente para primeiro conhecer e depois analisar alguns desses dados contidos nesse dataset.

As tabelas existentes no servidor SQL são as seguintes:

![image](https://github.com/user-attachments/assets/c475ffc4-bdf1-4022-bade-66df5d4a76df)

Inicialmente eu pensei que extrair alguns números gerais para entender o cenário macro desses dados e entender com o que vou lidar.

## Números Gerais

```
SELECT 
    COUNT(DISTINCT customer_unique_id) AS consumidores_unicos,
    COUNT(customer_id) AS total_consumidores
FROM olist_customers;
```

![image](https://github.com/user-attachments/assets/1fd3d1c4-8d59-4950-9757-2176b489083d)

```
SELECT  
    EXTRACT(YEAR FROM order_purchase_timestamp) AS ano, 
    COUNT(*) AS total_ordens_por_ano,
    SUM(COUNT(*)) OVER () AS total_ordens
FROM olist_orders
GROUP BY ano
ORDER BY ano DESC;
```

![image](https://github.com/user-attachments/assets/c17d740a-fb71-4d88-b6e8-e6c721bd1e9e)


```
SELECT COUNT(DISTINCT product_id) AS produtos_unicos
FROM olist_order_items;
```

![image](https://github.com/user-attachments/assets/fcf325c2-12d1-41a5-ba97-b6916c9bb282)

```
SELECT 
	product_category_name AS categorias_exemplos,
	SUM(COUNT(DISTINCT product_category_name)) OVER() AS num_total_categorias
FROM olist_products
GROUP BY categorias_exemplos
LIMIT 10;
```

![image](https://github.com/user-attachments/assets/d14088d8-9d07-467b-bf1b-fe2fcfd19051)


```
SELECT COUNT(seller_id) AS total_vendedores
FROM olist_sellers
```

![image](https://github.com/user-attachments/assets/e68239ea-22d7-4f5a-8357-a6077f1a6705)

Com essa extração inicial podemos fazer um resumo breve do que temos por enquanto que consiste em:
- Os dados são dos anos 2016, 2017 e 2018 mas já com uma grande observação que os dados de 2016 estão muito diferentes dos últimos dois anos. Acredito que a diferença seja tão significativa que podemos tratar 2016 como um valor atípico (outlier). Então para futuras analises é como vamos observa-lo.
- Temos 96 mil consumidores únicos
- 32 mil produtos únicos separados em 73 categorias
- 3095 vendedores
- Total de 99 mil ordens

O que eu gostaria de descobrir agora é: Quais categorias vendem mais dentro dessas 99 mil ordens

```
WITH ranked_categories AS (
    SELECT 
        product_category_name AS categoria,
        COUNT(order_id) AS total,
        ROW_NUMBER() OVER(ORDER BY COUNT(order_id) DESC) AS ranking
    FROM olist_products AS p
    LEFT JOIN olist_order_items AS o
    ON p.product_id = o.product_id
    GROUP BY product_category_name
    ORDER BY total DESC
    LIMIT 10
)
SELECT 
    categoria,
    total,
    SUM(CASE WHEN ranking <= 10 THEN total ELSE 0 END) OVER () AS soma_top5_categorias,
	(SELECT COUNT(*) FROM olist_orders) AS total_orders
FROM ranked_categories
ORDER BY ranking;
```

![image](https://github.com/user-attachments/assets/313134b7-4c68-4340-8cd9-8ad17cdf6afe)

Das 73 categorias disponíveis, as 10 melhores com maior número de pedidos são as mencionadas na imagem acima. Na mesma query aproveitei e extrai duas informações adicionais, a soma das 10 melhores categorias (71669) e em contraste o total de ordens (99441). Interessante notar que as 10 categorias que vendem mais produtos são responsáveis por 72% das vendas, como já mencionado, temos um total de 73 categorias, então ficamos com as 63 categorias restantes responsáveis pelos outros 28% das vendas.

## Qualidade da logística

As próximas perguntas que gostaria de responder são sobre a logistica desses pedidos. Extrai alguns dados com as seguintes consultas:

```
SELECT
	ROUND(AVG(order_delivered_customer_date - order_purchase_timestamp),2) AS media_entrega,
	MIN(order_delivered_customer_date - order_purchase_timestamp),
	MAX(order_delivered_customer_date - order_purchase_timestamp)
FROM olist_orders
WHERE order_delivered_customer_date IS NOT NULL
LIMIT 10;
```

![image](https://github.com/user-attachments/assets/323ee2a3-3f37-45bb-9c9e-b2149d6d9908)

Em média as encomendas demoram cerca de 12 dias para chegarem ao consumidor, e a entrega com o menor tempo foi de 0 dias, ou seja a compra chegou no mesmo dia que o consumidor a efetuou, e a que mais demorou foram 210 dias, o que me leva a acreditar que seja uma exceção devido a algum problema no pedido ou com a transportadora, mas para entender se esses casos são exceções resolvi extrair mais dados sobre isso.

```
SELECT
	(order_delivered_customer_date - order_purchase_timestamp) AS dias_entregue,
	COUNT(*) AS total
FROM olist_orders
WHERE order_delivered_customer_date IS NOT NULL
GROUP BY dias_entregue
ORDER BY dias_entregue DESC;
```

![logistica001](https://github.com/user-attachments/assets/38a14551-a3ef-43d5-9936-c5a9be93276d)

O maior volume de entrega fica entre 1 e 20 dias, com os picos entre 5 a 10 dias. Podemos ver que realmente os pedidos que excedem 50 dias são casos pontuais mas que acontecem mais de uma vez, o que cria um alerta sobre a qualidade da logistica ou eventuais problemas de estoque ou algo relacionado com as empresas.

## Entendendo nosso público

Com os dados que nós temos, podemos visualizar algumas informações para entender melhor nosso consumidor e assim tomar decisões para melhor atende-los e pensar em planejamentos para aumentar as vendas, explorar pontos fortes e melhorar os pontos fracos.

```
SELECT customer_state, COUNT(*) AS total
FROM olist_customers
GROUP BY customer_state
ORDER BY total DESC
LIMIT 5;
```

![image](https://github.com/user-attachments/assets/37fb5887-0c80-4c81-96f8-5915315d85b7)

Vemos que os 5 estados que mais consomem os produtos são: São Paulo, Rio de Janeiro, Minas Gerais, Rio Grande do Sul e Paraná.

E essas pessoas estão preferindo pagar suas compras como?

```
SELECT payment_type AS metodo_de_pagamento,
	COUNT(*) AS TOTAL
FROM olist_order_payments
GROUP BY payment_type
ORDER BY total DESC;
```

![image](https://github.com/user-attachments/assets/6aa35397-ccc6-4c9a-96b0-70ebb148d75a)

A maioria esmagadora escolhe a opção por cartão de crédito, seguida por boleto. Sabemos que muitas lojas tentam fazer descontos para as pessoas que pagam à vista, porém mesmo assim não consegue chegar perto dos números do cartão de crédito.

```
SELECT 
	payment_type,
	payment_installments AS parcelado_por,
	COUNT(payment_installments) AS total
FROM olist_order_payments
WHERE payment_type = 'credit_card'
GROUP BY payment_type, parcelado_por
ORDER BY total DESC
LIMIT 5;
```

![image](https://github.com/user-attachments/assets/305726b1-d09c-4a7a-b793-bf57e9768926)


```
SELECT 
	ROUND(AVG(payment_value),2) AS ticket_medio
FROM olist_order_payments;
```

![image](https://github.com/user-attachments/assets/0f7fb48b-032f-4b71-9e70-d93c653a111d)

Sendo que apesar da escolha ser por crédito, a grande maioria das compras são feitas em parcela única, com a densidade sendo muito alta em até 3 parcelas. Talvez o número de parcelas sejam baixos pelo fato do preço médio das ordens girar em torno de 154 reais.

E por fim vamos ver as avaliações dos consumidores para entendermos o nível de satisfação com as lojas e produtos.

```
SELECT review_score,
	COUNT(*) AS total
FROM olist_order_reviews
GROUP BY review_score
ORDER BY total DESC;
```

![image](https://github.com/user-attachments/assets/8a690a7d-75be-4482-9c44-d10a6e53580f)

O grande número de avaliações ficam na casa das 5 e 4 estrelas, de modo geral o consumidor tem uma visão positiva das suas compras, porém a terceira nota mais recebida é de 1 estrela. Acredito que isso liga o alerta para que há margem para melhoria, pois mais de 10 mil avaliações não são de ser ignoradas quando praticamente 10% das suas vendas receberam a menor nota possível.

Como dito no inicio, quis fazer algo diferente, mais direto e usando praticamente só o SQL para enteder alguns números e criar alguns insights rápidos.












