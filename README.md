# Estrutura-de-repticao-com-decisao-codigo-em-Java

Ir para o conteúdo principal
 
Moodle - IFRS

Programação Básica com Java III - Turma 2022B
Painel Meus cursos  PBJIII2022B 1. Integrando Estruturas de Controle  1.2. Combinando Estruturas de Repetição com Estruturas de Decisão
1.2. Combinando Estruturas de Repetição com Estruturas de Decisão
Assim como podemos combinar estruturas de decisão, é possível também combinar estruturas de decisão com estruturas de repetição. Vamos a outro problema. Imagine que você deseja trabalhar em uma empresa que desenvolve jogos eletrônicos. Como teste de avaliação de suas habilidades técnicas, a empresa lhe envia o seguinte problema:

Seu desafio é construir um jogo de adivinhação de números. O programa deve, inicialmente, sortear um número entre 1 e 1000. Durante o jogo, o usuário poderá realizar palpites, digitando um número o qual acredita ser o número sorteado. A cada palpite, o programa deve mostrar uma das três mensagens abaixo:

“Muito alto”, caso o palpite digitado pelo usuário seja maior do que o valor sorteado pelo programa;
“Muito baixo”, caso o palpite digitado pelo usuário seja menor do que o valor sorteado pelo programa;
“Você acertou!”, caso o palpite digitado pelo usuário seja igual ao valor sorteado pelo programa.
O programa deve continuar recebendo palpites do usuário até que ele acerte o número sorteado. Ou seja, o jogo só termina quando o usuário acertar o valor sorteado.

Um jogo! Que interessante! Um jogo nada mais é do que um programa de computador e nosso desafio não é diferente.  Então, vamos começar a resolver este problema fazendo a análise das entradas e saídas do programa, bem como do processamento necessário:

Segundo o enunciado do problema, o usuário precisará informar seus palpites e nada mais. Cada palpite deve ser um número inteiro.
O programa deverá mostrar uma mensagem para cada palpite enviado pelo usuário. As mensagens a serem mostradas estão descritas no enunciado do problema.
O primeiro tipo de processamento que o programa precisará realizar é sortear um número. Este número deverá ser adivinhado pelo usuário. A cada palpite informado pelo usuário o programa deverá verificar se o palpite é maior, menor ou igual ao número sorteado. Em cada um dos três casos, uma mensagem diferente deve ser mostrada.
Vamos começar simplificando o problema. Vamos considerar que o usuário terá direito a um único palpite. Nesse caso, podemos escrever o rascunho mostrado abaixo.

Sortear o NÚMERO SECRETO
Ler o PALPITE do usuário
Se PALPITE é maior do que o NÚMERO SORTEADO, mostrar a mensagem “Muito alto”
Se PALPITE é menor do que o NÚMERO SORTEADO, mostrar a mensagem “Muito baixo”
Se PALPITE é ao NÚMERO SORTEADO, mostrar a mensagem “Você acertou!”.
Para realizar o passo 1 precisamos de um mecanismo que nos permita sortear números. Como você já deve saber, a linguagem Java possui o método Math.random que nos permite sortear um número. O passo 2 é trivial e os passos 3 a 5 nos exigem o uso de estruturas de decisão. Para construir essas estruturas se...então podemos utilizar uma abordagem similar a que fizemos no tópico anterior, onde utilizamos estruturas aninhadas para diminuir o número de testes necessários. Assim, chegamos ao pseudocódigo mostrado abaixo.



Algoritmo “Jogo de Adivinhação (versão 1)”

var

       numero_sorteado, palpite: inteiro

início

       numero_sorteado ← sortear um número de 1 a 1000

       leia palpite

       se palpite > numero_sorteado então

             escreva “Muito alto”

       senão

             se palpite < numero_sorteado então

                    escreva “Muito baixo”

              senão

                    escreva “Você acertou!”

             fim se

       fim se

fim


Esse algoritmo funciona para apenas um palpite. Mas precisamos de vários deles! Na verdade precisamos fornecer a possibilidade do usuário fazer palpites até acertar o número sorteado. Isso lembra uma estrutura de repetição com uma condição. Como já vimos até aqui, temos duas opções: utilizar uma estrutura enquanto ou utilizar uma estrutura repita. Lembre-se que a diferença entre elas está em quando a condição é testada: se antes ou depois de se executar o bloco de instruções.

