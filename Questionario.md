# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
>> Compilação cruzada é o processo de compilar código-fonte em uma plataforma diferente daquela em que o código será executado. É frequentemente usado para desenvolver software em sistemas embarcados ou plataformas com arquiteturas distintas, permitindo que os desenvolvedores gerem código executável para o ambiente de destino sem a necessidade de compilá-lo lá.

## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
>>O código de inicialização, também chamado de "startup code", é um conjunto de instruções de baixo nível executado no início de um programa ou sistema embarcado. Sua finalidade é configurar o ambiente de execução, inicializar dispositivos de hardware e, eventualmente, chamar a função principal do programa, preparando o sistema para a execução do código do usuário.

## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.
>>Um Makefile é um arquivo de configuração usado pelo utilitário make para automatizar a compilação de programas. Ele contém instruções sobre como construir um programa a partir de vários arquivos-fonte, definindo dependências e regras de compilação.

#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.
>>O utilitário make examina as datas de modificação dos arquivos-fonte e objetos para determinar quais partes do projeto precisam ser recompiladas. Ele executa comandos no Makefile para compilar apenas os arquivos que foram modificados, otimizando o processo de compilação.

#### (c) Qual é a sintaxe utilizada para criar um novo **target**?
>>nome_do_target: dependências
    comandos


#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?
>>Dependências de um target são listadas após seu nome, indicando arquivos ou outros targets necessários para a construção. O make utiliza essas dependências para determinar a ordem de execução e identificar o que precisa ser recompilado com base nas modificações.

#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
>>Regras do Makefile são instruções que indicam como construir os targets. Existem regras implícitas, padrões pré-definidos, e regras explícitas, definidas pelo usuário. As regras incluem comandos que o make executa para construir o target, facilitando a automação do processo de compilação

## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?
>>O conjunto de instruções Thumb, uma extensão da arquitetura ARM, emprega instruções de 16 bits, reduzindo o espaço de memória necessário. Sua vantagem principal é a eficiência no uso de memória, crucial em sistemas com limitações de espaço. O Thumb opera em conjunto com o conjunto de instruções ARM, permitindo a seleção entre os dois conjuntos conforme a necessidade durante a execução.

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.
>>Na arquitetura Load/Store, apenas instruções de carga e armazenamento acessam a memória, enquanto operações aritméticas ocorrem apenas em registradores. Já na Register/Register, instruções de carga e armazenamento também operam diretamente entre registradores, sem necessidade de acesso à memória para operações entre registradores.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.
>>Os processadores ARM Cortex-M oferecem dois níveis de acesso (Privileged e Unprivileged) e dois modos de operação (Thread e Handler). O modo Thread é para execução normal, enquanto o modo Handler lida com exceções. Os níveis de acesso controlam o acesso a recursos e instruções privilegiadas.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.
>>Exceções e interrupções em processadores ARM são tratadas por meio de um vetor de interrupção, priorizando exceções. O mecanismo de group priority e sub-priority permite uma priorização mais detalhada, crucial em ambientes multitarefa.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?
>> O CPSR (Current Program Status Register) mantém o estado atual do processador, enquanto o SPSR (Saved Program Status Register) temporariamente armazena o CPSR durante exceções, restaurando-o no retorno à execução normal.

### (f) Qual a finalidade do **LR** (***Link Register***)?
>>O Link Register (LR) armazena o endereço de retorno para chamadas de função, sendo atualizado automaticamente para garantir um retorno adequado após a execução da função.

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?
>>O Program Status Register (PSR) em processadores ARM contém informações sobre o estado do processador, controlando o fluxo de execução e gerenciando exceções.

### (h) O que é a tabela de vetores de interrupção?
>>A tabela de vetores de interrupção é uma área de memória contendo os endereços dos tratadores de interrupção, permitindo ao processador encontrar o tratador associado a uma interrupção específica.

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?
>>O NVIC gerencia interrupções em processadores ARM Cortex-M, suportando alta prioridade e aninhamento de interrupções para uma resposta eficiente a eventos assíncronos.

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 
>>Durante uma exceção, o Cortex-M armazena o valor do Program Counter (PC) no registrador LR, facilitando o retorno à posição original do código após a conclusão da rotina de exceção.

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 
>>No Cortex-M3, o salvamento de contexto usa a pilha principal, enquanto no Cortex-M4F, com ponto flutuante, é necessário salvar registradores adicionais, aumentando o tempo de salvamento. O conceito de lazy stack adia o salvamento de alguns registradores, otimizando tempo e espaço na pilha conforme necessário e é configurado para otimizar o desempenho.

## Referências

### Básicas

[1] [STM32F411xC Datasheet](https://www.st.com/resource/en/datasheet/stm32f411ce.pdf)

[2] [RM0383 Reference Manual](https://www.st.com/resource/en/reference_manual/rm0383-stm32f411xce-advanced-armbased-32bit-mcus-stmicroelectronics.pdf)

[3] [Using the GNU Compiler Collection (GCC)](https://gcc.gnu.org/onlinedocs/gcc/index.html)

[4] [GNU Make](https://www.gnu.org/software/make/manual/html_node/index.html)

### Vídeos Microsoft Teams

[5] [05 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[6] [06 - Arquitetura Cortex-M Parte 1/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[7] [07 - Arquitetura Cortex-M Parte 2/2](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[8] [08 - Microcontroladores STM32](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

[9] [10 - Introdução à arquitetura de computadores](https://web.microsoftstream.com/embed/channel/f6b3a0de-e6f3-4652-b2d5-f1164032498a?app=microsoftteams&sort=undefined&l=pt-br#)

### Material Suplementar

[5] [A General Overview of What Happens Before main()](https://embeddedartistry.com/blog/2019/04/08/a-general-overview-of-what-happens-before-main/)
 
[6] [Bare metal embedded lecture-1: Build process](https://youtu.be/qWqlkCLmZoE?si=mn5yDnJYudQ1PpZH)
 
[7] [Bare metal embedded lecture-2: Makefile and analyzing relocatable obj file](https://youtu.be/Bsq6P1B8JqI?si=yuNLPj3JQ-2IT1yo)
 
[8] [Bare metal embedded lecture-3: Writing MCU startup file from scratch](https://youtu.be/2Hm8eEHsgls?si=c27MpZ47ApiMSwHR)
 
[9] [Lecture 15: Booting Process](https://youtu.be/3brOzLJmeek?si=MsHRUEJP8zofjwJQ)
