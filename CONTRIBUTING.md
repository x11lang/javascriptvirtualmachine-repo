# Como contribuir com a JSVM

Obrigado pelo seu interesse em contribuir com o ecossistema **JSVM**! Agradecemos toda ajuda, desde correções de bugs até novas instruções de opcode ou melhorias no sistema de pacotes.

## 1. Primeiros Passos
* Leia o nosso [Código de Conduta](CODE_OF_CONDUCT.md).
* Verifique se o seu problema já não foi relatado nas [Issues](https://github.com/x11lang/javascriptvirtualmachine-repo/issues).
* Se for uma nova funcionalidade, abra uma issue descrevendo o que deseja implementar antes de começar a codificar.

## 2. Estrutura do Código
O projeto é dividido em camadas claras. Ao propor uma alteração, verifique onde ela se encaixa:
* **Core Interpreter:** Lógica do ciclo de busca-execução (Stack, PC, Heap).
* **CLI/REPL:** Interface de usuário e processamento de comandos (`create`, `install`, `run`).
* **System API:** Módulos que permitem ao bytecode interagir com o sistema host.
* **Format:** Lógica de leitura/escrita do formato binário `.jsvmfile`.

## 3. Fluxo de Desenvolvimento (Workflow)
1. **Fork** do repositório.
2. **Clone** o seu fork localmente.
3. **Crie uma branch** para a sua feature: `git checkout -b feature/nome-da-feature`.
4. **Implemente** a alteração.
5. **Teste:** Certifique-se de que a nova funcionalidade não quebra a execução de binários existentes.
6. **Commit:** Use mensagens de commit claras seguindo o padrão de imperativo (ex: "Add PUSH opcode support").
7. **Push e Pull Request:** Envie sua branch e abra um Pull Request para a branch `main`.

## 4. Padrões de Código
* **Performance:** Ao tocar no `Core`, priorize a eficiência. Evite alocação excessiva de objetos dentro do loop de execução (`while(pc < bytecode.length)`).
* **Segurança:** Lembre-se que a JSVM lida com execução de binários. Toda nova API deve considerar se há risco de acesso indevido à memória fora do Heap da VM.
* **Documentação:** Se adicionar um novo opcode, atualize o documento de referência do formato `.jsvmfile`.

## 5. Licenciamento
Ao contribuir para este projeto, você concorda que suas contribuições serão licenciadas sob a **Apache License 2.0**, conforme definido no arquivo `LICENSE`.

---
*Dúvidas? Entre em contato através das nossas Issues ou abra uma discussão no GitHub.*
