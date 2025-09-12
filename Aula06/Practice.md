# Guia de Assinatura e Criptografia com GPG

Este guia demonstra os passos para assinar, verificar, criptografar e descriptografar arquivos entre duas máquinas (PC-01 e PC-02) usando GPG, garantindo autenticidade, integridade e confidencialidade.

## 1\. Assinatura de Arquivos (Garantindo Autenticidade e Integridade)

Este processo garante que o arquivo não foi modificado (integridade) e que foi realmente enviado pelo remetente esperado (autenticidade).

### No PC-01

1.  **Criar um arquivo de exemplo:**

    ```bash
    nano arquivo-pc1.txt
    ```

    *(Escreva qualquer conteúdo dentro do arquivo e salve-o.)*

2.  **Gerar o hash (checksum) do arquivo:**
    O hash é uma impressão digital única do arquivo.

    ```bash
    sha256sum arquivo-pc1.txt > arquivo-pc1.txt.sum
    ```

3.  **Criar um par de chaves GPG (pública e privada):**
    (Se você ainda não tiver um)

    ```bash
    gpg --full-gen-key
    ```

4.  **Assinar o arquivo de hash com sua chave privada:**
    Isso cria um novo arquivo `.gpg` que serve como prova de autoria.

    ```bash
    gpg -s arquivo-pc1.txt.sum
    ```

5.  **Exportar sua chave pública:**
    A chave pública será usada pelo PC-02 para verificar sua assinatura.

    ```bash
    gpg --export -a SEU_EMAIL@exemplo.com > chave-pc1.asc
    ```

6.  **Compartilhar os arquivos:**
    Inicie um servidor web simples para que o PC-02 possa baixar os arquivos.

    ```bash
    python -m http.server 8000
    ```

    *Arquivos a serem compartilhados: `arquivo-pc1.txt`, `arquivo-pc1.txt.sum.gpg`, `chave-pc1.asc`.*

-----

### No PC-02

1.  **Baixar os arquivos** do servidor web do PC-01.

2.  **Importar a chave pública do PC-01:**

    ```bash
    gpg --import chave-pc1.asc
    ```

3.  **Verificar a assinatura (Autenticidade):**
    Este comando usa a chave pública importada para confirmar que a assinatura no arquivo `.gpg` é válida.

    ```bash
    gpg arquivo-pc1.txt.sum.gpg
    ```

    *O GPG irá extrair o arquivo `arquivo-pc1.txt.sum` se a assinatura for válida.*

4.  **Verificar a integridade do arquivo original:**
    Compare o hash do arquivo recebido com o hash que estava dentro do arquivo de assinatura.

    ```bash
    # Visualizar o hash original enviado pelo PC-01
    cat arquivo-pc1.txt.sum

    # Gerar o hash do arquivo recebido
    sha256sum arquivo-pc1.txt
    ```

    *Se os dois hashes forem idênticos, a integridade do arquivo está confirmada.*

-----

*(O processo inverso, do PC-02 para o PC-01, segue exatamente os mesmos passos, apenas trocando os nomes dos arquivos e das chaves.)*

## 2\. Criptografar e Assinar Arquivos (Confidencialidade)

Este processo combina a assinatura (autenticidade e integridade) com a criptografia (confidencialidade), garantindo que apenas o destinatário correto possa ler o conteúdo.

### No PC-01

*Pré-requisito: O PC-01 já deve ter importado a chave pública do PC-02.*

1.  **Criar um arquivo confidencial:**

    ```bash
    nano arquivo-pc1-crip.txt
    ```

    *(Escreva um segredo dentro do arquivo e salve-o.)*

2.  **Criptografar e Assinar:**

      - `-e`: Criptografa (Encrypt).
      - `-s`: Assina (Sign).
      - `-a`: Gera uma saída em formato de texto (ASCII Armor).
      - `-r`: Especifica o destinatário (Recipient).

    <!-- end list -->

    ```bash
    gpg -e -s -a -r EMAIL_DO_PC02@exemplo.com arquivo-pc1-crip.txt
    ```

    *Isso criptografa o arquivo com a chave pública do PC-02 e assina com a chave privada do PC-01.*

3.  **Compartilhar o arquivo criptografado (`arquivo-pc1-crip.txt.asc`)** usando o servidor web.

-----

### No PC-02

1.  **Baixar o arquivo criptografado** (`arquivo-pc1-crip.txt.asc`).

2.  **Descriptografar e Validar a Assinatura:**
    O GPG usará a chave privada do PC-02 para descriptografar e a chave pública (já importada) do PC-01 para verificar a assinatura.

    ```bash
    gpg -d arquivo-pc1-crip.txt.asc
    ```

    *Será solicitada a senha da sua chave privada para completar o processo.*

-----

*(O processo inverso, do PC-02 para o PC-01, segue os mesmos passos.)*

## 3\. Comandos Úteis de Gerenciamento de Chaves

  * **Listar chaves privadas:**

    ```bash
    gpg --list-secret-keys
    ```

  * **Listar chaves públicas:**

    ```bash
    gpg --list-keys
    ```

  * **Apagar uma chave secreta:**

    ```bash
    gpg --delete-secret-key SEU_EMAIL@exemplo.com
    ```

  * **Apagar uma chave pública:**

    ```bash
    gpg --delete-key SEU_EMAIL@exemplo.com
    ```

## 4\. Estabelecendo um Nível de Confiança na Chave

Para evitar avisos do GPG, você pode definir explicitamente que confia em uma chave importada.

1.  **Editar a chave importada:**
    (Use os últimos 8 ou mais dígitos do ID da chave, que pode ser encontrado com `gpg --list-keys`)

    ```bash
    gpg --edit-key ID_DA_CHAVE
    ```

2.  **Dentro do prompt do GPG:**

      - Digite `trust` e pressione Enter.
      - Selecione o nível de confiança (ex: `5` para "confio plenamente").
      - Digite `sign` para assinar a chave com a sua própria, confirmando sua validade.
      - Digite `quit` para salvar e sair.

3.  **Verificar novamente:**
    Agora, ao verificar uma assinatura, o GPG não exibirá mais avisos sobre a confiança da chave.

    ```bash
    gpg --verify ARQUIVO.gpg
    ```

## 5\. Integração com Cliente de E-mail (Thunderbird)

1.  **Instalar o Thunderbird:**

    ```bash
    sudo apt install thunderbird
    ```

2.  **Configurar OpenPGP no Thunderbird:**

      - Vá para `Configurações de Conta` (`Account Settings`).
      - Selecione a aba `Criptografia de ponta a ponta` (`End-To-End Encryption`).
      - Na seção OpenPGP, clique em `Adicionar chave...` (`Add Key...`) e importe sua chave GPG existente.

-----

*Referência: Baseado no conteúdo do TryHackMe | Quebrando a criptografia da maneira simples.*
