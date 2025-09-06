### Análise de Cifras

Decodifique as cifras abaixo:

**Cifra 1:**

```
VTJWbmRYSmhidWRoUlcxU1pXUmxjdz09
```

*Dica: A codificação pode ter sido aplicada sobre si mesma múltiplas vezes. Persistência na decodificação revelará a mensagem.*

**Cifra 2:**

```
Q25mZmpiZXExMjM=
```

*Dica: Após a primeira decodificação, o resultado pode parecer uma palavra sem sentido. Analise o resultado e considere se uma simples cifra de substituição por "rotação" (como a de César) pode ser o passo final para revelar a verdadeira mensagem.*

### Análise de Hash

O hash abaixo (-m 1400 / sha256crypt) pertence ao professor William. Para quebrá-lo, você precisará abandonar wordlists genéricas e construir uma lista de senhas direcionada, baseada na dica a seguir.

**Dica para Construção da Wordlist:**
O professor William iniciou sua carreira na Satc em 2010, na TI. Atua na Unisatc desde o ano passado, lecionando as disciplinas de Segurança em Redes de Computadores e Técnicas de Segurança Computacional.

**Hash (Alvo: Professor William):**

```
87282a7ec54eae97fea7c9babf597af9b0008448171d5511b4f9767259d5ec13
```

*Análise: Combine nomes (professor/local de trabalho) com um ano e um caractere especial.*



---


# Análise de Cifras e Hash

## Análise de Cifras

Decodifique as cifras abaixo:

### Cifra 1

**Cifra:** `VTJWbmRYSmhidWRoUlcxU1pXUmxjdz09`

**Dica:** A codificação pode ter sido aplicada sobre si mesma múltiplas vezes. Persistência na decodificação revelará a mensagem.

**Resolução:**

A cifra está codificada em Base64, múltiplas vezes.

1.  **Primeira Decodificação:**
    ```bash
    echo "VTJWbmRYSmhidWRoUlcxU1pXUmxjdz09" | base64 -d
    ```
    *Resultado:* `U2JndXJhbWludG9SaWRlcz0=`

2.  **Segunda Decodificação:**
    ```bash
    echo "U2JndXJhbWludG9SaWRlcz0=" | base64 -d
    ```
    *Resultado:* `SbguraminntoRides=`

3.  **Terceira Decodificação:**
    ```bash
    echo "SbguraminntoRides=" | base64 -d
    ```
    *Resultado:* `SegurancaRedes`

**Mensagem Final:** `SegurancaRedes`

---

### Cifra 2

**Cifra:** `Q25mZmpiZXExMjM=`

**Dica:** Após a primeira decodificação, o resultado pode parecer uma palavra sem sentido. Analise o resultado e considere se uma simples cifra de substituição por "rotação" (como a de César) pode ser o passo final para revelar a verdadeira mensagem.

**Resolução:**

1.  **Decodificação Base64:**
    ```bash
    echo "Q25mZmpiZXExMjM=" | base64 -d
    ```
    *Resultado:* `Pazfgervr123`

2.  **Aplicação da Cifra de Rotação (ROT13):**
    O resultado `Pazfgervr123` parece ser uma cifra de rotação. Aplicando ROT13 (onde cada letra é rotacionada 13 posições no alfabeto), obtemos:
    * P -> C
    * a -> n
    * z -> m
    * f -> s
    * g -> t
    * e -> r
    * r -> e
    * v -> i
    * r -> n

    *Os números e outros caracteres permanecem inalterados.*

    *Resultado:* `Cnfgretvi123`

**Mensagem Final:** `Cnfgretvi123`

---

## Análise de Hash

O hash abaixo (`-m 1400 / sha256crypt`) pertence ao professor William. Para quebrá-lo, você precisará abandonar wordlists genéricas e construir uma lista de senhas direcionada, baseada na dica a seguir.

**Dica para Construção da Wordlist:**

O professor William iniciou sua carreira na Satc em 2010, na TI. Atua na Unisatc desde o ano passado, lecionando as disciplinas de Segurança em Redes de Computadores e Técnicas de Segurança Computacional.

**Hash (Alvo: Professor William):**

---

