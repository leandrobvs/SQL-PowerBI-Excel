# Introdução ao problema de Negócio.

ShopEasy, um negócio de varejo online, está enfrentando uma redução no engajamento dos clientes e nas taxas de conversão, apesar de ter lançado várias novas campanhas de marketing online. Eles estão pedindo sua ajuda para realizar uma análise detalhada e identificar áreas de melhoria em suas estratégias de marketing.

Vamos observar as mensagens que a empresa nos encaminhou e sublinhar as partes mais importantes, isso vai nos ajudar em todo o processo, entender o problema de negócio antes de entrar direto na parte técnica.

[Link -> Mensagens da Empresa](/powerbi_analise_marketing/Emails.md)

Pontos principais:

- Redução no Engajamento dos Clientes: O número de interações e engajamento dos clientes com o site e o conteúdo de marketing diminuiu.

- Diminuição das Taxas de Conversão: Menos visitantes do site estão se tornando clientes pagantes.

- Altos Custos de Marketing: Investimentos significativos em campanhas de marketing não estão trazendo os retornos esperados.

- Necessidade de Análise de Feedback dos Clientes: Compreender as opiniões dos clientes sobre produtos e serviços é crucial para melhorar o engajamento e as conversões.

## Objetivos

Vamos marcar alguns objetivos que gostariamos de entregar/mostrar a empresa que pediu nossos seviços, mais uma vez essa etapa de pensar no problema e objetivos vai ser fundamental no decorrer de todo o processo.

**Aumentar as Taxas de Conversão:**

- Objetivo: Identificar os fatores que impactam a taxa de conversão e fornecer recomendações para melhorá-la.
- Insight: Destacar as etapas-chave onde os visitantes abandonam e sugerir melhorias para otimizar o funil de conversão.

**Aumentar o Engajamento dos Clientes:**

- Objetivo: Determinar quais tipos de conteúdo geram maior engajamento.
- Insight: Analisar os níveis de interação com diferentes tipos de conteúdo de marketing para orientar melhores estratégias de conteúdo.

**Melhorar as Avaliações de Feedback dos Clientes:**

- Objetivo: Compreender os temas comuns nas avaliações dos clientes e fornecer insights acionáveis.
- Insight: Identificar feedbacks positivos e negativos recorrentes para orientar melhorias em produtos e serviços.

# Análise

Com essas informações vamos começar a entender os dados que temos em mãos. Inicialmente no SQL e depois exportar os dados para o Power BI, então dependendo se for interessante já exportamos com algumas modificações.

### :mag_right: [SQL análise](./powerbi_analise_marketing/sql.md)

E como parte final do trabalho vou deixar o link para o dashboard criado no Power BI. Qualquer informações pertinentes durante a parte do Power BI vou ir acrescentando no corpo desse README.md

## :mag_right: [Power BI Dashboard](https://app.powerbi.com/view?r=eyJrIjoiZmEzMGQzNGUtNWU4ZC00MjNjLWFlYzUtYjgxMzA0Zjc3OGQ5IiwidCI6ImU3ODllZDJmLWQ3YTUtNDJlMy1iODllLWJlOGE4YjJjZTY5YSJ9)

### Respondendo as Perguntas

Acredito que, com os dados fornecidos, podemos ajudar a responder as perguntas encaminhadas por e-mail. O dashboard criado destaca algumas observações interessantes sobre o engajamento, sendo elas:

- Os cinco primeiros meses apresentam altas taxas de visualizações, mas, a partir de junho até dezembro, esse número cai drasticamente. Sugerimos que a equipe de marketing analise se há mudanças significativas nas campanhas, seja na execução ou na abordagem, em comparação com o início do ano.
- Outro ponto relevante é a revisão da estratégia de manter o mesmo número de campanhas em newsletters, considerando que os melhores resultados estão sendo alcançados por blogs e mídias sociais.

Na questão das conversões baixas, foi identificado que muitos clientes chegam às etapas finais para adquirir o produto, mas desistem na área de checkout. Entre essas desistências, a grande maioria tinha produtos na faixa de preço _Alta_ em seus carrinhos.

Outro ponto identificado foi que as avaliações apresentam uma média de 3,69. Acredito que esse valor está abaixo do esperado pela empresa e pode ser um dos motivos pelos quais os clientes não demonstram interesse em adquirir os produtos, devido a dúvidas sobre a qualidade e a experiência de compra com a EasyShop.

Respondendo ao questionamento da Gerência de Experiência do Cliente sobre a análise detalhada dos feedbacks, ressaltamos que a principal reclamação recebida está relacionada ao "Não vale o dinheiro", o que reforça o ponto anteriormente mencionado sobre as desistências no checkout. Isso sugere que os produtos nessa faixa de preço podem não estar atendendo às expectativas do público-alvo atraído pelas campanhas.

Além disso, com o dashboard disponível, a equipe pode verificar, produto a produto, quantas avaliações cada um recebeu, sua média de avaliação e a distribuição das avaliações por nota.
