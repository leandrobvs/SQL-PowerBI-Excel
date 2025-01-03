### Análise, dados do Recursos Humano

![image](https://github.com/user-attachments/assets/7b808402-2d63-43ff-94fa-d68d539b97e8)

## Link --> [Dashboard Final](linkhere)

Neste estudo de caso vamos explorar os dados de RH de uma empresa fictícia de software chamada Atlas Labs. Vamos realizar uma análise exploratória de dados e utilizar DAX para criar visualizações que ajudaram a nos aprofundar no tema de rotatividade (attrition) e nos fatores que a influenciam. Essa análise ajudará a empresa a determinar as ações necessárias para reter mais funcionários.

O que temos em mãos é um Esquema SnowFlake e fizemos algumas ligações de relacionamento entre as tabelas existentes.

![image](https://github.com/user-attachments/assets/9a02e77f-1d2c-4e28-8a1a-c05f4b6c6a55)

Após fazer uma limpeza e conferência de dados, vemos que temos muitas informações dos funcionários. Por exemplo sobre qual nota os funcionários dão sobre diversos tópicos, como: Gerencia, Ambiente, Relações, Auto Avaliação, Trabalho etc...

Inicialmente gosto de criar algumas medidas padrões:

```
Total Empregados = COUNTA(Dim_Employee[EmployeeID])

Funcionário Ativo = CALCULATE(COUNTA(Dim_Employee[EmployeeID]),Dim_Employee[Attrition] = "Não")

Funcionário Inativo = CALCULATE(COUNTA(Dim_Employee[EmployeeID]),Dim_Employee[Attrition] = "Sim")

Taxa de Atrito = DIVIDE([Funcionário Inativo],[Total Empregados]) //Que irá ser multiplicado por 100 quando colocado em formato %
```

Por enquanto ficando com as seguintes medidas

![image](https://github.com/user-attachments/assets/feb6e7e9-e82c-4b72-a357-38a1a99b66ad)







