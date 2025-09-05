# 🕵️‍♂️ Steghide: Guia Completo para Esteganografia

Bem-vindo ao guia completo do **Steghide**, uma poderosa ferramenta de esteganografia que permite esconder dados secretos em diversos tipos de arquivos de imagem e áudio. Com este tutorial, você aprenderá a instalar e utilizar o Steghide em ambientes Linux e Windows para proteger suas informações.

## Índice

  - [O que é Esteganografia?](https://www.google.com/search?q=%23o-que-%C3%A9-esteganografia)
  - [Como o Steghide Funciona?](https://www.google.com/search?q=%23como-o-steghide-funciona)
  - [Instalação](https://www.google.com/search?q=%23instala%C3%A7%C3%A3o)
      - [🐧 Linux (Debian/Ubuntu)](https://www.google.com/search?q=%23-linux-debianubuntu)
      - [💻 Windows](https://www.google.com/search?q=%23-windows)
  - [Como Usar o Steghide](https://www.google.com/search?q=%23como-usar-o-steghide)
      - [Escondendo uma Mensagem (Embed)](https://www.google.com/search?q=%23escondendo-uma-mensagem-embed)
      - [Extraindo uma Mensagem (Extract)](https://www.google.com/search?q=%23extraindo-uma-mensagem-extract)
  - [Verificando a Integridade dos Arquivos](https://www.google.com/search?q=%23verificando-a-integridade-dos-arquivos)
  - [Exemplo Prático](https://www.google.com/search?q=%23exemplo-pr%C3%A1tico)
  - [Comandos Úteis](https://www.google.com/search?q=%23comandos-%C3%BAteis)

## O que é Esteganografia?

Esteganografia é a arte e a ciência de escrever mensagens ocultas de tal forma que ninguém, além do remetente e do destinatário, suspeite da existência da mensagem. Diferente da criptografia, que oculta o *conteúdo* de uma mensagem, a esteganografia oculta a *própria existência* da mensagem.

## Como o Steghide Funciona?

O Steghide utiliza técnicas avançadas para embutir dados em arquivos de imagem (como JPEG, BMP, PNG) ou áudio (WAV, AU), alterando os pixels ou amostras de áudio de forma imperceptível ao olho ou ouvido humano. Ele também criptografa os dados antes de embuti-los para uma camada extra de segurança.

## Instalação

### 🐧 Linux (Debian/Ubuntu)

A instalação no Linux é simples e pode ser feita através do gerenciador de pacotes `apt`.

```bash
# Atualize a lista de pacotes
sudo apt-get update

# Instale o Steghide
sudo apt-get install steghide -y
```

### 💻 Windows

Para o Windows, é necessário baixar o executável e, opcionalmente, adicioná-lo ao PATH do sistema para facilitar o uso.

1.  **Baixe o Steghide:**
    Faça o download da versão mais recente no [SourceForge](https://sourceforge.net/projects/steghide/files/latest/download).

2.  **Extraia os arquivos:**
    Descompacte o arquivo `.zip` em uma pasta de sua preferência (por exemplo, `C:\Program Files\steghide`).

3.  **Adicione ao PATH (Opcional, mas recomendado):**

      * Pesquise por "Variáveis de ambiente" no menu Iniciar.
      * Clique em "Variáveis de Ambiente...".
      * Na seção "Variáveis do sistema", encontre e selecione a variável `Path` e clique em "Editar".
      * Clique em "Novo" e adicione o caminho para a pasta onde você extraiu o `steghide.exe` (ex: `C:\Program Files\steghide\bin`).
      * Clique em "OK" em todas as janelas para salvar.

    Se não adicionar ao PATH, você precisará navegar até o diretório do Steghide via terminal ou usar o caminho completo do executável (`C:\path\to\steghide.exe`) em todos os comandos.

## Como Usar o Steghide

O uso básico do Steghide envolve dois processos principais: embutir (esconder) e extrair dados.

### Escondendo uma Mensagem (Embed)

Para esconder um arquivo de texto (`mensagem_secreta.txt`) dentro de uma imagem (`imagem_original.jpg`):

  - `-cf` (cover file): O arquivo que será usado para esconder a mensagem.
  - `-ef` (embed file): O arquivo com a mensagem que você quer esconder.
  - `-p`: Solicita uma senha (passphrase) para proteger os dados.

**Comando:**

```bash
steghide embed -cf imagem_original.jpg -ef mensagem_secreta.txt
```

O Steghide solicitará uma senha. **Guarde-a bem\!** Sem ela, será impossível extrair os dados. Após o processo, uma nova imagem (ou a original modificada, dependendo da versão) será criada. Para evitar sobrescrever a original, você pode especificar um novo nome de arquivo com o parâmetro `-sf`.

```bash
steghide embed -cf imagem_original.jpg -ef mensagem_secreta.txt -sf imagem_modificada.jpg
```

### Extraindo uma Mensagem (Extract)

Para extrair a mensagem escondida de uma imagem (`imagem_modificada.jpg`):

  - `-sf` (stego file): O arquivo que contém a mensagem oculta.

**Comando:**

```bash
steghide extract -sf imagem_modificada.jpg
```

Você precisará fornecer a mesma senha que usou para embutir os dados. O arquivo (`mensagem_secreta.txt`) será extraído no mesmo diretório.

## Verificando a Integridade dos Arquivos

É uma boa prática verificar se a imagem original e a modificada são diferentes. Para isso, você pode gerar um hash criptográfico (como SHA256) para cada uma delas.

#### 🐧 Linux

```bash
sha256sum imagem_original.jpg
sha256sum imagem_modificada.jpg
```

#### 💻 Windows (usando o `certutil`)

```powershell
certutil -hashfile imagem_original.jpg SHA256
certutil -hashfile imagem_modificada.jpg SHA256
```

Os hashes devem ser diferentes, confirmando que a imagem foi alterada para incluir os dados ocultos.

## Exemplo Prático

Vamos simular um cenário completo no Windows.

1.  **Crie os arquivos:**

      * Tenha uma imagem chamada `gato.jpg`.
      * Crie um arquivo de texto chamado `segredo.txt` com a mensagem: "Encontro ao meio-dia na praça."

2.  **Navegue até a pasta:**
    Abra o terminal (CMD ou PowerShell) e vá para a pasta onde estão os seus arquivos.

3.  **Esconda a mensagem:**

    ```bash
    # Lembre-se de usar "steghide.exe" se não estiver no PATH
    steghide embed -cf gato.jpg -ef segredo.txt -sf gato_com_segredo.jpg
    ```

    Digite uma senha segura quando solicitado.

4.  **Verifique a diferença (opcional):**

    ```powershell
    certutil -hashfile gato.jpg SHA256
    certutil -hashfile gato_com_segredo.jpg SHA256
    ```

5.  **Extraia a mensagem (em outro local, para simular o recebimento):**
    Imagine que você enviou `gato_com_segredo.jpg` para um amigo. Ele faria o seguinte:

    ```bash
    steghide extract -sf gato_com_segredo.jpg
    ```

    Após digitar a senha correta, o arquivo `segredo.txt` aparecerá na pasta.

## Comandos Úteis

  - **Ver informações sobre um arquivo stego:**
    ```bash
    steghide info imagem_modificada.jpg
    ```
  - **Usar um nível de compressão (1 a 9):**
    ```bash
    steghide embed -cf imagem.jpg -ef segredo.txt -z 9
    ```
  - **Não criptografar os dados (não recomendado):**
    ```bash
    steghide embed -cf imagem.jpg -ef segredo.txt -e none
    ```

-----

*Este guia foi criado para fins educacionais. Use a esteganografia de forma responsável.*
