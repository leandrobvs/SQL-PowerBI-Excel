![brazil-e-commerce](https://github.com/user-attachments/assets/d7e4ff27-c95f-4add-9be1-44a19ac23fac)

# Dataset sobre o e-commerce brasileiro
### Dados provenientes da Olist. A Olist é uma plataforma de e-commerce que ajuda lojistas a venderem em marketplaces, como Americanas, Mercado Livre, Submarino, Casas Bahia, Pontofrio, entre outros.
### [Olist](https://olist.com/)


Resolvi nesse estudo faze-lo como uma espécie de jornal, vou escrevendo um passo a passo o que vem em mente para primeiro conhecer e depois analisar alguns desses dados contidos nesse dataset.

As tabelas existentes no servidor SQL são as seguintes:

![image](https://github.com/user-attachments/assets/c475ffc4-bdf1-4022-bade-66df5d4a76df)

Inicialmente eu pensei que extrair alguns números gerais para entender o cenário macro desses dados e entender com o que vou lidar.

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
