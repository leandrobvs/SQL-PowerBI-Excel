### Estudo de caso feito com dataset fictício sobre uma companhia telefonica americana chamada Databel.

![image](https://github.com/user-attachments/assets/49dd4b08-090c-496c-a48e-60266bb109c6)

## Dashboard Final - PLACEHOLDER LINK

> [!NOTE]  
> Para quem se interessar no passo a passo e ideias que foram surgindo ao longo da analise pode acompanhar o processo nas descrições abaixo. Caso se interessar apenas com o produto final o link acima o levará para o dashboard com os resultados da analise. Obrigado.

### Metadados | Analisando a evasão de clientes

**Situação do cliente**

nome da coluna  | conteúdo
------------- | -------------
Customer ID  | Identificador único que identifica um cliente
Churn Label  | Contém “Sim” ou “Não” para indicar se o cliente cancelou
Churn Reason | A razão particular pela qual o cliente encerrou o contrato
Churn Category | Agrupa várias razões de cancelamento para fins de análise

**Demografia**

nome da coluna  | conteúdo
------------- | -------------
Gender  | O gênero do cliente, indicado por “Masculino”, “Feminino” ou “Prefere não dizer”
Under 30 | Indica se o cliente tem menos de 30 anos com “Sim” ou “Não”
Senior | Indica se o cliente tem 65 anos ou mais com “Sim” ou “Não”
Age | A idade do cliente

**Informações contratuais**

nome da coluna  | conteúdo
------------- | -------------
Contract Type  | Contém “Mensal”, “Um Ano” ou “Dois Anos”
Payment Method | Método de pagamento preferido do cliente indicado por “Cartão de Crédito”, “Débito Direto” ou “Cheque”
State | O código do estado onde o cliente reside
Phone Number | Número de telefone do cliente
Group | Indica se o cliente faz parte de um contrato coletivo. Um contrato coletivo oferece vantagens e geralmente é mais barato. Contém “Sim” ou “Não”
Number of customers in a group | Número de clientes no grupo

**Tipos de assinatura e cobranças**

nome da coluna  | conteúdo
------------- | -------------
Account Length  | O número de meses que o cliente está com o Databel
Local Calls | Quantidade de chamadas locais (dentro dos EUA) feitas pelo cliente
Intl Calls | Quantidade de chamadas internacionais (fora dos EUA) feitas pelo cliente
Intl Mins | Número de minutos gastos em chamadas internacionais
Intl Active | Indica se o cliente fez chamadas internacionais com “Sim” ou “Não”
Intl Plan | Indica se o cliente possui um plano premium para chamadas internacionais gratuitas com “Sim” ou “Não”. Esse premium é refletido no valor da cobrança mensal
Extra International Charges | Contém as cobranças extras por chamadas internacionais para clientes que não estão em um plano internacional
Customer Service Calls | O número de chamadas feitas para o atendimento ao cliente
Avg Monthly GB Download | Contém o volume médio mensal de download em gigabytes
Unlimited Data Plan | Indica se o cliente tem capacidade de download ilimitada com “Sim” ou “Não”. Esse premium é refletido no valor da cobrança mensal
Extra Data Charges | Contém as cobranças extras por downloads de dados para clientes que não estão em um plano ilimitado
Monthly Charges | Média de todas as cobranças mensais do cliente
Total Charges | Soma de todas as cobranças mensais

## Primeiros Cálculos

Inicialmente fiz alguns cálculos utilizando expressões DAX para criar algumas medidas, segue a lista das medidas criadas e quais expressão utilizadas:

![image](https://github.com/user-attachments/assets/ef597c8f-ebb1-4cf8-bf45-7ef8344746a7)

```
Numero de Consumidores = COUNTA('Databel - Data'[Customer ID])

Numero de IDs unicas = DISTINCTCOUNT('Databel - Data'[Customer ID])

Evasão de Clientes = CALCULATE(COUNTA('Databel - Data'[Churn Label]),'Databel - Data'[Churn Label] = "Yes")

Porcentagem de Evasão = DIVIDE([Evasão de Clientes],[Numero de Consumidores])
```

Com isso criei alguns cartões com essas informações e deixei esses cartões em uma página chamada 'Data Check' para futuras conferências.

![image](https://github.com/user-attachments/assets/bf4600cb-da65-4a8c-b232-3d0831f8697e)

De cara notamos que a taxa de cancelamente de clientes é alta (26.86%).

Jogando os dados que temos em mãos sobre os cancelamentos dos clientes, vamos entender as razões por trás dessa evasão tão alta.

![image](https://github.com/user-attachments/assets/13353952-f565-4917-8eca-7fa5a05b9fbc)

Vamos tentar entender se o problema pode ser regional ou se há uma constancia em todo o país.

![image](https://github.com/user-attachments/assets/000d46f7-f5dc-4811-977e-d2582a2e6d1d)

No geral cada estado tem uma taxa de cancelamento próxima a média geral, porém um estado chama a atenção, a California se destaca com mais de 60% de cancelamentos e levanta a dúvida se naquele estado se encontra alguma problema diferente dos demais.

## Analise Demografica

Foi criado uma nova coluna chamada Demografia e vamos categorizar por idade ela. Pessoas com idade superior a 65 foram  colocados no categoria Sênior, com idades inferiores a 30 na Menor que 30 e o restante em Outros, que seriam pessoas entre 30 e 65 anos.

```
Demografia = 
SWITCH(
    TRUE(),
    'Databel - Data'[Age] >= 65, "Sênior",
    'Databel - Data'[Age] < 30, "Menor que 30",
    "Outros"
)
```

![image](https://github.com/user-attachments/assets/a5e95c4f-169a-46e7-9bf7-c80d7c2dc212)

Descobrimos que entre a categoria Sênior a porcentagem de cancelamento entre eles é acima da média das outras categorias, uma descoberta que pode vir a nos dizer algo durante o resto das analises.

![image](https://github.com/user-attachments/assets/d218693a-e513-44c4-b9a6-c15423577e71)

Assim podemos notar que conforme a idade avança a taxa de cancelamento aumenta e consequentemente faz com que esses grupos sejam os que tem menor número de clientes.

Será que as pessoas que estão em planos família tem mais vantagens sobre os planos individuais e se isso interfere também na taxa de cancelamento. Vamos descobrir no gráfico a seguir.

![image](https://github.com/user-attachments/assets/bd79ac9b-f90e-40a6-a7b6-2151f66c5be1)

Quem não participa de algum plano em conjunto tem uma média mensal de cobranças de mais de 30 dolares e com taxas de cancelamento também acima dos 30%. Já os planos em conjunto tem uma redução nesse valor médio que fica em torno de 20 dolares e as taxas de cancelamento diminuiem para níveis abaixo de 10%.






