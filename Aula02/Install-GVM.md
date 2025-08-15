
### Instalação do GVM – Greenbone Vulnerability Management

#### Instalação ####

---

### Atualize e instale o GVM ###

```
sudo apt update && sudo apt upgrade -y
sudo apt install -y gvm
```

-----

### Depois rode o setup e guarde a senha do usuário admin que aparecer no final

```bash
sudo gvm-setup
sudo gvm-check-setup
```

-----

### Para iniciar/parar o serviço

```bash
sudo gvm-start
sudo gvm-stop
```

Abra a interface web: **https://127.0.0.1:9392/login**

Antes do primeiro scan, confirme em **"Administration \> Feed Status"** que os dados foram carregados. Se quiser forçar a sincronização de feed:

```bash
sudo greenbone-feed-sync
```

-----

#### Primeiro scan

-----

### Crie o alvo (Target)

**Configuration → Targets → New Target.**

Em **Hosts**, coloque o IP/FQDN (ex.: 192.168.56.101).

**Port list:** “All IANA assigned TCP” (ou a lista que preferir).

Se for credentialed scan, adicione credenciais SSH/SMB aqui. Salve.

-----

### Crie a tarefa (Task)

**Scans → Tasks → New Task.**

Em **Scan Config**, escolha **Full and fast** (padrão didático).

Em **Target**, selecione o alvo criado. Salve.

-----

### Execute e veja o relatório

Clique no botão **Play** da task.

Ao finalizar, abra **Reports** para ver CVEs, severidades, e detalhes técnicos/mitigações.

```
```
