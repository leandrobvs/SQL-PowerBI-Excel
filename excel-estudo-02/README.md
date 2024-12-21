Cenário

![image](https://github.com/user-attachments/assets/5606bd8c-f7b7-429e-a3a9-57ed10c970f7)

O Café Diário é uma torrefação de cafés especiais que vende grãos de café para lojas de varejo em todo o Brasil. A empresa sabe que a demanda por seu café varia significativamente com o preço. 
No último ano, a demanda em cada nível de preço foi registrada na tabela abaixo.

![image](https://github.com/user-attachments/assets/9f7f2068-8870-433f-86a7-c2bc33509772)

A empresa deseja estimar a relação entre demanda e preço com base nesses dados e utilizar o modelo para responder às seguintes perguntas:

 - Supondo que o custo de produção e embalagem dos grãos de café seja de R$ 50 por quilograma, e o preço deve ser um múltiplo de R$ 5, qual preço a empresa deve cobrar para maximizar seu lucro?
 - Este modelo é uma representação confiável da demanda no mundo real?

### Escolhendo o modelo a ser utilizado:

Inicialmente gostaria de entender e mostrar como podemos trabalhar em cima desses dados. Para isso podemos gerar um gráfico rápido e visualizar a relação de preço vs demanda.

![excel-sample001](https://github.com/user-attachments/assets/55a22a8b-0c0a-4ac5-99fb-a25f637102d5)

Como o esperado e nada fora do comum, conseguimos ver que conforme o preço sobe a demanda cai. Então vamos tentar responder a primeira pergunta que o setor de vendas gostaria de analisar é qual o preço que maximizaria os lucros.

Temos algumas opções aqui e acredito que a mais comum poderia ser a utilização de uma regressão linear. Mas será que ela é a com maior probabilidade de acerto? Para isso vamos entender ela e comparar ela com outras linhas de tendência.

![excel-sample002](https://github.com/user-attachments/assets/b4055411-8e0e-4e7f-86c9-0a7206f951ad)

Regressão linear é um método estatístico usado para modelar a relação entre uma variável dependente (y) e uma ou mais variáveis independentes (x). O objetivo principal é encontrar uma linha reta que melhor se ajusta aos dados.

Talvez por ser uma linha reta ela acaba não sendo a melhor opção para o cenário que temos, os preços nao seguem uma constante, então vamos comparar ela as tendências exponencial e logarítmica. Vemos que o Excel tem a opção de nos darmos as equação utilizadas para cada tendência escolhida. E vamos nos próximos passos colocar em prática essas formulas.

![image](https://github.com/user-attachments/assets/530db76e-c215-4346-a167-d2a1b917126a)

Extraido os valores e montado as equações vamos começar a relacionar cada modelo escolhido.

![image](https://github.com/user-attachments/assets/62289b1f-0ef7-4b85-8956-c3a870e29b68)

Vemos que para esse exemplo a linear não se saiu mal, porém a logarítmica ficou com melhor % de erro, e podemos descartar totalmente a potência para esse exemplo, apesar de visualmente como ela faz uma curva maior podemos pensar que iria acompanhar melhor a variação para esses dados não foi o caso.

Elaborada nossa defesa de qual modelo utilizar, vamos dar continuidade a nossa analise e enfim responder, qual preço a empresa deve cobrar para maximizar seu lucro?

![excel-sample003](https://github.com/user-attachments/assets/6adedd54-5187-4d9a-836a-16ea40b5777d)


Com isso achamos nosso valor mais lucrativo que podemos passar ao gerente decidir quals estratégias tomarem.

![image](https://github.com/user-attachments/assets/c7411867-2d26-426e-88b5-544317cd391e)

Valor de venda otimizado: **115 reais por Kg de café.**

![image](https://github.com/user-attachments/assets/1e3f158e-240b-40ee-a795-2a53f316f20a)

E adicionei um gráfico adicional para vermos que não é interessante aumentar muito o valor pois a demanda diminui e os lucros começam a cair mesmo que os produtos estão sendo vendidos por valores superiores.

### Este modelo é uma representação confiável da demanda no mundo real?

Por fim, acredito que sim, essa representação é um cenário muito comum no dia a dia, esses tipos de números e variáveis não estão fora da realidade de serem adquiridos, acho até que são números bem básicos para qualquer empresa ter e conforme o tamanho da empresa essa complexidade vai aumentando, que para fins de analise são até melhores para usarmos modelos mais detalhados, diminuir margens de erros etc.










