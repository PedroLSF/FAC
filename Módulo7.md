# Linguagem de Montagem II: MIPS

Programas são armazenados na memória para serem lidos da mesma forma que os dados.

### Programa armazenado

Ciclos de busca e execução:
* Instruções são buscadas e colocadas num registrador especial (IR: Instruction Register);
* Bits neste registrador "controlam" as ações subsequentes necessárias a execução da instrução;
* Busca a próxima instrução e continua...

### Formato de Instruções MIPS

Instruções, assim como registradores e words de dados, também têm 32 bits de comprimento.

![imagem](/Image/Formato%20de%20Instru%C3%A7%C3%B5es.png)

Campos (fields):
* op: Operação básica da instrução: opcode
* rs: primeiro registrador de operando origem (source);
* rt: segundo registrador de operando origem (source);
* rd: registrador de operando destino:  resultado (destination);
* shamt: shift amount;
* funct: variação da operação: function code.

Exemplo: 

    add $t0, $s1, $s2

* registradores são identificados por seus números(vide tabelas): $t0=8, $s1=17, $s2=18

Formato de Instrução Tipo-R (add: op=0 funct=32)

![image](/Image/Exemplo%20formato%20de%20instru%C3%A7%C3%B5es.png)

O que acontece quando uma instrução necessita de campos maiores?
* Deve-se usar o imediato

addi $t0, $t1, Imm
lw $t0, Imm($t1)

![image](/Image/Formato%20de%20Instru%C3%A7%C3%B5es%20compromisso.png)

Novo tipo de formato de instrução para instruções com dados Imediatos.
* Exemplo:lw $t0, 32($s3)

O comprimento do quarto campo do Tipo-I ́e a soma dos comprimentos dos ́ultimos três campos do Tipo-R.

Formato de Instrução Tipo-I

![image](/Image/Formato%20de%20Instru%C3%A7%C3%A3o%20Tipo-I.png)

Compilação manual...

* Suponha que $t1 tenha o endereço base de A e que $s2 corresponda a h, traduza a seguinte linha em C para código de máquina MIPS:

        A[300] = h + A[300];

* Primeiro, temos que o código em assembly correspondente é:

        lw $t0 ,1200( $t1) # $t0 = A[300]
        add $t0 , $s2 , $t0 # $t0 = h + A[300]
        sw $t0 , 1200( $t1) # A[300] = h + A[300]

* Qual o código em linguagem de máquina destas 3 instruções?

![image](/Image/Corre%C3%A7%C3%A3o%20manual....png)

### Operações Lógicas

![iamge](/Image/Operadores.png)

NOT:
* Realizado utilizando o NOR.
* Utiliza-se o $zero (Hardwired) de preferência!
* Expressão Booleana:

                A NOR B = NOT (A OR B).

* Se B = 0:NOT (A OR 0) = NOT(A).

sll e srl (deslocamentos lógicos ou logical shifts)
* Instrução do Tipo-R.
* Utiliza o campo shamt (shift amount)
        
        Quantidade de Deslocamento (de acordo com a direção!)   
        
        Exemplo:
        sll $t2, $s0, 4 # $t2 = $s0 << 4 bits

![image](/Image/OP%20L%C3%B3gco%20SLL.png)

AND e OR:
* Mesma atribuição do AND e OR booleanos
* Realizados Bit-abit

        AND: Operação de "mascaramento" (ocultar bits) e "chave lógica".
        OR: "Junção de sinais lógicos"

MIPS: Existem os equivalentes paraANDeORcom Imediatos (ori e andi).

### Controle de Fluxo
* Registrador Especial de PC (Program Counter): indica qual o endereço da próxima instrução a ser buscada na memória
* Instruções MIPS

        jr   $t0       # Jump  Register:   PC=[$t0]             Obs.: Tipo-R!
        j Label       # Jump  Label: PC=Label
        jal  Label     # Jump  and  Link: $ra=PC+4; PC=Label