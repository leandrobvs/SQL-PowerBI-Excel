![image](https://github.com/user-attachments/assets/715fa0d1-cda5-498f-b8ce-eafdbdc70a8c)


Uma grande empresa farmacêutica, Zephyr Pharmaceutika, está avaliando se deve prosseguir com o desenvolvimento de um de seus novos medicamentos, Aurora. 
Aurora está nos estágios finais de desenvolvimento e estará pronta para ser lançada no mercado daqui a um ano. O custo restante de desenvolvimento, que será incorrido no início do ano 1, é de R$7,5M.

A empresa estima que a demanda por Aurora inicialmente crescerá e, posteriormente, diminuirá gradualmente ao longo de sua vida útil de 18 anos. 
Especificamente, espera-se que as margens brutas (receita menos custos) sejam de R$900K no ano 1, aumentando a uma taxa anual de 12% até o ano 6 e, depois, diminuindo a uma taxa anual de 4% até o ano 18.

A Zephyr Pharmaceuticals deseja desenvolver um modelo em planilha para estimar os fluxos de caixa ao longo dos 18 anos, assumindo que todos os fluxos de caixa, exceto o custo inicial de desenvolvimento, ocorram no final dos respectivos anos. 
Utilizando uma taxa de desconto anual de 10% para calcular o valor presente líquido (VPL), a empresa pretende responder às seguintes perguntas:

 - A Zephyr Pharmaceuticals deve prosseguir com Aurora ou abandonar o projeto agora para evitar incorrer no custo de desenvolvimento de R$7,5M?
 - Como mudanças em premissas importantes, como taxa de crescimento, taxa de desconto ou vida útil, afetam a decisão?

## VPL

Vamos começar colocando todos os dados que vão ser referênciados nos cálculos em uma tabela inicial:

![image](https://github.com/user-attachments/assets/6d0aab87-9105-4ca0-8658-10a4366e42f4)

E com isso, podemos montar o fluxo de caixa dos 18 anos que nos pedem, com taxa de aumento até o sexto ano e, após isso, diminuição de 4% ao ano. A seguinte tabela foi montada. Vou deixar a função **FORMULATEXT()** na primeira ocorrência do uso de uma fórmula, mas ela se repete ao longo de toda a tabela. Utilizamos a função **IF()** caso o ano seja menor ou igual a 6, aplicamos o cálculo de aumento caso contrário, aplicamos o cálculo de diminuição.

![image](https://github.com/user-attachments/assets/9247ca50-94ea-49c9-8b75-d53f48e89978)

Agora podemos usar a fórmula **NVP()** (ou **VPL()** na versão pt-br) para calcular o VPL, lembrando um pequeno detalhe do Excel que mesmo tendo a fórmula com esse nome ele não faz o cáculo total do VPL, talvez pela fórmula ser NPV(taxa, valor1, [valor2], ...) ela fica em aberto o número de caixas futuros que cada um vai colocar, não daria para saber em qual argumento colocariamos o valor do investimento inicial que tem que ser subtraído no final do cálculo. Poderiam atualizar a fórmula para NPV(taxa, investimento_inicial, valor1, [valor2],...) assim fazendo tudo de uma vez, mas poderia confundir, apesar do nome confundir de qualquer maneira.

Enfim após esse devaneio, temos o resultado do VPL.

![image](https://github.com/user-attachments/assets/fc73201f-505e-4462-a659-5d3f0266eea0)

Então a resposta para a primeira pergunta:

- A Zephyr Pharmaceuticals deve prosseguir com Aurora ou abandonar o projeto agora para evitar incorrer no custo de desenvolvimento de R$7,5M?

Sim, sugerimos que com esses dados em mãos a empresa pode prosseguir com o projeto, ele é viável.

Agora a respeito da segunda questão que nos foi dada:

 - Como mudanças em premissas importantes, como taxa de crescimento, taxa de desconto ou vida útil, afetam a decisão?

Parece que temos um resultado bem sólido com esses números, mesmo diminuindo a taxa pela metade, ainda assim o projeto fica com números interessantes.

![image](https://github.com/user-attachments/assets/24813603-c75e-4194-b6ed-75c04f1fbf04)

Já a taxa de desconto aumentada de 10% para 15% já faz o projeto ficar inviável com os números padrões do problema.

![image](https://github.com/user-attachments/assets/a6696df1-00c0-4db6-8948-02b0f3679a65)












