# Linguagem de Montagem III: MIPS

### Instruções de suporte a procedimentos
Também conhecido como funções (com retorno ou tipo void)

Passos em um procedimento:
1. Colocar os parâmetros em um lugar onde o procedimento possa acessá-los;
2. Transferir o controle para o procedimento;
3. Adquirir recursos de armazenamento necessários para o procedimento;
4. Realizar a tarefa desejada;
5. Colocar o valor de retorno em um lugar onde o programa que o chamou possa acessá-lo;
6. Retornar o controle para o ponto de origem.

Qual o lugar mais rápido em que se pode armazenar/manipular dados em um sistema eletrônico?
Registradores MIPS:
* $a0 - $a3: parâmetros para os procedimentos;
* $v0 - $v1: valores de retorno do procedimento;
* $ra: registrador de endereço de retorno ao ponto de origem (ra = return address).

![image](/Image/Instru%C3%A7%C3%B5es%20de%20suporte%20a%20procedimentos.png)

### Instruções de suporte a procedimentos: jal (jump and link)
Link, neste caso, quer dizer é armazenado, no registrador $ra, o endereço da instrução que vem logo após a instrução jal Label:

    Código equivalente:

    addi $ra, $PC, 4
    j Label

Por que Existe a instrução jal?

### Instruções de suporte a procedimentos

![image](/Image/Exemplo%20formato%20de%20instru%C3%A7%C3%B5es.png)

### Usando mais registradores
**Q:** Se precisar mais de 4 argumentos e 2 valores de retorno?.
**Q:** Se o procedimento necessitar utilizar registradores salvos $sx?
**A:** Processo conhecido por *register spilling:*
* Uso de uma pilha;
* Temos um apontador para o topo da pilha;
* Este apontador é ajustado em uma palavra para cada registrador que é colocado na pilha (push), ou retirado da pilha (pop).
* Em MIPS, o registrador $29 é utilizado somente para indicar o topo da pilha: $sp (stack pointer).

### A Pilha
* Por razões históricas, a pilha "cresce" do maior endereço para o menor endereço.
* Para colocar um valor na pilha (push), devemos decrementar $sp em uma palavra e mover o valor desejado para a posição de memória apontada por $sp;
* Para retirar um valor da pilha (pop), devemos ler este valor da posição de memória apontado por $sp, e estão incrementar $sp em uma palavra.

### Exemplo de procedimentos folha (que não chamam outros procedimentos)

![image](/Image/Exemplo%20de%20procedimentos%20folha%20(que%20n%C3%A3o%20chamam%20outros%20procedimentos).png)

Vamos gerar o código correspondente em assembly MIPS.

![image](/Image/2.Exemplo%20de%20procedimentos%20folha%20(que%20n%C3%A3o%20chamam%20outros%20procedimentos).png)

![image](/Image/Comp%20da%20pilha.png)

![image](/Image/2.%20Comp%20da%20pilha.png)

![image](/Image/3.%20comp%20da%20pilha.png)

![image](/Image/C%C3%B3d%20Pilha%20Didatico.png)

![image](/Image/C%C3%B3d%20Pilha%20NaoDidatico.png)

### Procedimentos Aninhados
* Suponha o seguinte procedimento aninhado:

![image](/Image/Proc%20Aninhado.png)

* **Problema:** conflito com registradores $ax e $ra!
* Como resolver?

Covenção sobre registradores:
* Uma solução é empilhar todos os registradores que precisam ser preservados.
* Estabelecer uma convenção entre sbrotinas chamada e chamadora sobre a preservação dos registradores (uso eficiente da pilha).
* Definições:

    Chamadora(Caller): função que faz a chamada, utilizando jal;
    Chamada(Callee): função sendo chamada/receptora.

Benefícios:
* Porgramadores podem escrever funções que funcionam juntas;
* Funções que chamam outras funções - como as recursivas - funcionam corretamente.

![image](/Image/Exemplo%20soma%20recursiva.png)

Vamos gerar o código correspondente em assembly MIPS.

![image](/Image/soma%20recursiva%202.png)

![image](/Image/Soma%20recursiva%203.png)

![image](/Image/Soma%20recusiva%204.png)

![image](/Image/soma%20recursiva%205.png)

![image](/Image/Soma%20recursiva%206.png)

### O que deve ser preservado?

![image](/Image/Prev%20e%20not.png)

### Alocando espaço para novos dados (locais) na pilha
Frame de procedimento (Registro de ativação)
* Armazenar variáveis locais a um procedimento
* Facilita o acesso a essas variáveis locais ter um apontador estável $fp

### Frame de procedimento
![image](/Image/Frame%20de%20procedimento.png)

### Alocação de memória (SPIM e MARS)
![image](/Image/Aloca%C3%A7%C3%A3o%20de%20mem%C3%B3ria%20(SPIM%20e%20MARS).png)

### Política de Convenção de Uso dos Registradores
![image](/Image/Pol%C3%ADtica%20de%20Conven%C3%A7%C3%A3o%20de%20Uso%20dos%20Registradores.png)
