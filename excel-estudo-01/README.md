Análises e estudos para praticar.

A CellCaps vende capinhas de celulares ultra resistentes. A empresa está planejando imprimir um catálogo de seus produtos e realizar uma campanha de mala direta. O custo de impressão do catálogo é de R$20.000 mais R$0,10 por catálogo. O custo de envio de cada catálogo (incluindo postagem, formulários de pedido e compra de nomes de um banco de dados de mala direta) é de R$0,15. Além disso, a empresa planeja incluir envelopes de resposta direta em seu envio e incorrerá em um custo extra de R$0,20 por envelope de mala direta utilizado por um respondente. 

O tamanho médio de um pedido de cliente é de R$40, e o custo variável da empresa por pedido (principalmente devido a custos de mão-de-obra e material) é, em média, cerca de 80% do valor do pedido, ou seja, R$32. A empresa planeja enviar 100.000 catálogos. Ela deseja desenvolver um modelo de planilha para responder às seguintes perguntas:

- Como uma mudança na taxa de resposta afeta o lucro?

- Para qual taxa de resposta a empresa atinge o ponto de equilíbrio?

- Se a empresa estimar uma taxa de resposta de 3%, ela deve prosseguir com a mala direta?

- Como a presença de incerteza afeta a utilidade do modelo?


## Analise inicial

Primeiramente vamos entender o que é uma campanha de mala direta, na qual é uma estratégia de marketing em que uma empresa envia materiais promocionais, como catálogos, ofertas ou newsletters, diretamente para um grupo específico de consumidores ou empresas, com o objetivo de promover seus produtos ou serviços.

Custo de impressão: R$20.000

Custo adicional por catálogo R$0,10

Custo de envio que inclui tudo: R$0,15 cada

Envelope Resposta (se utilizado): R$0,20 cada

Tamanho médio de cada pedido: R$40,00

Custo médio por pedido: cerca de 80% do valor do pedido

Objetivo: Enviar 100.00 catálogos


Com esses dados fornecidos a seguinte tabela foi montada no excel, na tabela H coloquei a formula =FORMULATEXT() para mostrar os passos que coloquei em cada operação. Porém nas imagens após essa vou manter a coluna escondida para não poluir muito a tabela.

![image](https://github.com/user-attachments/assets/d2d0ca01-4aad-4d1a-98f0-7c4ce1d98611)

### Então com isso feito podemos começar a responder algumas perguntas, sendo a primeira: Como uma mudança na taxa de resposta afeta o lucro?

Para vermos com mais clareza quão sensível essa taxa de resposta pode afetar a campanha vamos fazer uma tabela com alguns valores para simularmos essa % de resposta, para facilitar essa tarefa podemos fazer uma *Data Table*.

![excel-sample001](https://github.com/user-attachments/assets/511bda44-4252-4538-8d7e-234eb87f8cbd)

E como uma análise final...

![image](https://github.com/user-attachments/assets/9fd0907b-0cf4-447f-abdd-7fc8b8ae2ef0)

Podemos observar como essa variação vai afetar os gastos da empresa. E que um ponto de equilibrio para ela parar de perder dinheiro e começar a lucrar com a campanha fica entre 5.5% e 6% em relação a taxa de resposta.

### Pergunta 2: Para qual taxa de resposta a empresa atinge o ponto de equilíbrio?

Para isso vamos usar a opção *Goal Seek* e achar exatamente o ponto de equilíbrio nessa taxa.

![excel-sample002](https://github.com/user-attachments/assets/bfe48d8d-32be-47c9-86c0-e8a294d7f387)

Assim podemos afirmar que para a empresa não perder dinheiro mas também não iria ter nenhum lucro, a taxa de resposta precisa ser de 5.77%, ou seja em torno de 5769 pedidos de um total de 100 mil enviados.

![image](https://github.com/user-attachments/assets/1f630c36-3ba8-487e-94eb-7762969c0c85)

### Pergunta 3: Se a empresa estimar uma taxa de resposta de 3%, ela deve prosseguir com a mala direta?

Como pudemos visualizar com a primeira pergunta, sabemos que uma taxa de 3% de respostas seria algo muito prejudicial financeiramente.

![image](https://github.com/user-attachments/assets/3755a8a5-99a6-4802-b4ac-80f70fc160a8)

Com 3% o prejuizo total esperado seria em torno de 21 mil e 600 reais. E o conselho seria para a empresa não prosseguir com a mala direta.

### Pergunta 4: Como a presença de incerteza afeta a utilidade do modelo?

Acredito que com mais clareza vimos o quão sensível é esse modelo montado. Os dois pontos cruciais que me chama a atenção seriam:

**Estimativa da Taxa de Resposta:** O modelo depende de uma previsão precisa da taxa de resposta dos clientes. Se houver incerteza significativa sobre essa taxa, as decisões baseadas no modelo podem ser incorretas. Por exemplo, prever uma taxa de 6% quando a taxa real pode ser menor (3% ou 4%) pode levar a prejuízos significativos.

**Preço médio de cada pedido:** Essa variável juntamente com a incerteza da taxa de resposta pode ocasionar ainda mais em um ponto negativo nessa campanha. Para aumentar a utilidade do modelo, seria necessário realizar análises de sensibilidade, ajustando as variáveis-chave para avaliar diferentes cenários e incluir margens de segurança na decisão final. Isso ajudaria a mitigar os riscos associados à incerteza.


