# Linguagem de montagem: MIPS

![image](https://user-images.githubusercontent.com/85000470/175837431-d3f81440-5c38-470d-8560-17871a994d80.png)

### Objetivo

Apresentar e construir a arquitetura do processador RISC MIPS R2000/3000 e exemplo de programação Assembly

Por que Assembly para MIPS (Microprocessor Without Interlocked Pipeline Stages)?
* Linguagem excelente para fins did ́aticos (extensamente coberta no livro-texto).
* Linguagem similar a ARMv7.  Mais de 9 bilh ̃oes de chips com processadores ARM foram produzidos em2011, o que tornou o conjunto de instruções mais popular do mundo!
* Ajudará no entendimento da linguagem de montagem para Intel x86, que controla a operação de dispositivos PC e da nuvem de dispositivos da era pós-PC.

### Arquitetura MIPS

Baseado na arquitetura RISC (Reduced Instruction Set Computer):  Computador com conjunto de instruções reduzidas.

### Arquitetura dos processadores MIPS R2000/R3000

Um processador MIPS consiste em uma unidade processadora de inteiros (CPU) e uma coleção de co-processadores que executam tarefas auxiliares ou operam sobre outros tipos de dados como números em ponto flutuante.
* O co-processador 0 gerencia traps (desvios e/ou chamadas de sistema), exce ̧c ̃oes e o sistema de memória virtual.
* O co-processador 1 é a unidade de ponto flutuante (FPU).
* A CPU MIPS contém 32 registradores de uso geral numerados de 0 a 31.  O registrador n  ́e designado por $n.

![image](https://user-images.githubusercontent.com/85000470/175838236-bd57b8a9-2567-4560-9832-5da228b441a8.png)

Alguns conceitos e boas práticas:
* O registrador$0 ($zero) cont ́em sempre o valor 0 (hardwired).
* Os registradores $1 ($at), $26 ($k0) e $27 ($k1) são reservados para uso do montador e sistema operacional.
* Os registradores $2 e$3 ($v0,$v1) são utilizados para retornar valores de funções.
* O registrador $28 ($gp) é um ponteiro global que aponta para o meio de um bloco de memória de 64K, nosegmento de dados estáticos.
* O registrador$29 ($sp) é o ponteiro de pilha, apontando sempre para o primeiro elemento da pilha.
* O registrador$30 ($fp) é o ponteiro de frame.  
* Pode ser utilizado como registrador callee-saved $s8.
* O registrador $31 ($ra) armazena o endereço de retorno quando é executada a instrução jal. (jal= instrução de jump to subroutine label);

![image](https://user-images.githubusercontent.com/85000470/175839858-d6bf26ec-1918-4f6e-a903-ee5efd1e0491.png)

### Organização da Memória

* Vista como um grande array unidimensional, com endere ̧cos sequenciais.
* Um endereço de memória ́e um índice no array.
* “Byte addressing” significa que o índice aponta para um byte na memória.

![image](https://user-images.githubusercontent.com/85000470/175840025-6e2c74db-ac10-453b-95ab-adc0ee3ff7b5.png)

* Bytes são práticos, porém a maioria dos dados utiliza “words”: unidade básica de referenciamento a memória. Definida pela arquitetura.
* Para MIPS, uma word tem 32 bits ou 4 bytes.
* Registradores armazenam 32 bits.

![image](https://user-images.githubusercontent.com/85000470/175840287-059169a8-41cb-463f-8394-b81dc7a89acb.png)

* Com 32 bits, ́e possível indexar 2^32 bytes com endereços de byte de 0 a (2^32−1).
* Ou, 2^30 words com endereços de byte de 0,4,8, ...(2^30−4).
* Words são alinhadas (Restrição de Alinhamento).  Quais são os valores dos 2 bits menos significativos do endereço de uma word?

![image](https://user-images.githubusercontent.com/85000470/175840440-5096a8a4-c8c1-4f7d-a600-d6a88adc9e79.png)

### Ordenamento dos Bytes

* Processadores MIPS podem operar tanto no esquema big-endian:  (IBM 360/370, Motorola 68k, MIPS,Sparc, HP PA)

![image](https://user-images.githubusercontent.com/85000470/175840775-9144989d-3e62-4e6f-8485-47d4662e3b85.png)

* quanto little-endian:  (Intel 80x86, MIPS, DEC Vax, DEC Alpha)

![image](https://user-images.githubusercontent.com/85000470/175840790-b11696f5-7fa8-420a-8df3-7d2fcda45d02.png)

### Modos de endereçamento

* MIPS  ́e uma arquitetura load/store, isto  ́e somente instruções load e store têm acesso á memória.
* As instruções da ULA operam somente com valores em registradores.
* A máquina básica provê unicamente o modo de endereçamento imm (register) que utiliza como endereçamento a soma de um inteiro imediato e o conteúdo de um registrador.

![image](https://user-images.githubusercontent.com/85000470/175840964-dbdb53a1-ff9c-4d30-b4e7-264faab5cdf4.png)

Operandos constantes ou Imediatos:
* E recorrente a necessidade de se usar uma constante em uma operação.
* Simplicidade arquitetural:  evitar a carga da constante na memória para posterior transferência da mesma antes para um registrador antes de seu uso.

*Commom case fast!*

* A arquitetura provê instruções que operam diretamente com constantes (imediatos).

### Formato de instruções

![image](https://user-images.githubusercontent.com/85000470/175841231-f52820ad-65d7-4f18-908f-094826c81340.png)

![image](https://user-images.githubusercontent.com/85000470/175841244-a631fafc-979a-4d7a-931c-808d45f354fb.png)

### Estruturas Básicas de um programa

Duas  ́areas distintas: .text e .data
* .text: área do programa (instruções) em si;
* .data: ́area para declarações de variáveis estáticas;
* Áreas Independentes da ordem:  Montador responsável pela colocação

*.globl:  Declaração para rótulos globais*

### Instruções

Linguagem da Máquina (de Montagem)
* Mais primitiva que linguagens de alto nível. Sem controle de fluxo sofisticado.
* Muito restritiva: MIPS Arithmetic Instructions.

![image](https://user-images.githubusercontent.com/85000470/175841534-ef2613b3-0144-4bd7-85fc-47472fa4f7d1.png)


### Instruções (Abstrações)

Modelo de programação: MIPS ISA (Instruction Set Architecture)
* Similar a outras arquiteturas desenvolvidas desde os anos 80.
Objetivos de projeto:
* Maximizar o desempenho;
* Minimizar o custo 
* E reduzir o tempo de projeto.

![image](https://user-images.githubusercontent.com/85000470/175841636-664d5b64-bb98-4cee-b58f-d7a0dd9dc0b6.png)

### Aritmética MIPS

* Todas as instruções possuem 3 operandos
* A ordem dos operandos é fixa.
Exemplo:
* código C:A=B+C;
* código MIPS: add $s0, $s1, $s2(associado as variáveis pelo compilador).

![image](https://user-images.githubusercontent.com/85000470/175841765-8f167429-cc7b-42b5-9549-a050aa5f8a7b.png)

* Operandos devem ser registradores.
* 32 registradores disponíveis.

![image](https://user-images.githubusercontent.com/85000470/175841827-261d1f56-be25-4d28-8f09-c8f7a0dc6a48.png)

### Registradores vs.  Memória

* Operandos de instru ções aritméticas devem ser registradores (32 registradores disponíveis).
* Compilador associa variáveis a registradores.
* E programas com várias variáveis, arrays, structs,...?

![image](https://user-images.githubusercontent.com/85000470/175841931-b8658399-c5e8-4aac-95a2-84b4ac1ed76c.png)

### Manipulação de memória MIPS

![image](https://user-images.githubusercontent.com/85000470/175842590-25516e0f-a1b4-47e4-8067-db5259b824fb.png)

![image](https://user-images.githubusercontent.com/85000470/175842617-383419ce-8cf5-4e47-9827-6717e42666db.png)

![image](https://user-images.githubusercontent.com/85000470/175842628-1e61b278-e755-4d69-a37a-d37d35b7d20f.png)

![image](https://user-images.githubusercontent.com/85000470/175842652-5ef61d03-e75f-49a0-ba6e-fb33867b0d6b.png)

![image](https://user-images.githubusercontent.com/85000470/175842680-095649cb-6a3a-4b83-95ae-5b090da6f922.png)
