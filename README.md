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
| Banco de Dados | MongoDB |
| CI/CD | GitHub Actions |
| Back-end | A definir (Node.js recomendado) |
| Front-end | A definir |

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
| Back-end da aplicação | ✅ Ajuda | ✅ Lidera |
| Banco de dados (MongoDB) | Configura infra | ✅ Modelagem/queries |
| Testes automatizados | — | ✅ Principal |
| Sistema de ranks/pontos | Apoio | ✅ Lidera |

---

## 🗺️ Roadmap

- [ ] Definir stack de back/front
- [ ] Subir VM com Windows Server no Azure
- [ ] Configurar MongoDB na VM
- [ ] Desenvolver CRUD de Usuários
- [ ] Desenvolver CRUD de Games
- [ ] Desenvolver CRUD de Torneios
- [ ] Implementar sistema de ranks
- [ ] Implementar sistema de torneios
- [ ] Configurar CI/CD com GitHub Actions
- [ ] Testes automatizados
- [ ] Deploy final

---

## 📁 Estrutura do Repositório

```
project-phiazada/
├── docs/          # Documentação técnica
├── infra/         # Scripts de infra, Azure, Windows Server
├── backend/       # Código do back-end
├── frontend/      # Código do front-end
└── tests/         # Testes automatizados
```

---

## 🤝 Membros

| Membro | Papel |
|---|---|
| Dherick | QA / Dev |
| A definir | Infra / SRE |
