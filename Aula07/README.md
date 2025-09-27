# Segurança em Redes Sem Fio

> Como as redes sem fio transmitem os dados por ondas de rádio, como podemos manter um certo nível de segurança?
> Protocolos, Senhas Atualizadas, Equipamentos, etc.

---

## Objetivos

- Perceber a importância da Segurança nas Redes Sem Fio, explorando suas fraquezas e vulnerabilidades.
- Conhecer os protocolos utilizados nas Redes Sem Fio.

---

## Protocolos

### [WEP (Wired Equivalent Privacy)](https://github.com/hqnicolas/Front-End/blob/main/Aula07/Wep.md)

O WEP foi criado em 1997 e foi a primeira tentativa de proteção sem fio, criptografando os dados a fim de que, se fossem interceptados, estariam irreconhecíveis.

#### Características
- Utiliza o algoritmo **RC4** para criptografia de dados.
- Chaves de 64 ou 128 bits, sendo 40 ou 104 bits para a chave de segurança + 24 bits do vetor de inicialização (IV).
- Esse IV é calculado e anexado junto à chave.
- Todos os dispositivos na rede compartilham a mesma chave.

#### Principais Vulnerabilidades
- Tamanho do IV muito pequeno.
- Chave estática.
- RC4 vulnerável a ataques de força bruta.

### WPA (Wi-Fi Protected Access)

O WPA foi desenvolvido em 2003 como solução para melhorar o nível de segurança das redes sem fio e combater as vulnerabilidades do protocolo WEP.

#### Características
- Usa **TKIP (Temporal Key Integrity Protocol)** em vez do RC4 puro.
- **MIC (Message Integrity Check)** para garantir a integridade das mensagens.
- **Chave dinâmica**: TKIP gera uma nova chave para cada pacote, mitigando ataques de repetição.

#### Principais Vulnerabilidades
- Dependência do algoritmo RC4.
- TKIP foi projetado para hardware legado e possui fraquezas.
- Vulnerável a ataques de força bruta.

### WPA2 (Wi-Fi Protected Access 2)

O WPA2 foi lançado em 2004 com o objetivo de aprimorar a segurança do Wi-Fi. Tornou-se o padrão de segurança predominante. Como requer mais poder de computação, muitas vezes exigiu a troca do equipamento, não apenas uma atualização de firmware.

#### Características
- **AES (Advanced Encryption Standard)**: Algoritmo de criptografia muito mais robusto.
- **CCMP (Counter Mode with Cipher Block Chaining Message Authentication Code Protocol)**: Protocolo que utiliza o AES.
- **WPA2-Personal (PSK)**: Usa uma chave pré-compartilhada (senha) para acesso.
- **WPA2-Enterprise (EAP)**: Usa um servidor de autenticação (RADIUS) para autenticação individual.

#### Principais Vulnerabilidades
- **KRACK (Key Reinstallation Attacks)**: Permite que um atacante intercepte e manipule o tráfego.
- **PSK fraco**: Senhas fracas são vulneráveis a ataques de força bruta offline.

### WPA3 (Wi-Fi Protected Access 3)

Lançado em 2018, o WPA3 é a nova geração de protocolo de segurança, projetado para corrigir as vulnerabilidades encontradas no WPA2 e oferecer segurança adequada às redes modernas.

#### Características
- **SAE (Simultaneous Authentication of Equals)**: Protege contra ataques de dicionário offline, substituindo o PSK.
- **Criptografia individualizada**: Cada dispositivo na rede tem sua própria chave de criptografia, mesmo em redes abertas.
- **Proteção contra ataques de dicionário**.
- **Forward Secrecy**: Se uma chave de sessão for comprometida, não compromete as sessões futuras.

#### Status
- Ainda em processo de disseminação em dispositivos e roteadores.
- Possíveis novas vulnerabilidades ainda estão sendo estudadas.

---

## Comparativo de Protocolos

| PROTOCOLO | ALGORITMO CRIPTOGRÁFICO | VULNERABILIDADES                               | USO ATUAL      |
| :-------- | :---------------------- | :--------------------------------------------- | :------------- |
| **WEP** | RC4                     | IV repetitivo, RC4 fraco                       | Obsoleto       |
| **WPA** | RC4 + TKIP              | RC4 e TKIP vulneráveis, força bruta            | Desatualizado  |
| **WPA2** | AES + CCMP              | KRACK, PSK fraco                               | Amplamente Usado |
| **WPA3** | AES + SAE               | Em estudo                                      | Crescendo      |

