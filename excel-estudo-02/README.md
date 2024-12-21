Cenário

![image](https://github.com/user-attachments/assets/5606bd8c-f7b7-429e-a3a9-57ed10c970f7)

O Café Diário é uma torrefação de cafés especiais que vende grãos de café para lojas de varejo em todo o Brasil. A empresa sabe que a demanda por seu café varia significativamente com o preço. No último ano, a demanda em cada nível de preço foi registrada na tabela abaixo.

![image](https://github.com/user-attachments/assets/9f7f2068-8870-433f-86a7-c2bc33509772)

A empresa deseja estimar a relação entre demanda e preço com base nesses dados e utilizar o modelo para responder às seguintes perguntas:

 - Supondo que o custo de produção e embalagem dos grãos de café seja de R$ 50 por quilograma, e o preço deve ser um múltiplo de R$ 5, qual preço a empresa deve cobrar para maximizar seu lucro?
 - Este modelo é uma representação confiável da demanda no mundo real?

### Escolhendo o modelo a ser utilizado:

Inicialmente, gostaria de entender e mostrar como podemos trabalhar com esses dados. Para isso, podemos gerar um gráfico rápido e visualizar a relação entre preço e demanda.

![excel-sample001](https://github.com/user-attachments/assets/55a22a8b-0c0a-4ac5-99fb-a25f637102d5)

Como esperado e nada fora do comum, conseguimos observar que, conforme o preço sobe, a demanda cai. Então, vamos tentar responder à primeira pergunta que o setor de vendas gostaria de analisar: qual é o preço que maximizaria os lucros?

Temos algumas opções aqui, e acredito que a mais comum seria a utilização de uma regressão linear. Mas será que ela é a opção com maior probabilidade de acerto? Para isso, vamos compreendê-la e compará-la com outras linhas de tendência.

![excel-sample002](https://github.com/user-attachments/assets/b4055411-8e0e-4e7f-86c9-0a7206f951ad)

A regressão linear é um método estatístico usado para modelar a relação entre uma variável dependente (y) e uma ou mais variáveis independentes (x). O objetivo principal é encontrar uma linha reta que melhor se ajuste aos dados.

Por ser uma linha reta, pode não ser a melhor opção para o cenário que temos, já que os preços não seguem uma constante. Então, vamos compará-la às tendências exponencial e logarítmica. O Excel permite exibir a equação usada para cada tendência escolhida, e, nos próximos passos, vamos aplicar essas fórmulas.

![image](https://github.com/user-attachments/assets/530db76e-c215-4346-a167-d2a1b917126a)

Com os valores extraídos e as equações montadas, começamos a relacionar cada modelo escolhido.

![image](https://github.com/user-attachments/assets/62289b1f-0ef7-4b85-8956-c3a870e29b68)

Observamos que, para este exemplo, a regressão linear não apresentou um desempenho ruim, mas a logarítmica resultou em um menor percentual de erro. Já a tendência de potência pode ser descartada completamente neste caso. Apesar de sua curva maior sugerir que acompanharia melhor a variação, isso não ocorreu para esses dados.

Após elaborar nossa defesa sobre qual modelo utilizar, damos continuidade à análise para responder: qual preço a empresa deve cobrar para maximizar seu lucro?

![excel-sample003](https://github.com/user-attachments/assets/6adedd54-5187-4d9a-836a-16ea40b5777d)


Com isso, encontramos o valor mais lucrativo que podemos passar ao gerente para definir quais estratégias tomar.

![image](https://github.com/user-attachments/assets/c7411867-2d26-426e-88b5-544317cd391e)

Valor de venda otimizado: **115 reais por Kg de café.**

![image](https://github.com/user-attachments/assets/1e3f158e-240b-40ee-a795-2a53f316f20a)

Adicionalmente, um gráfico foi incluído para demonstrar que não é interessante aumentar muito o preço, pois a demanda diminui e os lucros começam a cair, mesmo com produtos sendo vendidos a valores mais altos.

### Este modelo é uma representação confiável da demanda no mundo real?

Por fim, acredito que sim. Essa representação reflete um cenário muito comum no dia a dia. Esses tipos de números e variáveis estão dentro da realidade de serem obtidos. São, inclusive, dados básicos para qualquer empresa. À medida que o porte da empresa cresce, a complexidade dessas análises também aumenta, o que permite o uso de modelos mais detalhados e redução das margens de erro.










