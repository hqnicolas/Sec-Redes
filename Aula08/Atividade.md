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