---

## WPS (Wi-Fi Protected Setup)

O WPS é um protocolo projetado para simplificar o processo de conexão de dispositivos a uma rede Wi-Fi, permitindo conexões rápidas sem a necessidade de digitar senhas longas.

### Tipos de WPS

- **Botão Físico (Push Button Configuration - PBC)**: Pressiona-se o botão no roteador e no dispositivo cliente para conectar.
- **PIN (Personal Identification Number)**: Um PIN de 8 dígitos (geralmente do roteador) é inserido no dispositivo cliente.
- **NFC (Near Field Communication)**: Aproxima-se o dispositivo do roteador para conectar (menos comum).

### Vulnerabilidades do WPS

Apesar da conveniência, o WPS possui sérias vulnerabilidades, principalmente relacionadas ao método de PIN.

- **Ataque de Força Bruta no PIN**: O PIN de 8 dígitos é validado em duas metades de 4 e 3 dígitos (+ 1 checksum), reduzindo drasticamente o número de tentativas necessárias para quebrá-lo (de 10⁸ para ~11.000).
- **PIN Padrão Fraco**: Muitos roteadores usam PINs previsíveis ou baseados em informações como o endereço MAC.
- **Falta de Mecanismo de Bloqueio**: Muitos roteadores não bloqueiam tentativas de PIN após falhas repetidas, permitindo ataques contínuos.
- **Hardcoded PIN**: Alguns roteadores possuem um PIN fixo de fábrica que não pode ser alterado.

> **Recomendação**: Devido às suas vulnerabilidades, a melhor prática é **desativar o WPS** no roteador.

---

## Segurança em Redes Corporativas

### [Autenticação WPA2/WPA3-Enterprise](https://github.com/hqnicolas/Front-End/blob/main/Aula07/Wpa.md)

Diferente do modo *Personal (PSK)*, o modo *Enterprise* não usa uma única senha. Cada usuário é autenticado individualmente através de um servidor de autenticação, como o **RADIUS**.

#### Benefícios
- **Chaves de Criptografia Únicas**: Cada dispositivo recebe uma chave única, melhorando a segurança.
- **Controle Granular de Acesso**: Integra-se com sistemas de diretórios (ex: Active Directory) para gerenciar permissões.
- **Autenticação Forte com EAP-TLS**: Usa certificados digitais em vez de senhas, sendo um dos métodos mais seguros.

### Outras Medidas em Redes Corporativas

- **Implementação de VLANs**: Segrega o tráfego de rede (ex: separar departamentos ou redes de convidados).
- **Monitoramento Contínuo**: Ferramentas de detecção de intrusão (IDS/IPS) para identificar comportamentos anômalos como *Evil Twin*, *Rogue APs*, ou tráfego malicioso.
- **Redes para Convidados Isoladas**: Criar uma rede separada para visitantes, com acesso restrito apenas à internet e isolada da rede interna.
- **Atualizações Constantes**: Manter o firmware de pontos de acesso, roteadores e outros dispositivos sempre atualizados.

---

## [Principais Vulnerabilidades em Redes Sem Fio](https://github.com/hqnicolas/Front-End/blob/main/Aula07/EvilTwin.md)

| Vulnerabilidade         | Descrição                                                                                             |
| ----------------------- | ----------------------------------------------------------------------------------------------------- |
| **Sniffing de Pacotes** | Captura de tráfego de rede. Se não criptografado, dados sensíveis podem ser lidos.                       |
| **Força Bruta em PSK** | Tentar adivinhar a senha (PSK) da rede Wi-Fi através de dicionários ou combinações.                   |
| **KRACK** | *Key Reinstallation Attack*. Explora uma falha no WPA2 para forçar a reutilização de chaves e quebrar a criptografia. |
| **Evil Twin** | Um ponto de acesso falso com o mesmo nome (SSID) da rede legítima para enganar usuários e roubar dados. |
| **Ataque de Deauth** | Envio de pacotes de desautenticação para forçar um dispositivo a se desconectar e capturar a reconexão. |
| **Rogue Access Points** | Pontos de acesso não autorizados instalados na rede para interceptar tráfego.                         |

### Como se Proteger?

