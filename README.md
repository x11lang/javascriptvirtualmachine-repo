# ⚡ JSVM (JavaScript Virtual Machine)
> *O poder do baixo nível, a flexibilidade do JavaScript.*

[![Versão](https://img.shields.io/badge/version-0.1.2-blue.svg)](https://github.com/x11lang/javascriptvirtualmachine-repo/releases)
[![Licença](https://img.shields.io/badge/license-Apache%202.0-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-Active-success.svg)](#)

A **JSVM** nasceu de uma necessidade fundamental no ecossistema de desenvolvimento: preencher a lacuna entre linguagens de alto nível e a execução em *bare-metal* (baixo nível). O que começou como uma simples máquina de pilha (*Stack Machine*) de prova de conceito, evoluiu rapidamente para um **Runtime de Infraestrutura Completo**, operando sob o ecossistema [x11lang](https://github.com/x11lang).

---

## 📖 O Manifesto JSVM
A JSVM não é apenas mais um interpretador. Ela é um ambiente isolado que trata o Node.js como o "motor de um sistema operacional virtual". Com gerenciamento contíguo de memória (`SharedArrayBuffer`), processamento multi-thread isolado, e um sistema nativo de pacotes de binários descentralizados, a JSVM transforma a maneira como você compila e executa código.

## 🏗️ Arquitetura do Sistema

A máquina é desenhada em **4 Camadas de Isolamento**:

| Camada | Componente | Responsabilidade |
| :--- | :--- | :--- |
| **Camada 0** | `Virtual CPU` | Core de Opcodes, *Program Counter* (PC), Pilha Lógica e Registradores. |
| **Camada 1** | `Memory Manager` | Gerenciamento de `Uint8Array` persistente via arquivos `memory.bin`. |
| **Camada 2** | `Host OS (REPL)` | CLI Interativa (`[root@localhost $:/] #`) com suporte a 100+ comandos. |
| **Camada 3** | `Repo Network` | Distribuição e Linkagem via *JSVM-API* e pacotes `.jsvmfile`. |

## ⚙️ O Formato `.jsvmfile`
Os programas executados pela máquina são empacotados em um formato binário de alta performance, projetado para leitura ultrarrápida:
* **Header Mágico (4 bytes):** `JSVM` (Validação de integridade)
* **Entry Point (4 bytes):** Endereço inicial da instrução (PC).
* **Payload:** *Bytecode* puro interpretado diretamente pelo Dispatcher da CPU virtual.

## 🚀 Instalação e Quick Start

```bash
# 1. Clone o repositório oficial
git clone [https://github.com/x11lang/javascriptvirtualmachine-repo.git](https://github.com/x11lang/javascriptvirtualmachine-repo.git)

# 2. Acesse a pasta e instale as dependências
cd javascriptvirtualmachine-repo
npm install

# 3. Inicie o Daemon da JSVM
node jsvm-core.js
