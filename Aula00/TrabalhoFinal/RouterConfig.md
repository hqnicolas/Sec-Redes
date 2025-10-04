# Análise da Configuração do Roteador

Este documento detalha a configuração de um roteador, incluindo a configuração de BGP, interfaces VLAN, pools de DHCP e endereços IP excluídos.

## Configuração Completa

```cisco
enable
configure terminal
router bgp 65019
bgp log-neighbor-changes
interface FastEthernet0/0
no shutdown
interface FastEthernet0/1
no shutdown
interface FastEthernet0/0.10
encapsulation dot1Q 10
ip address 192.168.72.1 255.255.255.240
no shutdown
interface FastEthernet0/0.20
encapsulation dot1Q 20
ip address 192.168.72.17 255.255.255.252
no shutdown
interface FastEthernet0/0.30
encapsulation dot1Q 30
ip address 192.168.72.33 255.255.255.240
no shutdown
interface FastEthernet0/0.40
encapsulation dot1Q 40
ip address 192.168.72.49 255.255.255.240
no shutdown
ip dhcp pool VLAN_ADMINISTRACAO
network 192.168.72.0 255.255.255.240
default-router 192.168.72.1
dns-server 8.8.8.8
ip dhcp pool VLAN_COMUM
network 192.168.72.16 255.255.255.252
default-router 192.168.72.17
dns-server 8.8.8.8
ip dhcp pool VLAN_PLANEJAMENTO
network 192.168.72.32 255.255.255.240
default-router 192.168.72.33
dns-server 8.8.8.8
ip dhcp pool VLAN_APOIO
network 192.168.72.48 255.255.255.240
default-router 192.168.72.49
dns-server 8.8.8.8
ip dhcp excluded-address 192.168.72.1 192.168.72.2
ip dhcp excluded-address 192.168.72.17 192.168.72.18
ip dhcp excluded-address 192.168.72.33 192.168.72.34
ip dhcp excluded-address 192.168.72.49 192.168.72.50
end
write memory
````

-----

## Detalhes da Configuração

### Roteamento BGP

  - O protocolo BGP está configurado com o **Autonomous System (AS)** número `65019`.
  - O logging de alterações de vizinhança BGP está ativado.

### Interfaces Físicas

  - As interfaces `FastEthernet0/0` e `FastEthernet0/1` foram ativadas.

### Sub-interfaces e VLANs

A interface `FastEthernet0/0` foi dividida em várias sub-interfaces, cada uma associada a uma VLAN específica.

| Sub-interface | ID da VLAN | Endereço IP | Máscara de Sub-rede |
| :--- | :---: | :--- | :--- |
| `FastEthernet0/0.10` | 10 | `192.168.72.1` | `255.255.255.240` |
| `FastEthernet0/0.20` | 20 | `192.168.72.17`| `255.255.255.252` |
| `FastEthernet0/0.30` | 30 | `192.168.72.33`| `255.255.255.240` |
| `FastEthernet0/0.40` | 40 | `192.168.72.49`| `255.255.255.240` |

-----

## Servidor DHCP

O roteador foi configurado para atuar como um servidor DHCP, fornecendo endereços IP para quatro VLANs distintas.

### Pools de DHCP

#### Pool: `VLAN_ADMINISTRACAO`

  - **Rede:** `192.168.72.0/28`
  - **Gateway Padrão:** `192.168.72.1`
  - **Servidor DNS:** `8.8.8.8`

#### Pool: `VLAN_COMUM`

  - **Rede:** `192.168.72.16/30`
  - **Gateway Padrão:** `192.168.72.17`
  - **Servidor DNS:** `8.8.8.8`

#### Pool: `VLAN_PLANEJAMENTO`

  - **Rede:** `192.168.72.32/28`
  - **Gateway Padrão:** `192.168.72.33`
  - **Servidor DNS:** `8.8.8.8`

#### Pool: `VLAN_APOIO`

  - **Rede:** `192.168.72.48/28`
  - **Gateway Padrão:** `192.168.72.49`
  - **Servidor DNS:** `8.8.8.8`

### Endereços Excluídos do DHCP

Os seguintes endereços IP foram reservados e não serão distribuídos pelos pools de DHCP:

  - `192.168.72.1` a `192.168.72.2`
  - `192.168.72.17` a `192.168.72.18`
  - `192.168.72.33` a `192.168.72.34`
  - `192.168.72.49` a `192.168.72.50`

### Salvando a Configuração

  - O comando `write memory` foi utilizado para salvar a configuração ativa na memória não volátil do roteador.

<!-- end list -->

```