O que deve ser repetido? Analisando o enunciado do problema e o algoritmo anterior, podemos perceber que tudo, exceto a geração do número sorteado deve ser repetido. Lembre-se de que o número deve ser sorteado apenas uma vez, no início do jogo. Até o programa terminar, o número deve permanecer o mesmo.      Assim, chegamos aos algoritmos mostrados abaixo. O primeiro mostra a solução utilizando uma estrutura enquanto. Já o segundo utiliza uma estrutura repita.



Algoritmo “Jogo de Adivinhação (com enquanto)”

var

       numero_sorteado, palpite: inteiro

início

       numero_sorteado ← sortear um número de 1 a 1000

       palpite ← 0

enquanto palpite != numero_sorteado faça

              leia palpite

se palpite > numero_sorteado então

                    escreva “Muito alto”

              senão

                    se palpite < numero_sorteado então

                          escreva “Muito baixo”

                    senão

                           escreva “Você acertou!”

                    fim se

              fim se

       fim enquanto

fim


Algoritmo “Jogo de Adivinhação (com repita)”

var

       numero_sorteado, palpite: inteiro

início

       numero_sorteado ← sortear um número de 1 a 1000

       repita

              leia palpite

se palpite > numero_sorteado então

                    escreva “Muito alto”

              senão

                    se palpite < numero_sorteado então

                          escreva “Muito baixo”

                    senão

                           escreva “Você acertou!”

                    fim se

              fim se

       até que palpite = numero_sorteado

fim


As duas soluções são quase idênticas, porém há uma diferença. Na solução com enquanto foi necessário atribuir o valor zero à variável palpite antes do início da estrutura enquanto (na verdade qualquer valor menor do que 1 poderia ser utilizado). Esta operação foi necessária para que a variável contivesse um valor válido antes da comparação feita na condição do enquanto.  Isto não foi necessário na solução com repita, pois a condição é verificada após a execução do bloco de instruções interno, onde a variável palpite já recebe um valor válido (através do comando leia).

O código em Java para o jogo de adivinhação é mostrado abaixo. Note que foi implementado o algoritmo que utiliza uma estrutura repita (essa solução é menor e mais elegante[1]). Também utilizamos o método Math.random seguindo fórmula indicada no curso Programação Básica com Java II.



public class JogoDeAdivinhacao {

       public static void main(String[] args) {

             int numero_sorteado, palpite; 

             numero_sorteado = (int)(Math.random()*1000+1);

             do {

System.out.print(“Palpite: ”);

palpite = Integer.parseInt(System.console().readLine());

      

if(palpite > numero_sorteado)

                    System.out.println(“Muito alto”);

              else if(palpite < numero_sorteado)

                    System.out.println(“Muito baixo”);

              else

                    System.out.println(“Você acertou!”);

       } while(palpite != numero_sorteado);

}


}


 Você pode notar que não é complicado combinar uma ou mais estruturas de decisão dentro de uma estrutura de repetição. Se você pensar primeiro no código que deve ir dentro da repetição e depois construir a repetição em si fica mais fácil (como acabamos de fazer com o jogo de adivinhação). Assim, você acabou de realizar o desafio proposto e poderá ganhar o emprego na empresa de desenvolvimento de jogos!
Agora vem a parte triste! Infelizmente, nem sempre essa estratégia pode ser aplicada. Vejamos outro problema:

Escreva um programa que leia 20 notas de uma turma e mostre a maior e a menor.

Neste problema, a entrada a ser fornecida é composta pelas 20 notas dos estudantes da turma. As saídas serão os valores da maior e da menor nota.  A questão complexa desse problema é: como processar as entradas e gerar as saídas? Vamos nos concentrar primeiramente no problema de encontrar a maior das 20 notas e depois modificar essa solução para encontrar a menor delas (você verá que as soluções para ambos os problemas são bastante similares).

Para que uma nota seja a maior, seu valor precisa ser maior ou igual a cada uma das restantes. Assim, uma nota n1 será a maior se for maior ou igual n2, maior ou igual a n3, e assim por diante (até n20).  Poderíamos transcrever isso em um pseudocódigo como mostrado abaixo.


Algoritmo “Maior de 20 notas (versão 1)”

var

       n1,n2,n3,n4,n5,n6,n7,n8,n9,n10,n11,n12,n13,n14,n15,n16,n17,n18,n19,n20: real

