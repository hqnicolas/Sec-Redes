# Comandos para Configuração de Switches Cisco

Uma coleção de comandos básicos para configurar VLANs, ACLs e interfaces em switches Cisco.

## Modos de Acesso e Configuração

### Entrar em Modo Privilegiado

```bash
enable
```

### Entrar em Modo de Configuração Global

```bash
configure terminal
```

-----

## Configuração de VLANs

### Criar VLAN e Atribuir um Endereço IP

1.  **Criar a VLAN:**
    ```bash
    vlan 10
    name NOME_DA_VLAN
    exit
    ```
2.  **Atribuir um endereço IP à interface da VLAN:**
    ```bash
    interface vlan 10
    ip address 192.168.1.1 255.255.255.0
    ```

### Definir Interface como Modo de Acesso

Define uma porta para pertencer a uma única VLAN.

```bash
interface GigabitEthernet0/1
switchport mode access
switchport access vlan 10
```

### Definir Interface como Modo Trunk

Permite que a porta transporte tráfego de múltiplas VLANs.

```bash
interface GigabitEthernet0/2
switchport trunk encapsulation dot1q
switchport mode trunk
switchport trunk allowed vlan 10,20,30
```

### Habilitar Roteamento entre VLANs

Para que as VLANs possam se comunicar, o roteamento IP deve ser habilitado no switch (Layer 3).

```bash
ip routing
```

-----

## Configuração de Access Control List (ACL)

### Criar uma ACL Extendida

```bash
ip access-list extended NOME_DA_ACL
```

**Sintaxe da regra:**
`ação protocolo origem destino porta`

**Exemplos de regras:**

  * Permitir tráfego HTTP para um host específico:
    ```bash
    permit tcp any host 10.1.1.1 eq 80
    ```
  * Bloquear todo o tráfego IP:
    ```bash
    deny ip any any
    ```

### Vincular ACL a uma Interface VLAN

Aplique a ACL a uma interface VLAN para filtrar o tráfego de entrada (`in`) ou saída (`out`). Recomenda-se usar `in` para filtrar os pacotes na entrada.

```bash
interface vlan 10
ip access-group NOME_DA_ACL in
```

-----

## Comandos de Verificação

### Ver Todas as Configurações Ativas

```bash
show running-config
```

### Ver Apenas as ACLs Configuradas

```bash
show ip access-lists
```

### Ver o Status das Interfaces

```bash
show interfaces status
```

-----

## Desativar Configurações

Para desativar um comando, utilize `no` antes da configuração que deseja remover.

**Exemplos:**

  * **Desvincular uma ACL de uma interface VLAN:**
    ```bash
    no ip access-group NOME_DA_ACL in
    ```
  * **Remover uma regra específica de uma ACL:**
    ```bash
    no permit tcp any host 10.1.1.1 eq 80
    ```
  * **Remover o endereço IP de uma interface:**
    ```bash
    no ip address
    ```

-----

## Salvar Configurações

Para persistir as configurações após uma reinicialização, salve a configuração ativa na configuração de inicialização. Execute este comando em modo privilegiado.

```bash
write
```
