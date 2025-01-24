### Análise, dados do Recursos Humano

![image](https://github.com/user-attachments/assets/7b808402-2d63-43ff-94fa-d68d539b97e8)

## Link --> [Dashboard Final](https://app.powerbi.com/view?r=eyJrIjoiM2JlZjdmNGMtOWZjOS00MDg5LWFmYTQtOTA4NDNhYjQ3OGNlIiwidCI6ImU3ODllZDJmLWQ3YTUtNDJlMy1iODllLWJlOGE4YjJjZTY5YSJ9&pageName=2356803ad39e51ce9b3b)

Neste estudo de caso vamos explorar os dados de RH de uma empresa de software chamada Atlas Labs. Vamos realizar uma análise exploratória de dados e utilizar DAX para criar visualizações que ajudaram a nos aprofundar no tema de rotatividade (attrition) e nos fatores que a influenciam. Essa análise ajudará a empresa a determinar as ações necessárias para reter mais funcionários.

O que temos em mãos é um Esquema SnowFlake e fizemos algumas ligações de relacionamento entre as tabelas existentes.

![image](https://github.com/user-attachments/assets/9a02e77f-1d2c-4e28-8a1a-c05f4b6c6a55)

Após fazer uma limpeza e conferência de dados, vemos que temos muitas informações dos funcionários. Por exemplo sobre qual nota os funcionários dão sobre diversos tópicos, como: Gerência, Ambiente, Relações, Auto Avaliação, Trabalho etc...

Inicialmente gosto de criar algumas medidas padrões:

```
Total Empregados = COUNTA(Dim_Employee[EmployeeID])

Funcionário Ativo = CALCULATE(COUNTA(Dim_Employee[EmployeeID]),Dim_Employee[Attrition] = "Não")

Funcionário Inativo = CALCULATE(COUNTA(Dim_Employee[EmployeeID]),Dim_Employee[Attrition] = "Sim")

Taxa de Atrito = DIVIDE([Funcionário Inativo],[Total Empregados]) //Que irá ser multiplicado por 100 quando colocado em formato %
```

Por enquanto ficando com as seguintes medidas

![image](https://github.com/user-attachments/assets/feb6e7e9-e82c-4b72-a357-38a1a99b66ad)

Vamos tentar entender o fluxo de contratações conforme o tempo passou e analisar se há uma tendencia e uma relação disso sobre a taxa de atrito.

![sample001](https://github.com/user-attachments/assets/7b31ed1c-b007-4200-aecd-b22e31178fc1)

Como a tabela de datas já tinha uma relação com a tabela Fatos, a segunda relação ficou inativa e tivemos que forçar o uso dela com DAX utilizando a função USERELATIONSHIP() como visto na imagem acima.

```
Total Empregados Datas = CALCULATE([Total Empregados],USERELATIONSHIP(Dim_Employee[HireDate],DimDate[Date]))
```

Conseguimos notar que houve um aumento na rotatividade de funcionários nos últimos anos

![image](https://github.com/user-attachments/assets/30b8cb35-ce70-421c-b6a3-4b15ac191183)

Como a rotatividade é significativa para a empresa vamos tentar entender quais posições a empresa normalmente vem contratando, fazendo assim que o RH possa dar informações aos departamentos para se planejarem melhor nos futuros pedidos de contratações.

![image](https://github.com/user-attachments/assets/53e52023-82a8-468b-8215-e2cb243e77e2)

Não é surpresa que uma empresa de tecnologia tem uma demanda alta nas vagas de TI e a função com maior número de empregados é a de Engenheiro de Software. Agora que temos uma noção geral dos números da empresa, vamos começar a refinar nossas análises começando por Demografia.

## Demografia

A respeito da idade dos funcionários e em quais faixas etárias temos mais funcionários, criamos uma tabela condicional com os seguintes intervalos: <20; 20-29; 30-39; 40-49 e 50>.

![image](https://github.com/user-attachments/assets/fbbfe032-ef7a-4744-9c1b-a35bef4af05a)

Também investigamos algumas distribuições e relações entre gênero, etnias e estado civil.

![image](https://github.com/user-attachments/assets/fcf2f94d-1b81-49b9-82a0-aba740cef967)


![image](https://github.com/user-attachments/assets/9407de35-28d1-43ae-97f1-8679f494d549)

A próxima etapa foi criar ferramentas para podermos avaliar cada caso em particular com as avaliações e notas de satisfação que cada funcionário tem. Para isso criamos mais métricas para utilizarmos nos gráficos e após a criação dos mesmos ficamos com a tabela de _Medidas dessa forma:

![image](https://github.com/user-attachments/assets/889013a0-4330-45c9-82b6-993963945b15)

```
Satisfação Trabalho = MAX(FatosPerformanceRating[JobSatisfaction])
```

Um exemplo de uma medida que criamos, pegamos o valor máximo (apesar de termos apenas um valor na coluna) para vermos a relação das notas com o passar do tempo, assim podendo verificar a cada ano quais foram as avaliações e notas de cada funcionário. Isso ajuda o pessoal do RH a ter informações precisas a respeito de cada um para tomar as melhores medidas com base em cada contexto pessoal.

![image](https://github.com/user-attachments/assets/dc348a0f-15cd-45e8-ab44-8bdffd5d38fd)

Nesse exemplo vemos que a funcionária Garret Forrester está na empresa desde 2014, mas a última avaliação da gerencia e a auto avaliação demonstra uma certa queda com anos anteriores. Assim podemos interferir e evitar a chegar a um ponto no qual ela decida sair da empresa. Talvez essas notas sejam relacionadas a satisfação com o equilíbrio da vida profissional dela que vem com 3 anos na sequência com notas negativas (Nota: 2; Insatisfeito).

Mais algumas relações foram comparadas e adicionadas no dashboard final, como tempo na empresa, horas extras, viajar a trabalho etc. Se esses fatores tem relação com as taxas de desligamento dos funcionários com a empresa. Com isso podemos montar um cenário bem detalhado para o RH trabalhar em cima para diminuir essa rotatividade que vem aumentando com o passar dos anos na Atlas Lab.















