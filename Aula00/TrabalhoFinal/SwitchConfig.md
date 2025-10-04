# Análise da Configuração do Switch

Este documento detalha a configuração de um switch de Camada 3, incluindo a criação de VLANs, endereçamento IP, atribuição de portas e configuração de entroncamento (trunk).

## Configurações Globais

O roteamento IP é ativado, permitindo que o switch realize o roteamento entre as VLANs configuradas.

```cisco
enable
configure terminal
ip routing
````

-----

## Resumo das VLANs e Interfaces (SVIs)

Quatro VLANs foram criadas e configuradas com interfaces virtuais de switch (SVIs), cada uma com seu próprio endereço IP para atuar como gateway padrão para sua respectiva sub-rede.

| ID da VLAN | Nome da VLAN  | Endereço IP da Interface | Máscara de Sub-rede | Rede             | Broadcast        | Faixa de IPs Utilizáveis     |
| :--------- | :------------ | :----------------------- | :------------------ | :--------------- | :--------------- | :--------------------------- |
| `10`       | ADMINISTRACAO | `192.168.72.1`           | `255.255.255.240`   | `192.168.72.0`   | `192.168.72.15`  | `192.168.72.1` - `192.168.72.14`   |
| `20`       | COMUM         | `192.168.72.17`          | `255.255.255.252`   | `192.168.72.16`  | `192.168.72.19`  | `192.168.72.17` - `192.168.72.18`  |
| `30`       | PLANEJAMENTO  | `192.168.72.33`          | `255.255.255.240`   | `192.168.72.32`  | `192.168.72.47`  | `192.168.72.33` - `192.168.72.46`  |
| `40`       | APOIO         | `192.168.72.49`          | `255.255.255.240`   | `192.168.72.48`  | `192.168.72.63`  | `192.168.72.49` - `192.168.72.62`  |

### Comandos de Configuração das SVIs

```cisco
interface Vlan10
 ip address 192.168.72.1 255.255.255.240
 no shutdown
!
interface Vlan20
 ip address 192.168.72.17 255.255.255.252
 no shutdown
!
interface Vlan30
 ip address 192.168.72.33 255.255.255.240
 no shutdown
!
interface Vlan40
 ip address 192.168.72.49 255.255.255.240
 no shutdown
```

-----

## Atribuição de Portas de Acesso

As portas do switch são configuradas em modo de acesso e atribuídas às VLANs correspondentes.

| VLAN ID / Nome     | Portas Atribuídas                                   |
| :----------------- | :-------------------------------------------------- |
| **VLAN 10** (ADMINISTRACAO) | `Fa0/6` - `Fa0/9`, `Fa0/16` - `Fa0/17`, `Fa0/22` - `Fa0/23` |
| **VLAN 20** (COMUM)         | `Fa0/1` - `Fa0/2`                                     |
| **VLAN 30** (PLANEJAMENTO)  | `Fa0/3` - `Fa0/5`, `Fa0/10` - `Fa0/11`                  |
| **VLAN 40** (APOIO)         | `Fa0/12` - `Fa0/15`, `Fa0/18` - `Fa0/21`                |

### Comandos de Configuração das Portas

```cisco
! VLAN 10
interface range FastEthernet0/6 - 9, FastEthernet0/16 - 17, FastEthernet0/22 - 23
 switchport mode access
 switchport access vlan 10
 no shutdown
!
! VLAN 20
interface range FastEthernet0/1 - 2
 switchport mode access
 switchport access vlan 20
 no shutdown
!
! VLAN 30
interface range FastEthernet0/3 - 5, FastEthernet0/10 - 11
 switchport mode access
 switchport access vlan 30
 no shutdown
!
! VLAN 40
interface range FastEthernet0/12 - 15, FastEthernet0/18 - 21
 switchport mode access
 switchport access vlan 40
 no shutdown
```

-----

## Configuração da Porta Trunk

A porta `GigabitEthernet0/1` é configurada como um link trunk, com a descrição "Link para roteador externo". Este link permite o tráfego de todas as VLANs configuradas (`10, 20, 30, 40`) para um roteador externo ou outro switch.

```cisco
interface GigabitEthernet0/1
 description Link para roteador externo
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40
 no shutdown
```

-----

## Salvando a Configuração

Finalmente, a configuração ativa (`running-config`) é salva na memória não volátil (`startup-config`), garantindo que as configurações persistam após uma reinicialização do dispositivo.

```cisco
end
write memory
```

```
