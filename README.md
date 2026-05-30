# JSVM (JavaScript Virtual Machine)

O **JSVM** é um ambiente de execução de bytecode de baixo nível construído sobre o Node.js. Diferente de simuladores comuns, o JSVM foca em uma arquitetura real de máquina virtual, com gerenciamento de memória persistente, sistema de pacotes, e suporte a arquivos binários executáveis (`.jsvmfile`).

## Arquitetura
O sistema opera em três camadas principais:
1. **Host Layer:** O ambiente Node.js que gerencia o ciclo de vida dos processos.
2. **Virtual Hardware:** Emulação de memória (Heap), registradores e pilha (Stack).
3. **Repository System:** Integração com [x11lang/javascriptvirtualmachine-repo](https://github.com/x11lang/javascriptvirtualmachine-repo) para distribuição de pacotes.



## Comandos Principais
A interface de linha de comando permite o gerenciamento total das instâncias:

* `jsvm create [nome] [memoria]` - Cria uma nova instância de VM com heap dedicado.
* `jsvm install [pacote]` - Baixa e instala um `.jsvmfile` do repositório oficial.
* `jsvm run [arquivo]` - Executa o bytecode de um arquivo `.jsvmfile`.
* `jsvm list-all` - Lista instâncias e pacotes instalados.
* `jsvm update-repo [url]` - Altera o endpoint do repositório de pacotes.

## Formato .jsvmfile
O arquivo `.jsvmfile` é um formato binário compacto que armazena:
* **Magic Header:** `JSVM`
* **Entry Point:** Endereço inicial de execução.
* **Bytecode:** Instruções binárias processadas diretamente pelo interpretador.

## Instalação
```bash
git clone [https://github.com/seu-usuario/seu-projeto-jsvm](https://github.com/seu-usuario/seu-projeto-jsvm)
cd seu-projeto-jsvm
npm install
node cli.js
