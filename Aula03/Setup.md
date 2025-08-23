# Instalação e Configuração do VSFTPD

---

## 1. Instalação do Servidor VSFTPD

```bash
sudo apt install vsftpd
````

Instala o VSFTPD no sistema que será utilizado para gerenciar o servidor FTP.

## 2\. Criação do Usuário para Acesso ao FTP

```bash
sudo useradd -m ftpuser
sudo passwd ftpuser
```

Cria um usuário chamado **ftpuser** com um diretório `home` e define a senha para login via FTP.

## 3\. Estruturação dos Diretórios e Permissões para o FTP

```bash
sudo cd /home/ftpuser
sudo mkdir ftp
sudo chown nobody:nogroup /home/ftpuser/ftp
sudo chmod a-w /home/ftpuser/ftp
sudo cd ftp
sudo mkdir files
sudo chown ftpuser:ftpuser /home/ftpuser/ftp/files
```

Cria a pasta `ftp` e a pasta `files`, configurando permissões para segurança e acesso do usuário **ftpuser**.

## 4\. Criação de um Arquivo de Exemplo

```bash
echo "Arquivo de Exemplo do FTP" | sudo tee /home/ftpuser/ftp/files/exemplo.txt
```

Cria um arquivo de teste chamado `exemplo.txt` dentro do diretório `files`.

## 5\. Backup do Arquivo de Configuração Original

```bash
sudo cp /etc/vsftpd.conf /etc/vsftpd.conf_default
```

Faz um backup do arquivo de configuração original do VSFTPD para uma possível restauração.

## 6\. Edição do Arquivo de Configuração

```bash
sudo nano /etc/vsftpd.conf
```

Altere as seguintes configurações no arquivo:

  * `anonymous_enable=NO`
  * `write_enable=YES`
  * `local_enable=YES`
  * `chroot_local_user=YES`
  * `local_root=/home/ftpuser/ftp`

## 7\. Reiniciar o Serviço VSFTPD

```bash
sudo systemctl restart vsftpd
```

Reinicia o serviço para aplicar as novas configurações.

-----

# Habilitar o Telnet no Windows 7

### 1\. Ativar o Recurso

No **Painel de Controle**, siga os passos:

  * Vá em **Programas e Recursos**.
  * Clique em **Ativar ou desativar recursos do Windows**.
  * Marque **Servidor Telnet**.
  * Clique em **OK**.

### 2\. Iniciar e Configurar o Serviço

```bash
net start telnet
```

Adicione o usuário desejado ao grupo de Telnet:

```bash
net localgroup "TelnetClients" NomeDoUsuario /add
```

Reinicie o serviço para aplicar as alterações:

```bash
net stop telnet
net start telnet
```
