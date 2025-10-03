# Comandos Essenciais para Cisco IOS

Uma coleção de comandos básicos para configuração de switches Cisco.

## Modos de Acesso

### Modo Privilegiado
[cite_start]Para acessar o modo de execução privilegiado. [cite: 1]
```bash
enable
````

### Modo de Configuração Global

[cite\_start]Para acessar o modo de configuração. [cite: 2]

```bash
configure terminal
```

-----

## VLANs

### [cite\_start]Criar VLAN e Atribuir Endereço IP [cite: 4]

Sequência para criar uma VLAN, nomeá-la e configurar um endereço IP para sua interface.

```bash
# Entra no modo de configuração da VLAN
[cite_start]vlan 10 [cite: 5]

# Define um nome para a VLAN
[cite_start]name Marketing [cite: 6]
[cite_start]exit [cite: 7]

# Acessa a interface da VLAN para configuração
[cite_start]interface vlan 10 [cite: 8]

# Atribui um endereço IP e máscara de sub-rede
[cite_start]ip address 192.168.10.1 255.255.255.0 [cite: 9]
```

### [cite\_start]Habilitar Roteamento entre VLANs [cite: 19]

Este comando habilita o roteamento de pacotes entre diferentes VLANs.

```bash
[cite_start]ip routing [cite: 20]
```

-----

## Configuração de Interfaces

### [cite\_start]Definir Interface como Modo Acesso [cite: 10]

Configura uma porta para pertencer a uma única VLAN.

```bash
# Seleciona a interface
[cite_start]interface FastEthernet0/1 [cite: 11]

# Define a porta como modo de acesso
[cite_start]switchport mode access [cite: 12]

# Atribui a porta à VLAN 10
[cite_start]switchport access vlan 10 [cite: 13]
```

### [cite\_start]Definir Interface como Modo Trunk [cite: 14]

Configura uma porta para permitir o tráfego de múltiplas VLANs.

```bash
# Seleciona a interface
[cite_start]interface GigabitEthernet0/1 [cite: 15]

# Define o encapsulamento do tronco (padrão para a maioria dos switches)
[cite_start]switchport trunk encapsulation dot1q [cite: 16]

# Define a porta como modo trunk
[cite_start]switchport mode trunk [cite: 17]

# Define quais VLANs são permitidas no tronco (ex: VLANs 10, 20 e 30)
[cite_start]switchport trunk allowed vlan 10,20,30 [cite: 18]
```

-----

## Access Control Lists (ACL)

### [cite\_start]Criar ACL Estendida [cite: 23]

Cria uma lista de controle de acesso para filtrar o tráfego.

```bash
# Cria uma ACL estendida chamada "FILTRO_WEB"
[cite_start]ip access-list extended FILTRO_WEB [cite: 24]
```

[cite\_start]**Estrutura da regra:** `Ação - protocolo - origem - destino - porta` [cite: 25]

**Exemplos:**

```bash
# Permite tráfego TCP de qualquer origem para o host 10.1.1.1 na porta 80 (HTTP)
[cite_start]permit tcp any host 10.1.1.1 eq 80 [cite: 26]

# Bloqueia todo o tráfego IP de qualquer origem para qualquer destino
[cite_start]deny ip any any [cite: 27]
```

### [cite\_start]Vincular ACL a uma Interface VLAN [cite: 28]

Aplica as regras da ACL ao tráfego de entrada (in) ou saída (out) de uma interface VLAN.

```bash
# Acessa a interface da VLAN
[cite_start]interface vlan 10 [cite: 29]

# Aplica a ACL "FILTRO_WEB" para o tráfego de entrada
[cite_start]ip access-group FILTRO_WEB in [cite: 30]
```

[cite\_start]*Nota: Recomenda-se utilizar `in` para filtrar o tráfego antes que ele seja processado pelo switch. [cite: 30]*

-----

## Comandos de Verificação

| Comando | Descrição |
| --- | --- |
| `show running-config` | [cite\_start]Exibe a configuração atual em execução. [cite: 31, 32] |
| `show ip access-lists` | [cite\_start]Exibe todas as ACLs configuradas. [cite: 33, 34] |
| `show interfaces status` | [cite\_start]Mostra o status de todas as interfaces. [cite: 35, 36] |

-----

## Gerenciamento de Configurações

### [cite\_start]Salvar Configurações [cite: 21]

Salva a configuração em execução (`running-config`) na configuração de inicialização (`startup-config`). Execute em modo privilegiado.

```bash
[cite_start]write [cite: 22]
```

### [cite\_start]Desativar uma Configuração [cite: 37]

[cite\_start]Para desativar um comando, entre no modo de configuração apropriado e digite `no` seguido do comando que deseja remover. [cite: 38]

**Exemplos:**

```bash
# Desvincula a ACL "FILTRO_WEB" da interface onde foi aplicada
[cite_start]no ip access-group FILTRO_WEB in [cite: 39]

# Remove uma regra de "permit any any" de dentro de uma ACL
[cite_start]no permit any any [cite: 40]

# Remove o endereço IP de uma interface
[cite_start]no ip address [cite: 41]
```
```