início

       leia n1,n2,n3,n4,n5,n6,n7,n8,n9,n10,n11,n12,n13,n14,n15,n16,n17,n18,n19,n20

 

       se n1 >= n2 e n1 >= n3 e n1 >= n4 e n1 >= n5 e n1 >= n6 e n1 >= n7 e n1 >= n8 e

n1 >= n9 e n1 >= n10 e n1 >= n11 e n1 >= n12 e n1 >= n13 e n1 >= n14 e

n1 >= n15 e n1 >= n16 e n1 >= n17 e n1 >= n18 e n1 >= n19 e n1 >= n20 então

             escreva “Maior nota: ”, n1

       fim se

 

       se n2 >= n1 e n2 >= n3 e n2 >= n4 e n2 >= n5 e n2 >= n6 e n2 >= n7 e n2 >= n8 e

n2 >= n9 e n2 >= n10 e n2 >= n11 e n2 >= n12 e n2 >= n13 e n2 >= n14 e

n2 >= n15 e n2 >= n16 e n2 >= n17 e n2 >= n18 e n2 >= n19 e n2 >= n20 então

             escreva “Maior nota: ”, n2

       fim se

       ...

       se n20 >= n1 e n20 > n2 e n20 >= n3 e n20 >= n4 e n20 >= n5 e n20 >= n6 e

n20 >= n7 e n20 >= n8 e n20 >= n9 e n20 >= n10 e n20 >= n11 e

n20 >= n12 e n20 >= n13 e n20 >= n14 e n20 >= n15 e n20 >= n16 e

n20 >= n17 e n20 >= n18 e n20 >= n19 então

             escreva “Maior nota: ”, n20

       fim se

fim


Essa solução funciona, mas não é nada elegante! O algoritmo está bem grande (isso que boa parte dele foi omitida). Isso é um problema, pois imagine se precisássemos encontrar a maior de 100 notas!

Há outra forma mais elegante de resolver esse problema? A resposta é sim, mas precisamos raciocinar nele de forma um pouco diferente. Vamos começar criando uma única variável (em vez de 20) para receber cada nota. Vamos chamar essa variável de nota. Assim, a ideia é ler cada nota em um comando leia separado, como mostrado abaixo. Os três pontos (...) após cada leia indicam que haverá mais instruções ali futuramente.


Algoritmo “Maior de 20 notas (versão 2)”

var

       nota: real

início

       leia nota

       ...

leia nota

...

leia nota

...

Repetir isso mais 17 vezes

fim


Posso adivinhar seus pensamentos: qual o objetivo disso? Vamos utilizar as leituras sequenciais para fazer comparações parciais dos valores lidos, ao contrário da primeira versão, onde consideramos todas as 20 notas em cada comparação.

Após o primeiro leia, quantos notas o programa já obteve do usuário? Apenas um comando leia foi executado com uma única variável, resultando em um único valor lido. Em uma lista de notas com apenas uma nota, essa é a maior (se você fosse o único estudante de uma turma sempre tiraria a maior nota). Criaremos uma variável chamada maior que deverá conter, no final da execução do programa, a maior nota. Vamos, então, substituir o primeiro “...” por uma atribuição de nota para maior como mostrado abaixo.


Algoritmo “Maior de 20 notas (versão 2)”

var

       nota, maior: real

início

       leia nota

       maior ← nota

leia nota

...

leia nota

...

Repetir isso mais 17 vezes

fim


Após o segundo leia, temos duas notas lidas. A segunda nota passará a ser a maior somente se for superior ao valor da primeira. O valor da primeira nota está armazenado na variável maior. Assim, podemos substituir o segundo “...” por uma estrutura se...então, como mostrado no algoritmo abaixo.


Algoritmo “Maior de 20 notas (versão 2)”

var

       nota, maior: real

início

       leia nota

       maior ← nota

 

leia nota

se nota > maior então

       maior ← nota

fim se

 

leia nota

...

Repetir isso mais 17 vezes

fim


E quanto à terceira nota? Para ela ser a maior até o momento, deve ser maior do que a primeira e a segunda notas. Porém não temos mais nenhuma das duas armazenadas em variáveis para realizar esse teste. Felizmente, não precisamos mais delas. Basta verificar se a terceira nota é maior do que a MAIOR delas, que está armazenada na variável maior. Assim, obtemos o pseudocódigo abaixo.


Algoritmo “Maior de 20 notas (versão 2)”

var

       nota, maior: real

início

       leia nota

       maior ← nota

 

leia nota

se nota > maior então

       maior ← nota

fim se

 

