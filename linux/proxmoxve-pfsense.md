
# Documentação Oficial
## Configuração de Load Balance + Failover no pfSense
### Ambiente Virtualizado em Proxmox VE

---

# 1. Cenário da Infraestrutura

## Rede Física

| Interface Física | Função |
|------------------|--------|
| enp3s0 | LAN |
| enp2s0 | WAN1 |
| enp1s0 | WAN2 |

## Bridges Corretas no Proxmox

| Bridge | Porta Física | Função |
|--------|-------------|--------|
| vmbr0 | enp3s0 | LAN |
| vmbr1 | enp2s0 | WAN1 |
| vmbr2 | enp1s0 | WAN2 |

## Interfaces da VM pfSense

| Interface | Bridge | Função |
|-----------|--------|--------|
| vtnet0 | vmbr0 | LAN |
| vtnet1 | vmbr1 | WAN1 |
| vtnet2 | vmbr2 | WAN2 |

---

# PASSO A PASSO

---

## Passo 1
### System > Routing

### Gateways

Adicionar GW_WAN1:

- Interface: WAN1 (vtnet1)
- Gateway: DHCP
- Descrição: GW_WAN1
- Monitor IP: 8.8.8.8

Adicionar GW_WAN2:

- Interface: WAN2 (vtnet2)
- Gateway: DHCP
- Descrição: GW_WAN2
- Monitor IP: 1.1.1.1

---

### Gateway Groups

Criar grupo: LB_FAILOVER

- GW_WAN1: Tier 1
- GW_WAN2: Tier 1
- Trigger Level: Member Down

Comentário:
Tier 1 + Tier 1 = Load Balance ativo.
Se um cair = Failover automático.

Para futura WAN3:
Criar nova bridge vmbr3, adicionar interface vtnet3,
criar GW_WAN3 e incluir no grupo.
Tier 1 = balanceamento
Tier 2 = backup

---

## Passo 2
### Firewall > Rules > LAN

Editar regra Allow LAN to any:

- Action: Pass
- Source: LAN net
- Destination: any
- Advanced > Gateway: LB_FAILOVER

---

## Passo 3
### Firewall > NAT > Outbound

Selecionar: Hybrid Outbound NAT

Verificar regras automáticas para WAN1 e WAN2.

Se necessário criar:

Interface: WAN1
Source: 192.168.200.0/24
Translation: Interface Address

Interface: WAN2
Source: 192.168.200.0/24
Translation: Interface Address

Comentário:
NAT é obrigatório para múltiplas WANs.

---

## Passo 4
### System > Advanced > Miscellaneous

Marcar:
Skip rules when gateway is down

---

## Testes

Desconectar cabo WAN1.
Verificar Status > Gateways.
Tráfego deve sair automaticamente pela WAN2.

---

# Falsos Positivos e Oscilação de Links

Se utilizar Trigger Level:
"Packet Loss" ou "High Latency"

Valores muito baixos (ex: 2% perda)
podem causar alternância constante entre links.

Recomendação:

- Packet Loss: 5% a 10%
- Latência: 300ms ou mais
- Preferir "Member Down" para maior estabilidade.

Oscilações podem ocorrer por:

- Flutuação momentânea do provedor
- Monitor IP instável
- DNS mal configurado
- Problemas físicos no cabo

Sempre usar Monitor IP externo estável e diferente para cada WAN.

---

# Versão Avançada - Policy Routing e VLAN

Criar VLANs em Interfaces > Assignments > VLANs.

Exemplo:

VLAN10 - Administrativo
VLAN20 - Visitantes

Em Firewall > Rules > VLAN10:
Gateway: GW_WAN1

Em Firewall > Rules > VLAN20:
Gateway: GW_WAN2

Isso permite:

- Separação de tráfego
- Forçar setor administrativo sair por WAN1
- Visitantes por WAN2
- Controle granular de banda

Também possível:

- Failover exclusivo por VLAN
- Balanceamento somente para determinados serviços
- QoS com Traffic Shaper

---

Documento finalizado.
