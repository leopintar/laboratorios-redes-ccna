# 🖧 Laboratórios de Redes Corporativas, Segurança e Automação (Cisco CCNAv7)

Repositório dedicado à documentação de topologias e scripts de configuração em **Cisco IOS CLI**, desenvolvidos como aplicação prática da trilha **CCNAv7: Rede Empresarial, Segurança e Automação (Cisco Networking Academy / NIC.br)**[cite: 2].

---

## 🎯 Arquitetura e Cenário Implementado
Este laboratório estrutura a rede corporativa de uma matriz empresarial segmentada por **VLANs**, garantindo isolamento de tráfego entre departamentos, roteamento dinâmico e controle de acesso aos servidores críticos (Active Directory, DNS, ERP e sistema de chamados **GLPI**).

### Principais Tecnologias Aplicadas:
* **Segmentação L2 e Trunking (IEEE 802.1Q):** Separação lógica entre *Infraestrutura de TI (VLAN 10)*, *Corporativo/Usuários (VLAN 20)* e *Servidores (VLAN 30)*, além do isolamento da VLAN Nativa (VLAN 99).
* **Segurança de Camada 2 (Port-Security & BPDU Guard):** Proteção nas portas de acesso do switch (`SW1`) com aprendizado dinâmico (*Sticky MAC*), impedindo a conexão de dispositivos não autorizados na rede física.
* **Roteamento Inter-VLAN e OSPFv2:** Subinterfaces configuradas no roteador de borda (`R1`) atuando como *Default Gateway* de cada rede e troca dinâmica de rotas via protocolo **OSPFv2 (Area 0)**.
* **Listas de Controle de Acesso (ACLs Estendidas):** Filtragem de pacotes na interface de entrada para liberar aplicações web (HTTP/HTTPS - GLPI) e DNS aos usuários corporativos, bloqueando tentativas de acesso remoto administrativo via **SSH (Porta 22)** aos servidores.
* **NAT Overload (PAT):** Tradução de endereços internos (`192.168.0.0/16`) para navegação controlada na WAN/Internet.

---

## 📂 Arquivos do Repositório
1. [`config_roteador_r1_ospf_acl.ios`](./config_roteador_r1_ospf_acl.ios): Script completo de CLI para o Roteador de Borda `R1` (Hardening SSHv2, Subinterfaces 802.1Q, OSPFv2, ACL Estendida Nomeada e NAT/PAT).
2. [`config_switch_sw1_vlans_portsec.ios`](./config_switch_sw1_vlans_portsec.ios): Script completo de CLI para o Switch de Distribuição `SW1` (VLANs, Trunk 802.1Q, PortFast, BPDU Guard, Port-Security e bloqueio de portas ociosas).

*(Dica: você também pode subir seus arquivos `.pkt` salvos do Cisco Packet Tracer clicando em **Add file > Upload files** aqui no repositório).*

---

## 🔍 Comandos de Validação e Troubleshooting
Durante os testes de conectividade e segurança no **Cisco Packet Tracer**, os seguintes comandos validam a operação da rede:

```ios
! Verificar tabela de roteamento dinâmico OSPF e vizinhanças
show ip route ospf
show ip ospf neighbor

! Auditar contadores de bloqueio/permissão das políticas de segurança (ACL)
show access-lists ACL_SEGURANCA_CORP

! Verificar traduções ativas de endereços (NAT/PAT)
show ip nat translations

! Checar status das VLANs, Trunks e Port-Security no Switch
show vlan brief
show interfaces trunk
show port-security interface FastEthernet0/5
```

---
**Desenvolvido por:** [Leonardo de Freitas Pintar](https://github.com/leopintar) — *Engenheiro de Computação | Infraestrutura, Redes & Automação*
