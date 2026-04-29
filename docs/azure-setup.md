# ☁️ Infraestrutura Azure — Phiazada

Documentação completa do processo de configuração da infraestrutura no Microsoft Azure para o projeto Phiazada. Cada passo foi executado via **Azure CLI** para posterior automação com **GitHub Actions**.

> 💡 **Por que Azure CLI?** Usar a CLI em vez do portal gráfico permite que todos os comandos sejam reutilizados e automatizados futuramente no pipeline de CI/CD com GitHub Actions.

---

## 📋 Visão Geral

| Item | Valor |
|---|---|
| **Plataforma** | Microsoft Azure |
| **Sistema Operacional** | Windows Server 2022 Datacenter |
| **Região** | Brazil South (`brazilsouth`) |
| **Ferramenta** | Azure CLI |
| **Automação futura** | GitHub Actions |

---

## ✅ Passo a Passo

### Passo 1 — Criar o Resource Group

O **Resource Group** é um contêiner lógico no Azure que agrupa todos os recursos relacionados a um projeto (VMs, redes, discos, IPs, etc.). Ele facilita o gerenciamento, monitoramento e exclusão em conjunto de todos os recursos do projeto.

```bash
az group create --name rg-phiazada --location brazilsouth
```

**Resultado esperado:**
```
Name         Location     Status
-----------  -----------  ---------
rg-phiazada  brazilsouth  Succeeded
```

| Parâmetro | Valor | Descrição |
|---|---|---|
| `--name` | `rg-phiazada` | Nome do grupo de recursos |
| `--location` | `brazilsouth` | Região do Azure (São Paulo) |

---

### Passo 2 — Criar a VM Windows Server

A **Virtual Machine (VM)** é o servidor principal do projeto. Escolhemos o **Windows Server 2022 Datacenter** por ser a versão mais recente e estável, com suporte completo a Docker e todas as ferramentas que utilizaremos.

O tamanho `Standard_B2s` oferece **2 vCPUs e 4GB de RAM**, suficiente para o ambiente de estudos com bom custo-benefício.

```bash
az vm create \
  --resource-group rg-phiazada \
  --name vm-phiazada \
  --image Win2022Datacenter \
  --admin-username adminphiazada \
  --admin-password "Phiazada@2026" \
  --size Standard_B2s \
  --location brazilsouth \
  --public-ip-sku Standard \
  --output table
```

| Parâmetro | Valor | Descrição |
|---|---|---|
| `--resource-group` | `rg-phiazada` | Grupo de recursos onde a VM será criada |
| `--name` | `vm-phiazada` | Nome da VM |
| `--image` | `Win2022Datacenter` | Windows Server 2022 Datacenter |
| `--admin-username` | `adminphiazada` | Usuário administrador da VM |
| `--size` | `Standard_B2s` | 2 vCPUs, 4GB RAM |
| `--location` | `brazilsouth` | Mesma região do Resource Group |
| `--public-ip-sku` | `Standard` | IP público estático para acesso RDP |

---

### Passo 3 — Liberar porta RDP (3389) *(em breve)*

### Passo 4 — Configurar Network Security Group (NSG) *(em breve)*

### Passo 5 — Instalar Docker na VM *(em breve)*

### Passo 6 — Configurar CI/CD com GitHub Actions *(em breve)*

---

## 📌 Recursos Criados

| Recurso | Nome | Região |
|---|---|---|
| Resource Group | `rg-phiazada` | Brazil South |
| Virtual Machine | `vm-phiazada` | Brazil South |

---

## 🔗 Referências

- [Azure CLI Docs](https://learn.microsoft.com/en-us/cli/azure/)
- [Windows Server 2022 no Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/)
- [GitHub Actions + Azure](https://learn.microsoft.com/en-us/azure/developer/github/github-actions)
