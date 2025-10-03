# ACL (Access Control List)

## Objetivos

Conhecer as listas de controle de acessos em Switches e Roteadores.

## O que é uma ACL?

Listas de Controle de Acesso (ACLs) são regras aplicadas a dispositivos de rede, como roteadores e switches, para permitir ou negar o tráfego de rede com base em critérios específicos, como endereços IP, protocolos ou portas. Elas são fundamentais para filtrar e controlar o acesso a recursos em um ambiente de rede.

## Onde são Utilizadas

* **Roteadores e switches**: ACLs são aplicadas para controlar o tráfego entre sub-redes ou segmentos de rede.
* **Firewalls**: ACLs definem as regras de permissão para tráfego de entrada e saída.
* **Sistemas operacionais**: ACLs são usadas para controlar o acesso a recursos do sistema, como arquivos e diretórios.

## Vantagens

* **Controle Granular**: Permite definir regras específicas para controlar o tráfego.
* **Segurança Adicional**: Filtra o tráfego indesejado ou malicioso antes de atingir recursos críticos.
* **Flexibilidade**: Pode ser configurada em diversos dispositivos e sistemas, fornecendo uma camada adicional de segurança.

## Desvantagens

* **Complexidade**: Manter e gerenciar grandes conjuntos de ACLs pode se tornar difícil.
* **Desempenho**: ACLs muito extensas podem impactar a performance de dispositivos de rede.
* **Falta de Detecção de Ameaças**: ACLs não identificam padrões de ataques mais avançados, como ataques DDoS ou malware.

## Importância para a Segurança

1.  **Proteção contra acessos não autorizados**.
2.  **Redução da superfície de ataque**: Reduzir a superfície de ataque, permitindo apenas o tráfego necessário.
3.  **Melhoria na segmentação da rede**: Melhorar a segmentação da rede, impedindo que hosts comprometam partes críticas da infraestrutura.

## Tipos de ACL

### 1. ACL Padrão

Baseada apenas no endereço IP de origem. Permite ou nega o tráfego com base em endereços IP de origem.

**Exemplo de comando no Cisco:**
```

access-list 1 permit 192.168.1.0 0.0.0.255

```

### 2. ACL Estendida

Mais avançada, permite especificar endereços IP de origem e destino, portas e protocolos.

**Exemplo de Comando:**
```

access-list web permit tcp 192.168.1.0 0.0.0.255 any eq 80

```

### 3. ACL Baseada em Tempo

Define regras com base em períodos de tempo.

**Configuração:**
```

time-range work-hours
periodic weekdays 8:00 to 18:00

```

**Aplicação:**
```

access-list 101 permit ip any any time-range work-hours

```
