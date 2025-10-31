# Firewall
## Objetivos

* Entender o funcionamento de um firewall
* Tipos de firewall
* Regras/Políticas
* Prática com pfSense e Fortigate

## O que é um Firewall?

Um firewall atua como uma **barreira**, realizando a **filtragem de tráfego** com base em **regras** predefinidas.

### Objetivo Principal

* Bloqueio de acesso não autorizado
* Autorização de comunicações legítimas

### Funções

1.  **Filtragem de pacotes:** Baseado em IP e porta.
2.  **Controle de acesso:** Baseado em Serviços.

## Funcionamento

1.  Inspeção de Pacotes
2.  Filtros baseados em Políticas
3.  Logs e Monitoramento

## Importância

* **Segurança Proativa:** Atua como a 1ª Linha de Defesa.
* **Proteção:** Contra ataques e vulnerabilidades conhecidas.
* **Prevenção de Ameaças:** Evita danos de usuários ou dispositivos maliciosos.
* **Gerenciamento de Tráfego:** Permite a priorização de tráfego.

## Tipos de Firewall

### 1. Firewall de Filtragem de Pacotes

* Básico
* Simples
* Rápido
* Seguro? (Questionável)

### 2. Firewall UTM (Unified Threat Management)

* Gestão Unificada de Ameaças
* Possui Funções de Segurança Adicionais

### 3. Firewall de Próxima Geração (NGFW)

* **Recursos Avançados:** Funções além da filtragem básica.
* **Análise Profunda:** Inspeção profunda de pacotes (DPI).
* **Controle de Aplicações:** Gerencia o acesso por aplicativo, não apenas por porta.
* **Monitoramento de Usuários:** Integração com identidade de usuários.

## Implementações de Firewall

* **Hardware:**
    * Equipamentos físicos dedicados.
    * Comum em meio corporativo.
* **Software:**
    * Rodam em algum servidor (físico ou virtual).

## Onde podem ser utilizados?

Os firewalls são ferramentas essenciais de segurança que podem ser utilizados em diversos contextos para proteger redes e sistemas contra ameaças cibernéticas.

* **Redes Corporativas:**
    * Proteção de dados
    * Aplicação de Políticas de Segurança
* **Redes Domésticas:**
    * Proteção dos equipamentos residenciais (PCs, smart Tvs, IoT).
* **Sistemas Pessoais (Host-based):**
    * Bloqueio de conexões indesejadas em PCs.
    * Controla o tráfego dos programas instalados.

## Exemplos de Firewall

### Soluções Pagas

* **Palo Alto Networks:** Reconhecida por suas soluções de segurança de próxima geração (NGFW).
* **Checkpoint:** Oferece uma ampla gama de produtos de segurança cibernética.
* **Fortinet (Fortigate):** Conhecida por seus firewalls de alto desempenho (UTM/NGFW) e recursos avançados.

### Soluções Gratuitas / Open Source

* **IPtables:** Firewall nativo do Linux (filtragem de pacotes).
* **pfSense:** Solução de firewall completa baseada em FreeBSD.
* **OPNSense:** Um fork do pfSense com recursos adicionais e ciclo de desenvolvimento diferente.

## Como saber qual utilizar?

1.  **Necessidades:** Avalie suas necessidades específicas de segurança e escalabilidade.
2.  **Indispensável:** Determine quais recursos de segurança são absolutamente essenciais para sua rede ou sistema.
3.  **Recursos financeiros:** Considere seu orçamento e os recursos financeiros disponíveis para investir em uma solução de firewall.

---

## Foco: IPTables

O IPTables é um firewall de filtragem de pacotes, baseado em regras, que utiliza o framework Netfilter no kernel do Linux.

### Estrutura do IPTables

1.  **Tabelas:** O nível mais alto de organização. Agrupam chains por funcionalidade.
2.  **Chains (Correntes):** Listas de regras dentro de cada tabela.
3.  **Regras:** Instruções específicas para o tratamento dos pacotes.

### Tabelas Principais

* **Filter:** Determina o que entra e o que sai na máquina localmente. É a tabela padrão.
* **Nat:** Usada para Tradução de Endereços de Rede (ex: compartilhar internet).
* **Mangle:** Para alterações especiais nos pacotes (QoS, MTU, TTL).
* **Raw:** Utilizada para configurar exceções (pacotes que não devem ser processados pelo "connection tracking").
* **Security:** Usada para controle de MAC (Mandatory Access Control, ex: SELinux).

### Chains por Tabela (Comuns)

| Tabela | Chains |
| :--- | :--- |
| **Filter** | `INPUT`, `OUTPUT` e `FORWARD` |
| **Nat** | `PREROUTING`, `POSTROUTING`, `INPUT` e `OUTPUT` |
| **Mangle** | `PREROUTING`, `POSTROUTING`, `INPUT`, `OUTPUT` e `FORWARD` |
| **Raw** | `PREROUTING` e `OUTPUT` |
| **Security**| `INPUT`, `OUTPUT` e `FORWARD` |

### Ações (Targets)

* **ACCEPT:** Permite o pacote.
* **DROP:** Recusa o pacote silenciosamente (sem dar nenhum retorno/resposta).
* **REJECT:** Recusa o pacote, mas devolve um erro/mensagem ao remetente.

### Exemplo de Comando

O comando abaixo bloqueia todo o tráfego encaminhado (FORWARD) para a rede `157.240.0.0/16`.

```bash
iptables -t filter -A FORWARD -d 157.240.0.0/16 -j DROP

Tabela (-t): filter

Chain (-A): FORWARD (Append/Adicionar regra)

Condição (-d): Destino 157.240.0.0/16

Ação (-j): DROP
```

Foco: Outras Soluções
pfSense
Pode ser considerado um Firewall UTM? Sim, especialmente com o uso de Plugins (ex: Snort para IDS/IPS, Squid para Proxy).

Baseado em FreeBSD.

Fortigate
Classificado como Firewall UTM e Firewall NGFW.

Troubleshooting (Perguntas)
P: Instalei um Firewall e percebi que a rede ficou lenta. E agora?
Causa Possível:

Solução:

P: Mesmo com um Firewall, tenho suspeita de acesso não autorizado. O que faço?
Solução:

P: Instalei um NGFW e percebi que algumas aplicações críticas pararam (estão bloqueadas). O que será?
Possível Problema:

Solução:
