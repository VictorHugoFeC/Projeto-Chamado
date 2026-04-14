# 📌 Sistema de Controle de Chamados de TI

> **Versão:** 2.0 – 25/02/2026  
> **Status:** Em Desenvolvimento 🛠️

## 👥 Grupo de Desenvolvimento
* Beatriz Moscareli
* Bruno Rodrigues
* Cayky Victor Hermann
* Henrique de Souza
* João Vitor Martins dos Santos
* Marcos Munir Moreira Melo da Silva
* Rodrigo Alves dos Santos

---

## 🏢 Visão Geral da Empresa
Rede de supermercados de pequeno porte (5 lojas) que necessita gerenciar problemas técnicos internos como:
* 💻 Computadores e Periféricos
* 🖨️ Impressoras
* 🛠️ Sistemas Internos
* 🌐 Equipamentos de Rede

### ⚠️ O Problema
Atualmente, o controle é feito via planilhas e anotações manuais, resultando em:
* Falta de rastreabilidade e auditoria.
* Ausência de controle de login e permissões.
* Perda de histórico de movimentações.
* Dificuldade na priorização de tarefas.

### 🎯 Objetivo da Solução
Desenvolver um software em **Java** estruturado e seguro para centralizar o registro, acompanhamento e finalização de chamados técnicos com histórico completo.

---

## 📦 Escopo do Projeto

### ✅ Dentro do Escopo (IN)
- [x] Sistema de Login e Cadastro de Usuários.
- [x] Cadastro de Categorias e Prioridades (Estágios 1, 2 e 3).
- [x] Abertura e Listagem de chamados com filtros por status.
- [x] Registro automático de histórico e inserção de observações.
- [x] Fluxo de finalização de chamados.

### ❌ Fora do Escopo (OUT)
- [ ] Interface Web ou Mobile (O sistema será Desktop/Console).
- [ ] Envio automático de e-mails.
- [ ] Dashboards com gráficos complexos.
- [ ] Integrações com sistemas externos.

---

## 🔄 Fluxo do Sistema

1. **Login:** Validação de credenciais para acesso ao sistema.
2. **Abertura:** Registro do problema com ID automático, data/hora e status inicial "Aberto".
3. **Andamento:** Alteração de status com registro obrigatório de histórico.
4. **Finalização:** Só permitida se o chamado estiver "Em Atendimento". Uma vez concluído, o chamado torna-se imutável.

---

## 📋 Especificações Técnicas

### Requisitos Funcionais (Principais)
| ID | Descrição |
|:---:| --- |
| **RF01** | Realizar login de usuário |
| **RF03** | Registrar chamado com data/hora automática |
| **RF06** | Alterar status do chamado |
| **RF09** | Finalizar chamado (Regra de transição) |
| **RF12** | Visualizar histórico completo de movimentações |

### Regras de Negócio (RN)
* **RN02:** Todo chamado inicia obrigatoriamente com o status `Aberto`.
* **RN03:** A finalização só é permitida se o status atual for `Em Atendimento`.
* **RN04:** Chamados finalizados não permitem novas alterações.
* **RN08:** Registros de histórico não podem ser editados ou excluídos (Auditoria).

### Requisitos Não Funcionais (RNF)
* **Linguagem:** Java.
* **Persistência:** Local (JSON ou CSV).
* **Capacidade:** Suporte para até 500 chamados.
* **Ambiente:** Funcionamento Offline.

---

## 🗂️ Estrutura de Entidades

```java
// Representação conceitual das classes principais
class Usuario {
    int id;
    String nome, login, senha;
}

class Chamado {
    int id;
    String descricao;
    LocalDateTime dataAbertura;
    Status statusAtual;
    int prioridade;
    Categoria categoria;
}

enum Status {
    ABERTO, EM_ATENDIMENTO, AGUARDANDO_PECA, 
    AGUARDANDO_USUARIO, EM_OBSERVACAO, CONCLUIDO
}