leia nota

se nota > maior então

       maior ← nota

fim se

...

Repetir isso mais 17 vezes

fim


Observando o código percebe-se que o código que escrevemos para a terceira nota é idêntico ao que escrevemos para a segunda nota. Será que isso é um padrão que se repete?

A resposta é sim. Para que qualquer nota posterior possa ser a maior até o momento, é necessário que seu valor seja maior do que o valor presente na variável maior (que guarda o valor da maior nota digitada até o momento, não esqueça disso). Assim, temos um mesmo código que será repetido a partir da segunda nota até a vigésima. Quando precisamos repetir algo diversas vezes, o que devemos utilizar? Bingo! Uma estrutura de repetição! Como neste caso temos um número fixo de repetições a realizar, podemos utilizar uma repetição controlada por contador através de uma estrutura para...faça. O algoritmo resultante é mostrado abaixo.



Algoritmo “Maior de 20 notas (versão final)”

var

nota, maior: real

cont: inteiro

início

       leia nota

       maior ← nota

para cont de 2 até 20 faça

leia nota

se nota > maior então

             maior ← nota

fim se

fim para

       escreva “Maior nota: ”, maior

fim


A estrutura para...faça que colocamos no algoritmo utiliza uma variável inteira cont como sua variável contadora. Essa variável deve começar recebendo o valor 2, já que a primeira nota já foi lida e processada antes (a estrutura para...faça vai processar as notas a partir da segunda). Também poderíamos iniciar a variável cont com 1 e fazer com que ela fosse até 19. O resultado final não seria alterado (na verdade, se você escolher qualquer intervalo que resulte em 19 números o algoritmo continuará correto).

Para completar a solução do problema, precisamos também encontrar a menor nota digitada. A lógica nesse caso é a mesma. Precisaremos de uma variável para guardar o menor valor até o momento (que chamaremos de menor) e comparar cada nota lida com ela, utilizando o operador < (menor que). Obtemos, assim, o algoritmo mostrado abaixo.


Algoritmo “Maior e Menor de 20 notas”

var

nota, maior, menor: real

cont: inteiro

início

       leia nota

       maior ← nota

       menor ← nota

para cont de 2 até 20 faça

leia nota

se nota > maior então

             maior ← nota

fim se

se nota < menor então

             menor ← nota

fim se

fim para 

       escreva “Maior nota: ”, maior

       escreva “Menor nota: ”, menor

fim


Veja que mantivemos um único para...faça e não dois (queremos continuar lendo 20 notas, e não 40). Note que o restante do código é praticamente idêntico ao da verificação de maior nota.

O programa em Java resultante é mostrado abaixo. Um detalhe que é importante mencionar é que a variável cont foi declarada no próprio for, o que é uma prática bastante comum entre programadores.

public class MaiorMenorDe20Notas {

       public static void main(String[] args) {

double nota, maior, menor;

System.out.print(“Informe a nota 1: ”);

              nota = Double.parseDouble(System.console().readLine());

              maior = nota;

              menor = nota;

 

              for(int cont = 2; cont <= 20; cont++) {

System.out.printf(“Informe a nota %d: ”, cont);

nota = Double.parseDouble(System.console().readLine());  

if(nota > maior)

                    maior = nota;

if(nota < menor)

                    menor = nota;

       }

       System.out.printf(“Maior nota = %.1f\n”, maior);

       System.out.printf(“Menor nota = %.1f\n”, menor);

}

}


[1] Provavelmente você nunca viu o adjetivo elegante ser aplicado a um código de computador. Em textos técnicos sobre programação é comum utilizar esse adjetivo para códigos claros, pequenos e com bom desempenho, que não se utilizam de “gambiarras” para resolver o problema.


Última atualização: domingo, 1 nov 2020, 16:58
Seguir para...
Academi
Dúvidas? 
Perguntas frequentes

Fale conosco | Suporte | Contato

Informação
Termos e Condições de Uso
Aviso de Privacidade e Proteção de Dados Pessoais
Contato
Rua Gen. Osório, 348, Bento Gonçalves/RS
Siga-nos
Copyright © 2017 - Desenvolvido por LMSACE.com. Distribuído por Moodle

Português - Brasil ‎(pt_br)‎
English ‎(en)‎
Español - Internacional ‎(es)‎
Français ‎(fr)‎
Italiano ‎(it)‎
Português - Brasil ‎(pt_br)‎
Mudar para o tema padrão
