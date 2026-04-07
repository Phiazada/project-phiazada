# 🎮 Project Phiazada

Plataforma de ranks e organização de torneios amistosos, com suporte a múltiplos jogos.

---

## 📌 Sobre o Projeto

O **Project Phiazada** é uma plataforma para gerenciar usuários, jogos e torneios amistosos entre amigos. O sistema permite cadastro de jogadores, seleção de jogos favoritos, criação de torneios com tabela de pontos e sistema de ranks com reset mensal.

---

## 🛠️ Stack

| Camada | Tecnologia |
|---|---|
| Infra | Windows Server + Azure |
| Banco de Dados | MongoDB + MariaDB |
| Back-end | Node.js com TypeScript |
| Front-end | React com TypeScript |
| Dev local | Docker |
| CI/CD | GitHub Actions |

---

## 🏗️ Arquitetura

O projeto utiliza arquitetura de **microserviços** com um API Gateway central roteando as chamadas entre os serviços.

```
Gateway
├── users-service       → MongoDB
├── jogos-service       → MongoDB
├── torneios-service    → MariaDB
└── pareamento-service  → MariaDB
```

| Serviço | Banco | Descrição |
|---|---|---|
| users | MongoDB | Usuários, ranks, amizades |
| jogos | MongoDB | Catálogo de jogos |
| torneios | MariaDB | Torneios, pontos, reset mensal |
| pareamento | MariaDB | Pareamento de partidas e resultados |
| gateway | — | Roteamento central de todas as APIs |

---

## 📦 CRUDs

### 👤 CRUD de Usuários
- Nome
- Senha
- Foto de perfil *(talvez)*
- Rank
- Sistema de envio de pedido de amizade
- Sistema de aceite de pedido de amizade

### 🎮 CRUD de Games
- Nome
- Plataforma
- Gênero
- Modo de jogo

### 🏆 CRUD de Torneios
- Nome do torneio
- Convidar jogadores amigos
- Tabela de usuários com respectivos pontos
- Sistema de reset a cada mês
- Sistema de pareamento de partida
- Sistema de banir mapas
- Sistema de partida — ganhadores ganham X pontos, perdedores perdem Y pontos

---

## 👥 Divisão de Tarefas

| Tarefa | Infra/SRE | QA/Dev |
|---|---|---|
| Windows Server | ✅ Lidera | ✅ Aprende junto |
| Azure (VM, redes) | ✅ Lidera | ✅ Aprende junto |
| CI/CD (GitHub Actions) | ✅ Configura | Usa |
| Back-end (Node.js + TS) | ✅ Ajuda | ✅ Lidera |
| Banco de dados | Configura infra | ✅ Modelagem/queries |
| Front-end (React + TS) | — | ✅ Lidera |
| Testes automatizados | — | ✅ Principal |
| Sistema de ranks/pontos | Apoio | ✅ Lidera |

---

## 🗺️ Roadmap

- [x] Definir estrutura do banco de dados
- [ ] Subir VM com Windows Server no Azure
- [ ] Configurar MongoDB + MariaDB na VM
- [~] Configurar ambiente local com Docker *(em progresso)*
- [x] Desenvolver CRUD de Usuários
- [x] Desenvolver CRUD de Games
- [x] Desenvolver CRUD de Torneios
- [ ] Implementar sistema de ranks
- [ ] Implementar sistema de torneios
- [ ] Montar API Gateway
- [ ] Configurar CI/CD com GitHub Actions
- [ ] Testes automatizados
- [ ] Deploy final no Azure

---

## 📁 Repositórios

| Repositório | Descrição |
|---|---|
| [infra](https://github.com/Phiazada/infra) | Docker com MongoDB e MariaDB |
| [gateway](https://github.com/Phiazada/gateway) | API Gateway central |
| [users](https://github.com/Phiazada/users) | API de usuários |
| [jogos](https://github.com/Phiazada/jogos) | API de jogos |
| [torneios](https://github.com/Phiazada/torneios) | API de torneios |
| [pareamento](https://github.com/Phiazada/pareamento) | API de pareamento de partidas |

---

## 🤝 Membros

| Membro | Papel |
|---|---|
| Dherick | QA / Dev |
| Arthur | Infra / SRE |

---

## 🔗 Links

- [Notion do Projeto](https://www.notion.so/Projeto-Cfs-Phiazada-33bc57f4dcdd80b6ada2fef8d322b8a5)
- [Organização GitHub](https://github.com/Phiazada)
