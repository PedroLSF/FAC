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
**Q**




