# Linguagem de Montagem: MARS e Arquitetura x86 (IA-32)

### Simuladores SPIM/MARS: chamadas de sistemas
Implementa o montador, pseudo-instruções, simula um sistema operacional com fnções de Entrada/Saída em console próprio.

Exemplo:

    Aplicação que escreve na tela: the answer = 5

![imagem](/Image/Escreve%20the%20answer.png)

![image](/Image/Chamadas%20de%20sistemas.png)

Exemplo:  clear (ponteiro vs.  array)

![image](https://user-images.githubusercontent.com/85000470/178120110-9aaff6eb-4449-4ecd-be8b-e988424bb941.png)

Exemplo: SORT

![image](https://user-images.githubusercontent.com/85000470/178120114-976091a8-a4c4-46d2-9eca-dba117c1bdc6.png)

![image](https://user-images.githubusercontent.com/85000470/178120123-38dd402d-52d8-472e-9204-01b0b42b7338.png)

### Arquiteturas alternativas
Alternativa de projeto:
* Forneça operações mais poderosas;
* O Objetivo é reduzir o número de instruções executadas;
* O risco é um tempo de ciclo mais lento e/ou uma CPI mais alta.

Vejamos o IA-32

### IA-32
Linha temporal:
* 1978: O Intel 8086  ́e anunciado (arquitetura de 16 bits);
* 1980: O co-processador de ponto flutuante Intel 8087 ́e acrescentado;
* 1982: O 80286 aumenta o espaço de endereçamento para 24 bits; disponibiliza mais instruções;
* 1985: O 80386 estende para 32 bits; novos modos de endereçamento;
* 1989-1995: O 80486, Pentium e Pentium Pro acrescentam algumas instruções (especialmente projetadas para um maior desempenho);
* 1997:  57 novas instruções MMX (SIMD) são acrescentadas; Pentium II;
* 1999: O Pentium III acrescenta outras 70 instruções (SSE — Streaming SIMD Extensions): reação aos concorrentes(ADM 3DNow).
* 2001: Outras 144 instruções (SSE2)
* 2003: A AMD estende a arquitetura para aumentar o espaço de endereço para 64 bits; estende todos os registradorespara 64 bits, além de outras mudanças (AMD64)
* 2004: A Intel se rende e abraça o AMD64 (o chama EM64T) e inclui mais extensões de mídia. Essa história ilustra o impacto das “algemas douradas” da compatibilidade “adicionando novos recursos da mesma forma que se colocaroupas em uma sacola”, uma arquitetura “difícil de explicar e impossível de amar”.
* 2006: SSE4 adiciona 54 instruções!  Suporte especial a máquinas virtuais.
* 2007: AMD anuncia 170 instruções do conjunto SSE5
* 2011: Intel anuncia Advanced Vector Extension: registradores SSE evoluem de 128 bits para 256 bits, redefinição de 250 instruções e adição de 128 instruções.

### Visão geral do IA-32
Complexidade:
* Instruções de 1 a 17 butes (136 bits) de tamanho;
* Um operando precisa agir como origem e destino;
* Um operando pode vir da memória;
* Modos de endereçamento complexos, por exemplo, "índice ase ou escalado com deslocamento de 8 ou 32 bits"

### Registradores e endereçamento de dados do IA-32
Registradores no subconjunto de 32 bits que surgiram com o 80386

![image](/Image/Registradores%20e%20endere%C3%A7amento%20de%20dados%20do%20IA-32.png)

### Restrições de registrador do IA-32
Não são viáveis operações memória-memória.

Imediatos podem ser de 8, 16 ou 32 bits. Qualquer um dos registradores (exceto EIP e EFLAGS) se enquadram nas combinações.

![image](/Image/Memoria-Memoria.png)

![image](/Image/Restri%C3%A7%C3%A3o%20IA-32.png)

### Instruções típicas do IA-32
Quatro tipos principais de instruções de inteiro:
* Movimento de dados, incluindo move, push, pop
* Aritmética e lógica (registrador de destino ou memória)
* Fluxo de controle (uso de códigos de condição/flags)
* Instruções de string, incluindo movimento e comparação de strings.

![image](/Image/Inst%20tip.png)

P.S.: call salva EIP da próxima instrução na pilha/stack. EIP ́e o PC da Intel.

### Formatos de instruções do IA-32
Formatos típicos:

![image](/Image/Formato%20inst%20IA32.png)

### Restrições de registrador do IA-32
![image](/Image/Restri%C3%A7%C3%A3o%201.png)

![image](/Image/Restri%C3%A7%C3%A3o%202.png)

### Resumo
A complexidade da instrução é apenas uma variável
* Instrução mais simples versus CPI mais alta / velocidade de clock mais baixa

Princípios de projeto:
* simplicidade favorece a regularidade;
* menor é melhor;
* bom projeto exige comprometimento
* agilizar o caso comum

Arquitetura do conjunto de instruções: uma abstração muito importante!

