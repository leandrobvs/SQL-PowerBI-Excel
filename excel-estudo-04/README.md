### Problema:

![image](https://github.com/user-attachments/assets/2932ae7f-d1f3-446c-ac6b-22f9c50e92cd)

Utilize a **Programação Linear** (PL) para resolver o seguinte:

Um candidato a prefeito alocou R$80.000 para propaganda de última hora nos dias que antecedem a eleição. Dois tipos de anúncios serão utilizados: rádio e televisão. Cada anúncio de rádio custa R$400 e alcança um público estimado de 6.000 pessoas. 

Cada anúncio de televisão custa R$1.000 e alcança um público estimado de 14.000 pessoas. O candidato deseja alcançar o maior número possível de pessoas, mas estipulou que devem ser utilizados pelo menos 20 anúncios de cada tipo. 
Além disso, o número de anúncios de rádio deve ser pelo menos igual ao número de anúncios de televisão.

Perguntas:

- Quantos anúncios de cada tipo devem ser utilizados?
- Quantas pessoas serão alcançadas?

### Análise

Com isso nós temos as variáveis de decisão:

  x: número de anúncios de rádio.
  y: número de anúncios de televisão.

Então queremos maximizar o número de pessoas alcançadas (Z) assim tendo

Z = 6000x + 14000y

As **Restrições** que nos foram impostas ficam sendo

Orçamentária:

400x + 1000y ≤ 80000

Mínima de anúncios:

x ≥ 20

y ≥ 20

Sendo Rádio (x) >= TV (y)

Com isso temos o cenário montado no Excel

![image](https://github.com/user-attachments/assets/37bc285d-5005-42da-8fe8-58267d0595e0)

Para facilicar nossos cálculos podemos utilizar o add-in Solver que já vem disponível para ser habilitado no Excel

![image](https://github.com/user-attachments/assets/f665a599-d4c8-4647-857f-552e1288727a)

E finalizamos o cálculo.

![excel-sample001](https://github.com/user-attachments/assets/0a78601a-e08a-4484-b2fc-6b0655877721)

Assim utilizando o Solver com o método Simplex LP, que seria Programação Linear, os números que otimizariam o alcance do público são:

![image](https://github.com/user-attachments/assets/48ee4693-5b73-477c-84b8-b7ae566e9de5)

Assim respeitariamos todas as restrições impostas e alcançariamos um número de 1.180.000 pessoas.





