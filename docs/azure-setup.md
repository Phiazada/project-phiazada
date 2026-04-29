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

### Passo 1 — Criar o Resource Group ✅

O **Resource Group** é um contêiner lógico no Azure que agrupa todos os recursos relacionados a um projeto (VMs, redes, discos, IPs, etc.). Ele facilita o gerenciamento, monitoramento e exclusão em conjunto de todos os recursos do projeto.

```bash
az group create --name rg-phiazada --location brazilsouth
```

**Resultado:**
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

### Passo 2 — Criar a VM Windows Server ✅

A **Virtual Machine (VM)** é o servidor principal do projeto. Escolhemos o **Windows Server 2022 Datacenter** por ser a versão mais recente e estável, com suporte completo a Docker e todas as ferramentas que utilizaremos.

O tamanho `Standard_D2as_v4` oferece **2 vCPUs e 8GB de RAM** com processador AMD, com melhor custo-benefício para o ambiente de estudos.

> ⚠️ O tamanho `Standard_B2s` não estava disponível na região `brazilsouth`. Utilizamos o `Standard_D2as_v4` como alternativa.

```bash
az vm create \
  --resource-group rg-phiazada \
  --name vm-phiazada \
  --image Win2022Datacenter \
  --admin-username adminphiazada \
  --admin-password "Phiazada@2026" \
  --size Standard_D2as_v4 \
  --location brazilsouth \
  --public-ip-sku Standard \
  --output table
```

**Resultado:**
```
ResourceGroup    PowerState    PublicIpAddress    PrivateIpAddress    Location
---------------  ------------  -----------------  ------------------  -----------
rg-phiazada      VM running    4.201.216.92       10.0.0.4            brazilsouth
```

| Recurso | Valor |
|---|---|
| **IP Público** | `4.201.216.92` |
| **IP Privado** | `10.0.0.4` |
| **Status** | `VM running` |

> 💡 Para economizar créditos, desligue a VM quando não estiver usando:
> ```bash
> az vm deallocate --resource-group rg-phiazada --name vm-phiazada
> ```

---

### Passo 3 — Liberar porta RDP (3389) ✅

O **RDP (Remote Desktop Protocol)** é o protocolo que permite acessar a interface gráfica do Windows Server remotamente. A porta **3389** foi aberta no firewall da VM.

```bash
az vm open-port \
  --resource-group rg-phiazada \
  --name vm-phiazada \
  --port 3389 \
  --priority 100
```

| Parâmetro | Valor | Descrição |
|---|---|---|
| `--resource-group` | `rg-phiazada` | Grupo de recursos da VM |
| `--name` | `vm-phiazada` | Nome da VM |
| `--port` | `3389` | Porta do protocolo RDP |
| `--priority` | `100` | Prioridade da regra no NSG |

**Acesso confirmado:** conexão RDP estabelecida com sucesso na VM (`4.201.216.92`). Windows Server Manager acessível.

---

### Passo 4 — Configurar Network Security Group (NSG) ✅

O **NSG (Network Security Group)** controla o tráfego de entrada e saída da VM. Para aumentar a segurança, a regra de RDP foi restringida para aceitar conexões **apenas dos IPs autorizados** da equipe.

```bash
az network nsg rule update \
  --resource-group rg-phiazada \
  --nsg-name vm-phiazadaNSG \
  --name rdp \
  --source-address-prefixes <IP_ARTHUR> <IP_DHERICK>
```

| Usuário | Acesso |
|---|---|
| Arthur | ✅ IP autorizado |
| Dherick | ✅ IP autorizado |

> 🔒 **Segurança:** apenas os IPs da equipe conseguem conectar via RDP. Qualquer outra origem é bloqueada pelo NSG.

---

### Passo 5 — Instalar Docker na VM *(em breve)*

### Passo 6 — Configurar CI/CD com GitHub Actions *(em breve)*

---

## 📌 Recursos Criados

| Recurso | Nome | Região | Detalhes |
|---|---|---|---|
| Resource Group | `rg-phiazada` | Brazil South | — |
| Virtual Machine | `vm-phiazada` | Brazil South | IP: `4.201.216.92` |
| NSG | `vm-phiazadaNSG` | Brazil South | RDP restrito aos IPs da equipe |

---

## ⏳ Próximos Passos

- [x] Configurar acesso RDP
- [x] Configurar Network Security Group (NSG)
- [ ] Instalar Docker na VM
- [ ] Configurar CI/CD com GitHub Actions
- [ ] Deploy da aplicação

---

## 🔗 Referências

- [Azure CLI Docs](https://learn.microsoft.com/en-us/cli/azure/)
- [Windows Server 2022 no Azure](https://learn.microsoft.com/en-us/azure/virtual-machines/windows/)
- [GitHub Actions + Azure](https://learn.microsoft.com/en-us/azure/developer/github/github-actions)
