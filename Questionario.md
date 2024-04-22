# Questionário Sistemas Embarcados I

## 1. Explique brevemente o que é compilação cruzada (***cross-compiling***) e para que ela serve.
Compilação cruzada refere-se à prática de compilar um programa em um ambiente de desenvolvimento diferente daquele em que será executado. É útil quando se deseja desenvolver e testar software em uma plataforma mais poderosa antes de implantá-lo em uma plataforma mais restrita, como dispositivos embarcados ou sistemas heterogêneos.

## 2. O que é um código de inicialização ou ***startup*** e qual sua finalidade?
O código de inicialização, ou startup code, é um conjunto de instruções fundamentais que são executadas quando um sistema é ligado ou um programa é iniciado. Ele tem como objetivo preparar o ambiente de execução para o software principal, realizando tarefas como configuração de hardware, inicialização de variáveis e alocação de memória. Esse código é crucial, especialmente em sistemas embarcados, pois garante que o hardware seja configurado corretamente antes de iniciar o sistema operacional ou o aplicativo principal.

## 3. Sobre o utilitário **make** e o arquivo **Makefile responda**:

#### (a) Explique com suas palavras o que é e para que serve o **Makefile**.

#### (b) Descreva brevemente o processo realizado pelo utilitário **make** para compilar um programa.

#### (c) Qual é a sintaxe utilizada para criar um novo **target**?

#### (d) Como são definidas as dependências de um **target**, para que elas são utilizadas?

#### (e) O que são as regras do **Makefile**, qual a diferença entre regras implícitas e explícitas?
(a) Um arquivo Makefile é um documento que contém instruções para o utilitário Make, usado para automatizar a compilação de programas ou projetos. Ele oferece orientações sobre como compilar, vincular e executar diferentes partes de um programa, além de definir as relações de dependência entre os arquivos.

(b) O processo executado pelo utilitário Make envolve a verificação das datas de modificação dos arquivos fonte e de seus objetos compilados associados. Sempre que um arquivo fonte é alterado ou suas dependências mudam, o Make recompila os arquivos pertinentes, seguindo as instruções fornecidas no Makefile.

(c) Para criar um novo target em um Makefile, utiliza-se a seguinte sintaxe:

makefile
Copy code
nome_do_target: dependências
    comando
(d) As dependências de um target são especificadas logo abaixo dele no Makefile. Elas indicam quais arquivos ou targets precisam ser atualizados antes que o target em questão possa ser construído. O Make usa essas dependências para determinar se o target precisa ser recompilado ou não.

(e) As regras no Makefile são as instruções que orientam como os targets devem ser construídos. Existem dois tipos de regras: implícitas, que são predefinidas pelo Make para compilar certos tipos de arquivos, e explícitas, que são definidas pelo usuário no Makefile para compilar ou realizar outras tarefas específicas.


## 4. Sobre a arquitetura **ARM Cortex-M** responda:

### (a) Explique o conjunto de instruções ***Thumb*** e suas principais vantagens na arquitetura ARM. Como o conjunto de instruções ***Thumb*** opera em conjunto com o conjunto de instruções ARM?

### (b) Explique as diferenças entre as arquiteturas ***ARM Load/Store*** e ***Register/Register***.

### (c) Os processadores **ARM Cortex-M** oferecem diversos recursos que podem ser explorados por sistemas baseados em **RTOS** (***Real Time Operating Systems***). Por exemplo, a separação da execução do código em níveis de acesso e diferentes modos de operação. Explique detalhadamente como funciona os níveis de acesso de execução de código e os modos de operação nos processadores **ARM Cortex-M**.

### (d) Explique como os processadores ARM tratam as exceções e as interrupções. Quais são os diferentes tipos de exceção e como elas são priorizadas? Descreva a estratégia de **group priority** e **sub-priority** presente nesse processo.

### (e) Qual a diferença entre os registradores **CPSR** (***Current Program Status Register***) e **SPSR** (***Saved Program Status Register***)?

### (f) Qual a finalidade do **LR** (***Link Register***)?

### (g) Qual o propósito do Program Status Register (PSR) nos processadores ARM?

### (h) O que é a tabela de vetores de interrupção?

### (i) Qual a finalidade do NVIC (**Nested Vectored Interrupt Controller**) nos microcontroladores ARM e como ele pode ser utilizado em aplicações de tempo real?

### (j) Em modo de execução normal, o Cortex-M pode fazer uma chamada de função usando a instrução **BL**, que muda o **PC** para o endereço de destino e salva o ponto de execução atual no registador **LR**. Ao final da função, é possível recuperar esse contexto usando uma instrução **BX LR**, por exemplo, que atualiza o **PC** para o ponto anterior. No entanto, quando acontece uma interrupção, o **LR** é preenchido com um valor completamente  diferente,  chamado  de  **EXC_RETURN**.  Explique  o  funcionamento  desse  mecanismo  e especifique como o **Cortex-M** consegue fazer o retorno da interrupção. 

### (k) Qual  a  diferença  no  salvamento  de  contexto,  durante  a  chegada  de  uma  interrupção,  entre  os processadores Cortex-M3 e Cortex M4F (com ponto flutuante)? Descreva em termos de tempo e também de uso da pilha. Explique também o que é ***lazy stack*** e como ele é configurado. 

(a) O conjunto de instruções Thumb é uma extensão do conjunto ARM, focada em reduzir o tamanho do código e melhorar o desempenho em sistemas com cache limitado. Ele opera em conjunto com as instruções ARM, permitindo que o processador execute ambas as instruções conforme necessário.

(b) As arquiteturas ARM Load/Store e Register/Register referem-se a diferentes métodos de acesso à memória. Na Load/Store, as operações de memória são realizadas explicitamente por instruções separadas, enquanto na Register/Register algumas operações podem ser feitas diretamente entre registradores.

(c) Nos processadores ARM Cortex-M, o acesso e os modos de operação são gerenciados pelo SCB e CTRL. Os níveis de acesso incluem Privilegiado, Não-privilegiado e Thread Mode, enquanto os modos de operação incluem Handler Mode e Thread Mode, cada um com suas próprias permissões e restrições.

(d) As exceções e interrupções são tratadas pelos processadores ARM com base em prioridades, usando group priority e sub-priority para gerenciar a ordem de execução das exceções.

(e) O CPSR armazena o estado atual do processador, enquanto o SPSR é usado para armazenar o estado durante exceções, permitindo a retomada após a conclusão da exceção.

(f) O LR armazena o endereço de retorno após uma chamada de função, permitindo que o programa retorne ao ponto de execução anterior.

(g) O PSR armazena informações sobre o estado do processador, incluindo flags de condição e modo de execução.

(h) A tabela de vetores de interrupção contém os endereços das rotinas de tratamento de interrupção, consultadas pelo processador quando uma interrupção ocorre.

(i) O NVIC gerencia interrupções e exceções, fornecendo suporte para interrupções de prioridade variável em tempo real.

(j) O Cortex-M salva o valor atual do LR no SPSR antes de iniciar a execução da rotina de tratamento de interrupção, usando o EXC_RETURN para determinar como a execução deve ser retomada após a conclusão da interrupção.

(k) A diferença no salvamento de contexto entre os processadores Cortex-M3 e Cortex-M4F durante interrupções é principalmente devido à capacidade do Cortex-M4F de lidar com instruções de ponto flutuante. Ele pode salvar e restaurar automaticamente o estado do registrador de ponto flutuante, resultando em economia de tempo e espaço na pilha. O "lazy stack" é configurado no NVIC, adiando o salvamento de alguns registradores até que seja necessário, reduzindo a sobrecarga.


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
