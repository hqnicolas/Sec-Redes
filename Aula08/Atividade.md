## ATIVIDADE – ACL (Access Control List)

Na rede abaixo é demonstrado de forma lógica a segmentação de rede de alguns setores:

<img width="1260" height="627" alt="image" src="https://github.com/user-attachments/assets/4276c8de-85bc-4627-8861-8f78a1d87979" />


### Equipamentos

-   **Switch-Core:** Responsável por endereçar as VLANs aos demais Switches dos outros prédios e também a rede de servidores.
-   **Switch-Predio01:** Equipamento localizado no Prédio-01, abrigando os setores de Contabilidade e TI.
-   **Switch-Predio02:** Equipamento localizado no Prédio-02, abrigando os setores de RH e Departamento Pessoal.

### Redes

#### **Switches:**
- **VLAN:** 100
- **Rede:** `192.168.100.0/24`

#### **Servidores:**
- **VLAN:** 101
- **Rede:** `192.168.101.0/24`

#### **Contabilidade**
- **VLAN:** 102
- **Rede:** `192.168.102.0/24`

#### **TI**
- **VLAN:** 103
- **Rede:** `192.168.103.0/24`

#### **RH**
- **VLAN:** 104
- **Rede:** `192.168.104.0/24`

#### **Departamento Pessoal**
- **VLAN:** 105
- **Rede:** `192.168.105.0/24`

---

### Servidores
Os servidores possuem IPs estáticos.

**Server-DHCP-DNS**
- **IP:** `192.168.101.1`
- Tem os serviços de DHCP e DNS habilitados.
- No DNS tem o apontamento para:
    - `empresa.com` -> `192.168.101.2`
    - `www.empresa.com` -> `192.168.101.2`
    - `portal.empresa.com` -> `192.168.101.2`
    - `ftp.empresa.com` -> `192.168.101.3`

**Server-WEB**
- **IP:** `192.168.101.2`
- Tem os serviços HTTP e HTTPS habilitados.

**Server-FTP**
- **IP:** `192.168.101.3`
- Tem o serviço de FTP habilitado.
- **Usuário/Senha:** `admin/admin` ou `cisco/cisco`

---

### Objetivo

Como observado, as redes estão segmentadas, mas há um problema: não estão segregadas. Você será o responsável por manter a segurança entre essas redes por meio de ACLs.

Crie uma ou mais ACL(s) de forma que:

-   Todos os setores precisam ter acesso ao DHCP e DNS.
-   A contabilidade não deve ter acesso ao FTP.
-   O serviço HTTP foi deixado disponível por ter uma aplicação legada que somente a TI utiliza; por isso, deixe disponível esse serviço **apenas a este setor**.
-   Uma VLAN não pode “enxergar” a outra.

### Entrega

-   Deverá ser entregue o arquivo em `.pkt` com a(s) ACL(s) configurada(s).
-   Lembrar de dar o comando `write memory` no switch para salvar a configuração.


# Switch Core
```
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
hostname SW-CORE
ip routing
spanning-tree mode pvst
interface FastEthernet0/1
 description Server-DHCP-DNS
 switchport access vlan 101
 switchport mode access
interface FastEthernet0/2
 description Server-WEB
 switchport access vlan 101
 switchport mode access
interface FastEthernet0/3
 description Server-FTP
 switchport access vlan 101
 switchport mode access
interface GigabitEthernet0/1
 description Link-SW-Predio01
 switchport trunk allowed vlan 100,102-103
 switchport trunk encapsulation dot1q
 switchport mode trunk
interface GigabitEthernet0/2
 description Link-SW-Predio02
 switchport trunk allowed vlan 100,104-105
 switchport trunk encapsulation dot1q
 switchport mode trunk
interface Vlan1
 no ip address
interface Vlan100
 mac-address 0060.70be.8a01
 ip address 192.168.100.1 255.255.255.0
interface Vlan101
 mac-address 0060.70be.8a02
 ip address 192.168.101.254 255.255.255.0
interface Vlan102
 mac-address 0060.70be.8a03
 ip address 192.168.102.254 255.255.255.0
 ip helper-address 192.168.101.1
 ip access-group block in
interface Vlan103
 mac-address 0060.70be.8a04
 ip address 192.168.103.254 255.255.255.0
 ip helper-address 192.168.101.1
 ip access-group block in
interface Vlan104
 mac-address 0060.70be.8a05
 ip address 192.168.104.254 255.255.255.0
 ip helper-address 192.168.101.1
 ip access-group block in
interface Vlan105
 mac-address 0060.70be.8a06
 ip address 192.168.105.254 255.255.255.0
 ip helper-address 192.168.101.1
 ip access-group block in
ip classless
ip flow-export version 9
ip access-list extended block
 permit udp any any eq bootps
 permit udp any any eq bootpc
 permit udp any host 192.168.101.1 eq domain
 permit tcp any host 192.168.101.1 eq domain
 deny tcp 192.168.102.0 0.0.0.255 host 192.168.101.3 eq ftp
 permit tcp any host 192.168.101.3 eq ftp
 permit tcp 192.168.103.0 0.0.0.255 host 192.168.101.2 eq www
 deny tcp any host 192.168.101.2 eq www
 permit tcp any host 192.168.101.2 eq 443
line con 0
line aux 0
line vty 0 4
 login
end
```

# Switch Predio 1
```
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
hostname SW-Predio01
spanning-tree mode pvst
spanning-tree extend system-id
interface FastEthernet0/1
 description PC-Contabilidade
 switchport access vlan 102
 switchport mode access
interface FastEthernet0/2
 description PC-Contabilidade
 switchport access vlan 102
 switchport mode access
interface FastEthernet0/3
 description PC-TI
 switchport access vlan 103
 switchport mode access
interface GigabitEthernet0/2
 description Link.SW-CORE
 switchport trunk allowed vlan 100,102-103
 switchport mode trunk
interface Vlan1
 no ip address
 shutdown
interface Vlan100
 ip address 192.168.100.2 255.255.255.0
line con 0
line vty 0 4
 login
line vty 5 15
 login
end
```

# Switch Predio 2
```
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
hostname SW-Predio02
spanning-tree mode pvst
spanning-tree extend system-id
interface FastEthernet0/1
 description PC-RH
 switchport access vlan 104
 switchport mode access
interface FastEthernet0/2
 description PC-RH
 switchport access vlan 104
 switchport mode access
interface FastEthernet0/3
 description PC-DP
 switchport access vlan 105
 switchport mode access
interface GigabitEthernet0/2
 description Link.SW-CORE
 switchport trunk allowed vlan 100,104-105
 switchport mode trunk
interface Vlan1
 no ip address
 shutdown
interface Vlan100
 ip address 192.168.100.3 255.255.255.0
line con 0
line vty 0 4
 login
line vty 5 15
 login
end
```
