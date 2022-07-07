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

Formato de instrução Tipo-J: Ex.: j 1200

![image](/Image/Controle%20de%20Fluxo.png)

Desvio Condicional:

        bne $t0, $t1, Label     # Branch if Not Equal: $t0 != $t1       ?       PC=Label
        beq $t0, $t1, Label     # Branch if Equal: $t0 == $t1   ?       PC=Label

![image](/Image/Comp%20C%20e%20Assembly.png)

### Comparações

No MIPS, são implementadas as comparações:

        == e != 
        
Como implementar:

        <,>,<=,>=?
        
Instrução MIPS: Set on Less Than

         slt $t0,$t1,$t2        # $t0=1 se $t1<$t2;    $t0=0 caso contrário;
         slti $t0,$t1,Imm     # $t0=1  se $t1<Imm; $t0=0 caso contrário;
         Apenas com estas instruções podemos montar várias estruturas de controle;
         Ao montador, é reservado o registrador $1 ($at) para essa tarefa.

Exemplo:

        Construa a pseudo-instrução Branch If Less Than: blt $t0,$t1,Label 
        slt $at, $t0, $t1
        bne $at, $zero, Label

### Constantes

Constantes pequenas são usadas muito frequentemente (50% dos operandos).

        A = A + 5;
        B = B + 1;
        C = C - 18;

Como tratar constantes no MIPS?
* Coloque constantes típicas na memória e carregue-as.
* Crie registradores hardwired (como $zero) para constantes como um (1).

Instruções com imediato MIPS:

add $29, $29, 4
slti $8, $18, 10
andi $29, $29, 6
ori $29, $29, 4;

### Princípio de Projeto

Agilizar o caso mais comum!

### Constantes (maiores)

Para carregar uma constante de 32 bits num registrador são necessárias duas instruções. Nova instrução: load upper immediate

![image](/Image/Const.%20Maiores.png)

Carga dos bits menos significativos...

![image](/Image/Ori.png)

### Linguagem Assembly vs. Linguagem de Máquina

O assembly fornece uma representação simbólica conveniente
* muito mais fácil do que escrever números binários;
* por exemplo, destino primeiro;
* Pode-se usar Labels em vez de endereços numéricos;
A linguagem de máquina é realidade subjacente
* Por exemplo, o destino não é mais o primeiro;
* Labels são convertidos em números apropriados;
O assembly pode fornecer "pseudo-instruções"
* por exemplo, move $t0, $t1 existe apenas no assembly;
* pode ser implementada usando add $t0, $t1, $zero
Ao considerar o desempenho, você deve contar as instruções reais

### Resumo
Instruções simples, todas de 32 bits

Bastante estruturada

Somente três formatos de instruções

![image](/Image/Resumo%20Mod%207.png)

Contar com o compilador para obter desempenho

Auxiliar o compilador onde for possível

### Endereços (do Contador de Programa PC) em desvios

Instruções

        bne $t4, $t5, Label     # Próxima instrução em Label se $t4 != $t5
        beq $t4, $t5, Label     # Próxima instrução em Label se $t4 == $t5
        j Label # Próxima instrução em Label
        jal Label # $ra=PC+4; Próxima Instrução em Label 

Formatos

![image](/Image/Formatos.png)

### Linguagem Assembly vs. Linguagem de Máquina

Pode-se especificar um registrador (como lw e sw) e adicioná-lo ao endereço (Endereço Relativo)
* Utilizar Instruction Address Register (PC = program counter);
* Maioria dos descios são locais (Princípio da Localidade);
Instruções tipo-J, j e jal, utilizam os 4bits de alta ordem do PC e concatenam ao endereço do (Label (26)<<2)(28) totalizando os 32 bits:
* limites de endereço de 256 MB (64M instruções).
* O montador e o linker precisam cuidar diso!

### Endereços (do Contador de Programa PC) em desvios

![image](/Image/End%20em%20desvios.png)

Exemplo: 
        
        while(save[i]==k) i++;

* MIPS: Possuem endereços em bytes, diferenciando em 4 bytes (word);
* A instrução bne acrescenta 2 words (8 bytes) na instrução seguinte, especificando o endereço de descio (8 + 80016) e não em relação à instrução atual (12 + 80012), ou ao endereço completo/absoluto (80024).
* O jump utiliza o endereço completo (2000 x 4 = 80000)
![image](/Image/End%20em%20desvios%20Ex.png)

