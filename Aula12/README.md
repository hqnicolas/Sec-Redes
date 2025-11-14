# Monitoramento de Ativos de TI

> Gerenciar a infraestrutura de TI com eficiência exige mais do que apenas garantir que os servidores estejam funcionando. É crucial monitorar o desempenho, a disponibilidade e a segurança de todos os ativos de TI.

---

## 🎯 Objetivos

* Reconhecer a relevância do monitoramento de ativos, sua análise e alertas.
* Atividade Prática.

---

## 💡 Conceito

### Acompanhamento e Gerenciamento Constante dos Ativos
Coleta contínua de dados sobre o status e desempenho de ativos de TI, como servidores, redes, aplicações e dispositivos.

### Observação e Análise de Métricas
Utilização de ferramentas e dashboards para visualizar dados de monitoramento, identificar tendências e tomar decisões informadas.

---

## 📈 Importância

* **Prever Falhas:** Identificar problemas potenciais antes que causem interrupções.
* **Reduzir Tempo de Inatividade:** Diagnosticar e resolver falhas rapidamente.
* **Gestão Estratégica:** Obter insights para planejamento e otimização de recursos.

---

## 🏆 Vantagens

1.  **Detecção Precoce:** Identificar anomalias no início.
2.  **Notificação em Tempo Real:** Receber alertas imediatos sobre eventos críticos.
3.  **Planejamento de Upgrades:** Basear decisões de upgrade em dados de desempenho reais.
4.  **Otimização de Custos com TI:** Alocar recursos de forma mais eficiente.
5.  **Reconhecimento de Ameaças de Segurança:** Monitorar tráfego e logs em busca de atividades suspeitas.

---

## 📡 Protocolos para Coletas de Dados

Os principais protocolos usados para a coleta de dados de monitoramento incluem:

* SNMP (Simple Network Management Protocol)
* ICMP (Internet Control Message Protocol)
* NetFlow e sFlow

---

### 1. SNMP (Simple Network Management Protocol)

O SNMP é um dos protocolos mais comuns para gerenciamento e monitoramento de dispositivos de rede.

* **Operação:** Funciona sobre o protocolo **UDP** (User Datagram Protocol), o que proporciona uma comunicação rápida e eficiente.
* **Porta Padrão:** Utiliza a **porta 161** para a comunicação.

#### Componentes do SNMP

* **Manager:** O sistema (geralmente um servidor) responsável por monitorar e controlar os dispositivos gerenciados na rede.
* **Agent:** Um software que roda nos dispositivos gerenciados (como roteadores, switches, servidores) e é responsável por coletar e fornecer informações ao Manager.
* **MIB (Management Information Base):** Uma estrutura hierárquica, como um banco de dados, que define os dados (objetos) que podem ser coletados e gerenciados via SNMP.


#### Métodos de Coleta SNMP

* **Polling (Coleta):** Método onde o Manager solicita periodicamente informações aos Agents. Permite um monitoramento constante e programado.
* **Traps (Alertas):** Mensagens assíncronas enviadas pelos Agents ao Manager quando ocorrem eventos específicos ou críticos (ex: falha de um link).

---

### 2. ICMP (Internet Control Message Protocol)

O ICMP é usado principalmente para diagnósticos de rede.

* Verifica o **Status** e a **Conectividade** de dispositivos.
* Mede o **Tempo de Resposta** (latência).
* É a base de ferramentas essenciais como `Ping` e `Traceroute`.

---

### 3. NetFlow e sFlow

Estes protocolos são focados na análise de tráfego de rede.

#### NetFlow
* Tecnologia desenvolvida pela **Cisco**.
* Fornece **dados detalhados** sobre o fluxo de tráfego de rede.
* Usado para **análise avançada** de quem está falando com quem, por qual porta e quanto de dados está sendo transferido.

#### sFlow
* Utiliza **amostragem de dados** (sampling) em vez de capturar todo o fluxo.
* É muito eficaz em redes com **grande volume de dados**, pois exige menos recursos dos dispositivos.

---

## 🕵️ Agentes para Coleta de Dados

* **Agente SNMP:** Software embutido na maioria dos dispositivos de rede (roteadores, switches) que implementa o protocolo SNMP, permitindo a coleta de dados.
* **Agente Específico da Ferramenta:** Software customizado, desenvolvido especificamente para uma ferramenta de monitoramento (como Zabbix ou Nagios). Geralmente oferece recursos mais avançados e personalizados de coleta de dados do que o SNMP padrão.

---

## 🛠️ Ferramentas de Monitoramento

Existe uma vasta gama de ferramentas disponíveis, desde projetos open source até soluções comerciais robustas.

### Ferramentas Gratuitas (Open Source)
* Zabbix
* Observium
* The Dude
* Nagios
* Prometheus

### Ferramentas Pagas (Comerciais)
* SolarWinds
* OpManager
* PRTG
