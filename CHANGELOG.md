# Changelog - JSVM (JavaScript Virtual Machine)

Todos os registros de mudanças notáveis neste projeto serão documentados neste arquivo.

O formato é baseado no [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), e este projeto segue o [Versionamento Semântico](https://semver.org/lang/pt-BR/). 
*Nota de Arquitetura:* Mudanças na tabela de Opcodes (alteração de valores hexadecimais de instruções existentes) sempre resultarão em uma mudança de versão MAIOR (Major), pois quebram a retrocompatibilidade dos binários `.jsvmfile` já compilados.

---

## [0.2.0] - 2026-05-30
Esta versão marca a transição da JSVM de um "simulador de array em memória" para um **Runtime de Infraestrutura Real**, com isolamento de processos e persistência em disco.

### Adicionado
- **Gerenciamento de Instâncias (Host Layer):**
  - Implementação do isolamento de processos usando `child_process`. Cada comando `jsvm create <nome>` agora gera uma thread separada no sistema operacional host (Node.js).
  - Criação da estrutura de diretórios reais em `/opt/jsvm/instances/` para armazenamento persistente do estado de cada VM.
  - O Heap agora é mapeado fisicamente para o arquivo `memory.bin` dentro do diretório da instância correspondente, permitindo dumps de memória reais.
- **Integração de Repositório e CLI:**
  - Adicionado comando `jsvm update-repo` que altera o endpoint central de pacotes. O repositório padrão agora aponta para `https://raw.githubusercontent.com/x11lang/javascriptvirtualmachine-repo/main`.
  - Adicionado comando `jsvm install <pacote>` que realiza o download assíncrono de arquivos `.jsvmfile` via HTTPS e os salva em `/opt/jsvm/packages/`.
  - Adicionado comando `jsvm list-all` que escaneia o sistema de arquivos e formata uma tabela interativa mostrando status (RUNNING/STOPPED) e tamanho do Heap.
- **Sistema de API (System Calls):**
  - Introduzida a `JSVM-API` interna para expor funcionalidades do host para o bytecode sem comprometer a segurança.
  - Novas interrupções de hardware simuladas: `SYS_PRINT` (IO Básico) e `SYS_TIME` (Relógio de Sistema).
- **Documentação e Governança:**
  - Adicionado o `CODE_OF_CONDUCT.md` baseado no Contributor Covenant v2.1.
  - Adicionado o `CONTRIBUTING.md` especificando fluxos de pull request para modificações no Core.
  - Adicionado o `EULA.md` e aplicada a **Apache License 2.0** no repositório.

### Mudado
- **CLI REPL:** O terminal interativo `[root@localhost $:/] #` foi refatorado. Agora ele atua como um gerenciador de host (Daemon) em vez de rodar a máquina virtual no mesmo loop de eventos.
- **Alocação de Memória:** Substituído o uso de arrays padrão do JavaScript por `SharedArrayBuffer` e `Uint8Array` contíguos no motor para aumentar a performance em operações de leitura/escrita diretas.

---

## [0.1.0] - 2026-05-15
Primeira versão com suporte a arquivos binários e estruturação da arquitetura de CPU Virtual.

### Adicionado
- **Formato Executável:**
  - Definição do formato oficial `.jsvmfile`.
  - Adicionado validador de cabeçalho: O arquivo deve começar obrigatoriamente com o *Magic Number* (4 bytes em UTF-8) igual a `JSVM`.
  - Adicionada leitura de *Entry Point* (4 bytes seguintes), determinando onde o Program Counter (`PC`) deve iniciar.
- **Core Interpreter (Opcodes Base):**
  - Tabela de instruções iniciais implementada (Hex mapping).
  - `0x01` -> `PUSH`: Empilha um valor na Operand Stack.
  - `0x02` -> `POP`: Remove o valor do topo da pilha.
  - `0x10` -> `ADD`: Desempilha dois valores, soma e empilha o resultado.
  - `0x11` -> `SUB`: Desempilha dois valores, subtrai e empilha o resultado.
  - `0x20` -> `STORE`: Armazena o valor do topo da pilha em um registrador local.
  - `0x21` -> `LOAD`: Carrega o valor de um registrador local para a pilha.
- **Ferramentas de Debug:**
  - Adicionado comando interativo `DUMP` no REPL, que exibe os registradores atuais (`PC`, `SP`) e o estado bruto da pilha.

### Corrigido
- Falha de estouro de pilha (Stack Overflow) quando o comando `PUSH` era executado mais de 10.000 vezes sequencialmente em loop. Limite imposto via validação no motor.

---

## [0.0.1] - 2026-05-01
Prova de conceito inicial.

### Adicionado
- Estrutura básica da classe `JSVM` em JavaScript.
- Loop de ciclo de máquina (`while(pc < bytecode.length)`).
- Pilha lógica (baseada em `Array.prototype.push/pop`).
- Suporte a execução linha-a-linha de strings de texto simulando Assembly.