- **Sniffing**: Use criptografia forte (WPA3/WPA2-AES) e VPNs, especialmente em redes públicas.
- **Força Bruta em PSK**: Use senhas longas, complexas e exclusivas. Migre para WPA3, que é resistente a esse ataque.
- **KRACK**: Mantenha todos os seus dispositivos (roteadores, smartphones, laptops) atualizados com os últimos patches de segurança.
- **Evil Twin**: Desative a conexão automática a redes conhecidas e use uma VPN. Verifique a autenticidade da rede.
- **Deauth**: O WPA3 oferece maior proteção contra este tipo de ataque. Sistemas de monitoramento de rede podem detectar esses eventos.
- **Rogue APs**: Em ambientes corporativos, use monitoramento de rede e autenticação WPA2/WPA3-Enterprise para garantir que apenas APs autorizados operem.

---

## Melhores Práticas de Segurança

- ✅ **Usar WPA3**: Se disponível, habilite o WPA3 para a segurança mais robusta.
- 🔑 **Senhas Fortes e Complexas**: Crie senhas longas com uma mistura de caracteres.
- 🏢 **WPA2/WPA3-Enterprise**: Em empresas, use autenticação baseada em servidor RADIUS.
- 🔄 **Atualizar Firmware**: Mantenha roteadores e dispositivos sempre atualizados.
- 🚫 **Desativar WPS**: Desabilite o Wi-Fi Protected Setup para evitar ataques de força bruta.
- 🌐 **Rede para Convidados**: Crie uma rede separada e isolada para visitantes.
- 🛡️ **Utilizar VPN**: Adiciona uma camada extra de criptografia, essencial em redes públicas.
- 🔍 **Monitoramento**: Monitore a rede para atividades suspeitas.
- 🔒 **Ativar o Firewall do Roteador**: Garante uma barreira básica de proteção.
- 🏡 **Filtro de MAC**: Permite que apenas dispositivos conhecidos se conectem (pode ser contornado, mas adiciona uma camada).
- 🤫 **Ocultar SSID**: Dificulta a descoberta da rede (segurança por obscuridade, não uma medida forte).
- リモート **Desativar Gerenciamento Remoto**: Evite que seu roteador seja acessado pela internet.

---

## Segurança em Dispositivos IoT (Internet of Things)

Dispositivos IoT são frequentemente alvos fáceis devido à falta de foco em segurança durante seu desenvolvimento. Um dispositivo comprometido pode ser uma porta de entrada para a rede inteira.

### Principais Vulnerabilidades em IoT
- **Falta de Atualizações**: Muitos fabricantes não fornecem patches de segurança.
- **Autenticação Fraca**: Senhas padrão como "admin/admin" são comuns e raramente alteradas.
- **Conexões Não Seguras**: Transmissão de dados em texto plano, sem criptografia.
- **Falta de Segmentação de Rede**: Dispositivos IoT muitas vezes estão na mesma rede que sistemas críticos.

### Melhores Práticas para IoT
- **Atualizações Regulares**: Compre dispositivos de fabricantes que oferecem suporte e atualizações contínuas.
- **Credenciais Fortes**: Altere imediatamente as senhas padrão e use senhas fortes.
- **Criptografia de Dados**: Prefira dispositivos que criptografam a comunicação.
- **Segmentação de Rede**: Isole os dispositivos IoT em uma VLAN ou rede separada.
- **Monitoramento**: Monitore o tráfego dos dispositivos IoT para detectar comportamentos anômalos.

---

## WIDS e WIPS (Sistemas de Detecção e Prevenção de Intrusão Sem Fio)

### WIDS (Wireless Intrusion Detection System)
É um sistema projetado para **detectar** intrusões, atividades suspeitas ou maliciosas em redes sem fio. Ele monitora o espectro de rádio em busca de ameaças e **alerta** os administradores.

### WIPS (Wireless Intrusion Prevention System)
É uma extensão do WIDS. Além de **detectar**, o WIPS pode tomar ações automáticas para **prevenir** e mitigar ataques em tempo real.

#### Funcionalidades do WIPS
- **Bloqueio Automático**: Impede que dispositivos não autorizados se conectem.
- **Desautenticação de Ameaças**: Desconecta clientes maliciosos ou não autorizados.
- **Isolamento**: Isola dispositivos suspeitos para que não possam atacar outros na rede.
- **Proteção contra Man-in-the-Middle (MITM)** e **Denial of Service (DoS)**.
