# T10

## 🧠 Desafio Técnico - Backend Assessment

Bem-vindo(a)! 👋

Este repositório contém um desafio técnico proposto pela T10, cujo objetivo é avaliar suas habilidades de desenvolvimento backend, com foco em boas práticas de arquitetura, clareza, testes e modelagem de domínio.

---

## 🧩 Contexto do Problema

Uma instituição financeira contratou a T10 com o objetivo de obter maior agilidade e controle sobre seus processos. Um desses processos — até então realizado de forma manual — é a **solicitação de débito automático** de empresas parceiras.

Seu desafio é construir uma aplicação backend responsável por **automatizar essa operação**, permitindo que outros serviços possam consumir os eventos gerados de forma fluida, segura e rastreável.

---

## 📌 Escopo do Projeto

### Entidades principais

- **ExternalApp**: aplicação externa que solicita ativações.
- **Customer**: cliente representado por `customer_mid`.
- **SuperUser**: analista da mesa de integração.

### Glossário

- `"Solicitação de ativação"` = **Activation Request**

---

## ✅ Casos de Uso

### 1. Autenticação

- `ExternalApp` ou `SuperUser` com credenciais válidas deve conseguir gerar um **token JWT**.
- Credenciais inválidas resultam em erro; nenhum token é gerado.
- A lista de tokens ativos é atualizada a cada geração.

### 2. Acesso a Recursos

- Um token válido e autorizado permite executar:

#### Comandos

| Ação                    | Permissão               |
|-------------------------|--------------------------|
| `RequestToken`          | ExternalApp, SuperUser   |
| `IssueProductActivation`| ExternalApp              |
| `RejectActivation`      | SuperUser                |
| `ApproveActivation`     | SuperUser                |

#### Leitura

| Recurso                 | Permissão               |
|-------------------------|--------------------------|
| `ActivationRequests`    | ExternalApp, SuperUser   |

- Tokens inválidos ou sem permissão retornam erro.

### 3. Solicitação de Ativação

- `ExternalApp` com token válido pode solicitar ativação para um `customer_mid`.
- Uma solicitação é criada e um **email de confirmação** enviado ao cliente.

### 4. Avaliação da Ativação

`SuperUser` com token válido pode:

- **Rejeitar** a ativação:
  - Despacha o cancelamento
  - Atualiza o modelo de leitura
  - Envia email de cancelamento
- **Aprovar** a ativação:
  - Despacha a aprovação
  - Atualiza o modelo de leitura
  - Envia email de confirmação

---

## 🧠 Modelo de Domínio

> Recomendado: incluir um diagrama de eventos ilustrando a relação entre comandos, eventos e modelos de leitura.

---

## 📋 Requisitos

### Requisitos Não Funcionais

- Até **30 empresas parceiras**
- Até **10 super-users**
- Suporte a **1 milhão de requisições por dia**
- Eventos operacionais disponíveis via **stream** para consumo externo

### Requisitos Funcionais

- Suporte aos **casos de uso descritos**

---

## 🛠️ Tecnologias Esperadas

| Camada        | Opções sugeridas               |
|---------------|--------------------------------|
| Backend       | Python · Go · Elixir           |
| Armazenamento | PostgreSQL · MongoDB           |
| Broker        | Kafka · RabbitMQ               |
| Entrypoints   | HTTP com autenticação JWT      |

---

## 🧱 Padrões Recomendados

- Arquitetura: **CQRS**, **Hexagonal**
- Design: **DDD**, **SOLID**
- **Bônus**: uso de **message bus como stream**

---

## 📦 Deploy

A entrega é livre. Sugestões:

- Docker + docker-compose
- PaaS como Heroku, Render ou Railway
- Documentação clara caso utilize localhost

---

## 🚀 Entrega (Release 0.1)

A primeira entrega deve conter:

- Um **servidor web funcional**
- Implementação completa dos casos de uso
- Requisitos funcionais e não funcionais
- Testes (unitários/integrados)
- Scripts de migração e schemas (se aplicável)

---

## 🧪 Avaliação

Critérios (em ordem de prioridade):

1. ✅ **Correção da solução**
2. 🧪 Qualidade e cobertura de **testes**
3. 📁 Organização, documentação e clareza
4. 🧼 Estilo, legibilidade e simplicidade do código
5. 🔌 Uso consciente de bibliotecas externas
6. 🔐 Boas práticas de segurança

### 🏆 Pontos Extras

- Testes de stress
- Modelagem e armazenamento bem estruturado

---

## ❌ Critérios Eliminatórios

- **Proibido copiar ou "se inspirar" em código de terceiros.**

---

## 📤 Submissão

Envie sua solução:

1. Por **fork e Pull Request** neste repositório, ou  
2. Por **email** para `it@t10.digital` com o assunto:

