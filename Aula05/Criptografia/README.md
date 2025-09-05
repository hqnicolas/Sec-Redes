# Guia Prático de Criptografia com OpenSSL

Este guia demonstra operações básicas de criptografia simétrica, assimétrica e híbrida utilizando a ferramenta de linha de comando `openssl`, além de um exemplo de como gerar wordlists para testes de segurança.

## 🔐 Criptografia Simétrica

Na criptografia simétrica, a mesma chave é usada tanto para cifrar quanto para decifrar a mensagem. É um método rápido e eficiente, ideal para grandes volumes de dados.

### 1\. Preparação do Ambiente

  * Crie um diretório e um arquivo de texto para o teste.

<!-- end list -->

```bash
# Criar um diretório para os arquivos
mkdir simetrica
cd simetrica

# Criar um arquivo de teste com uma mensagem secreta
echo "Segredo: Aula de Segurança em Redes" > mensagem.txt
```

### 2\. Verificação de Integridade (Hash)

  * Antes de cifrar, vamos gerar um hash `SHA-256` do arquivo original. Isso nos permitirá verificar se o arquivo decifrado é idêntico ao original.

<!-- end list -->

```bash
# Gerar o hash do arquivo original
sha256sum mensagem.txt
```

### 3\. Cifragem

  * Cifre a mensagem usando o algoritmo **AES-256-CBC**. O OpenSSL solicitará uma senha, que será a sua chave simétrica.

<!-- end list -->

```bash
# Cifrar a mensagem com uma senha
# Você precisará digitar uma senha que será usada para a cifragem
openssl enc -aes-256-cbc -salt -pbkdf2 -in mensagem.txt -out mensagem.enc
```

> **Nota:** Usamos `-salt` para proteger contra ataques de tabela arco-íris e `-pbkdf2` para fortalecer a derivação da chave a partir da senha.

### 4\. Decifragem

  * Para decifrar, use o comando reverso, fornecendo a mesma senha utilizada na cifragem.

<!-- end list -->

```bash
# Decifrar a mensagem
# Você precisará digitar a mesma senha usada anteriormente
openssl enc -d -aes-256-cbc -pbkdf2 -in mensagem.enc -out mensagem.dec.txt
```

### 5\. Verificação Final

  * Compare o hash do arquivo original com o do arquivo decifrado. Se os hashes forem idênticos, a operação foi um sucesso e a integridade da mensagem foi mantida.

<!-- end list -->

```bash
# Verificar a integridade comparando os hashes
sha256sum mensagem.txt mensagem.dec.txt
```

-----

## 🔑 Criptografia Assimétrica

A criptografia assimétrica utiliza um par de chaves: uma **chave pública** (para cifrar) e uma **chave privada** (para decifrar). A chave pública pode ser compartilhada livremente, mas a privada deve ser mantida em segredo absoluto.

### 1\. Preparação do Ambiente

```bash
# Voltar para o diretório anterior e criar um novo
cd ..
mkdir assimetrica
cd assimetrica

# Criar um arquivo com uma mensagem
echo "Mensagem secreta: Aula de Criptografia" > msg_rsa.txt
```

### 2\. Geração do Par de Chaves (RSA 3072 bits)

  * Vamos gerar uma chave privada e, a partir dela, extrair a chave pública correspondente.

<!-- end list -->

```bash
# Gerar a chave privada (rsa_priv.pem)
openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:3072 -out rsa_priv.pem

# Proteger a chave privada, permitindo acesso apenas ao proprietário
chmod 600 rsa_priv.pem

# Extrair a chave pública (rsa_pub.pem) a partir da chave privada
openssl pkey -in rsa_priv.pem -pubout -out rsa_pub.pem
```

### 3\. Cifragem com a Chave Pública

  * A mensagem é cifrada utilizando a **chave pública**. Qualquer pessoa com esta chave pode nos enviar uma mensagem segura.

<!-- end list -->

```bash
# Cifrar a mensagem usando a chave pública do destinatário
openssl pkeyutl -encrypt \
  -pubin -inkey rsa_pub.pem \
  -in msg_rsa.txt -out msg_rsa.enc \
  -pkeyopt rsa_padding_mode:oaep \
  -pkeyopt rsa_oaep_md:sha256
```

### 4\. Decifragem com a Chave Privada

  * A mensagem só pode ser decifrada com a **chave privada** correspondente.

<!-- end list -->

```bash
# Decifrar a mensagem usando a chave privada
openssl pkeyutl -decrypt \
  -inkey rsa_priv.pem \
  -in msg_rsa.enc -out msg_rsa.dec.txt \
  -pkeyopt rsa_padding_mode:oaep \
  -pkeyopt rsa_oaep_md:sha256
```

### 5\. Verificação

  * Use o comando `diff` para comparar o arquivo original e o decifrado. Se não houver nenhuma saída, significa que os arquivos são idênticos.

<!-- end list -->

```bash
# Verificar se os arquivos são iguais
diff -s msg_rsa.txt msg_rsa.dec.txt
```

-----

## 🧬 Criptografia Híbrida

A abordagem híbrida combina o melhor dos dois mundos: a eficiência da criptografia **simétrica** para cifrar os dados e a segurança da criptografia **assimétrica** para proteger a chave simétrica.

### Lado do Remetente 📤

1.  **Preparação do Ambiente**

    ```bash
    cd ..
    mkdir hibrida
    cd hibrida
    echo "Criptografia hibrida: simetrica e assimetrica" > mensagem.txt
    ```

2.  **Gerar uma Chave de Sessão Simétrica**

      * Criamos uma chave aleatória forte que será usada apenas para esta sessão.

    <!-- end list -->

    ```bash
    openssl rand -base64 32 > sessao.pass
    ```

3.  **Cifrar a Mensagem (Simétrica)**

      * Ciframos o arquivo principal (`mensagem.txt`) com a chave de sessão, usando um método simétrico rápido (AES-256).

    <!-- end list -->

    ```bash
    openssl enc -aes-256-cbc -salt -pbkdf2 \
      -in mensagem.txt -out payload.enc \
      -pass file:./sessao.pass
    ```

4.  **Obter Chave Pública do Destinatário e Cifrar a Chave de Sessão (Assimétrica)**

      * Para este exemplo, vamos gerar um novo par de chaves. Na prática, você usaria a chave pública já conhecida do destinatário.

    <!-- end list -->

    ```bash
    # Gerar par de chaves do destinatário (simulação)
    openssl genpkey -algorithm RSA -pkeyopt rsa_keygen_bits:3072 -out rsa_priv.pem
    chmod 600 rsa_priv.pem
    openssl pkey -in rsa_priv.pem -pubout -out rsa_pub.pem

    # Cifrar a chave de sessão com a chave pública do destinatário
    openssl pkeyutl -encrypt \
      -pubin -inkey rsa_pub.pem \
      -in sessao.pass -out sessao.pass.enc \
      -pkeyopt rsa_padding_mode:oaep \
      -pkeyopt rsa_oaep_md:sha256
    ```

5.  **Enviar o Pacote**

      * O remetente envia ao destinatário os seguintes arquivos:
          * `payload.enc` (a mensagem cifrada)
          * `sessao.pass.enc` (a chave de sessão cifrada)
          * A informação do método usado (ex: AES-256-CBC+PBKDF2)

### Lado do Destinatário 📥

1.  **Decifrar a Chave de Sessão (Assimétrica)**

      * O destinatário usa sua **chave privada** para decifrar a chave de sessão.

    <!-- end list -->

    ```bash
    openssl pkeyutl -decrypt \
      -inkey rsa_priv.pem \
      -in sessao.pass.enc -out sessao.pass.dec \
      -pkeyopt rsa_padding_mode:oaep \
      -pkeyopt rsa_oaep_md:sha256
    ```

2.  **Decifrar a Mensagem (Simétrica)**

      * Com a chave de sessão decifrada em mãos, o destinatário pode finalmente decifrar a mensagem principal.

    <!-- end list -->

    ```bash
    openssl enc -d -aes-256-cbc -pbkdf2 \
      -in payload.enc -out payload.dec.txt \
      -pass file:./sessao.pass.dec
    ```

      * Agora você pode verificar o conteúdo do arquivo `payload.dec.txt`.

-----

## 🎯 Geração de Wordlists para Testes de Segurança

Esta seção descreve como usar a ferramenta `bopscrk` para criar wordlists personalizadas, que podem ser usadas em testes de penetração para quebrar hashes com ferramentas como o `Hashcat`.

### 1\. Instalação e Configuração (Ex: Kali Linux)

  * Siga os passos para configurar o ambiente Python e instalar as dependências.

<!-- end list -->

```bash
# Clone ou faça o download e descompacte o bopscrk
# Exemplo: git clone https://github.com/r3nt0n/bopscrk.git
# cd bopscrk

# Crie e ative um ambiente virtual Python
python3 -m venv bopscrk_env
source bopscrk_env/bin/activate

# Instale as dependências necessárias
pip install -r requirements.txt
```

### 2\. Execução Interativa

  * Execute o `bopscrk` no modo interativo para gerar sua wordlist personalizada com base nas informações que você fornecer sobre o alvo.

<!-- end list -->

```bash
# Execute a ferramenta
python bopscrk/bopscrk.py -i
```

### 3\. Teste de Quebra de Hash com Hashcat

  * Após gerar sua `wordlist.txt`, você pode usá-la com o Hashcat para tentar quebrar um hash.

<!-- end list -->

```bash
# Exemplo de quebra de um hash SHA-256
# -m 1400: Código do modo de hash para SHA-256
# -a 0: Modo de ataque (dicionário)
hashcat -m 1400 -a 0 hash.txt wordlist.txt
```