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

Exemplo: add $t0, $s1, $s2

* registradores são identificados por seus números(vide tabelas): $t0=8, $s1=17, $s2=18

Formato de Instrução Tipo-R (add: op=0 funct=32)

![image](/Image/Exemplo%20formato%20de%20instru%C3%A7%C3%B5es.png)

O que acontece quando uma instrução necessita de campos maiores?
* Deve-se usar o imediato

addi $t0, $t1, Imm
lw $t0, Imm($t1)

![image](/Image/Formato%20de%20Instru%C3%A7%C3%B5es%20compromisso.png)

