# 🪟 Guia para Usuários Windows — Inicializando o Container Ubuntu com SSH

Este guia foi criado especialmente para usuários do **Windows** que desejam rodar o ambiente **Ubuntu 24.04 com SSH e interface desktop mínima** em um container Docker.

---

## ⚙️ Pré-requisitos

Antes de começar, certifique-se de que possui os seguintes componentes instalados:

### 🧩 1. Docker Desktop
- Baixe e instale o **Docker Desktop for Windows**:  
  👉 [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
- Durante a instalação, **ative o suporte ao WSL 2** (Windows Subsystem for Linux).
- Após instalado, abra o Docker Desktop e verifique se está **"Running"**.

### 🪟 2. Windows Terminal ou PowerShell
Você pode usar:
- **PowerShell**
- **Windows Terminal**
- **Git Bash** (opcional, mas recomendado)

---

## 📂 Estrutura do Projeto

Certifique-se de que a estrutura de pastas esteja assim:

```
Aula11/
└── Container/
    ├── Dockerfile
    ├── docker-compose.yml
    └── README_Windows.md   ← (este arquivo)
```

---

## 🚀 Inicializando o Container

1. **Abra o PowerShell** (ou Windows Terminal).
2. Navegue até a pasta do projeto:

   ```powershell
   cd caminho\para\Aula11\Container
   ```

   > 💡 Exemplo:  
   > `cd C:\Users\SeuUsuario\Documents\Aula11\Container`

3. **Construa a imagem Docker:**

   ```powershell
   docker compose build
   ```

4. **Inicie o container em segundo plano:**

   ```powershell
   docker compose up -d
   ```

5. **Verifique se está rodando:**

   ```powershell
   docker ps
   ```

   Deve aparecer algo como:

   ```
   CONTAINER ID   IMAGE          COMMAND          STATUS         PORTS
   123abc456def   container_ssh  "/usr/sbin/sshd" Up 5 minutes   0.0.0.0:2222->22/tcp
   ```

---

## 🔑 Conectando via SSH (no Windows)

### 🧰 Opção 1 — Usando o PowerShell

O Windows 10/11 já possui o cliente SSH integrado.  
Basta executar:

```powershell
ssh dockeruser@localhost -p 2222
```

> Quando solicitado, insira a senha:  
> **password**

Se aparecer um aviso de autenticação, digite `yes` para continuar.

---

### 🧰 Opção 2 — Usando o PuTTY (Interface Gráfica)

Se preferir uma ferramenta visual:

1. Baixe o **PuTTY**:  
   👉 [https://www.putty.org/](https://www.putty.org/)
2. Abra o PuTTY e configure:
   - **Host Name (or IP address):** `localhost`
   - **Port:** `2222`
   - **Connection type:** `SSH`
3. Clique em **Open**.
4. Quando solicitado:
   - **Username:** `dockeruser`
   - **Password:** `password`

---

## 🖼️ Acessando o Ambiente Gráfico (Opcional)

O container vem com o **ubuntu-desktop-minimal** instalado, mas por padrão ele roda em **modo headless (sem tela)**.

Você pode acessar a interface gráfica via:

### 💠 X11 Forwarding (requer X server no Windows)

1. Instale o **VcXsrv** ou **Xming**:
   - [https://sourceforge.net/projects/vcxsrv/](https://sourceforge.net/projects/vcxsrv/)
2. Inicie o servidor X no Windows.
3. No PowerShell, conecte-se com:
   ```powershell
   ssh -X dockeruser@localhost -p 2222
   ```
4. Execute um app gráfico, por exemplo:
   ```bash
   xclock
   ```

---

## 🧹 Encerrando o Container

Para parar o container:

```powershell
docker compose down
```

Para reiniciar:

```powershell
docker compose restart
```

Para limpar completamente (containers, volumes e imagens):

```powershell
docker compose down --rmi all -v
```

---

## ⚠️ Dicas Importantes

- Altere as credenciais padrão se for expor o container em rede.
- Use SSH keys para conexões seguras.
- Para uma experiência completa com GUI, substitua `ubuntu-desktop-minimal` por `ubuntu-desktop` no Dockerfile (requer mais espaço).

---

**Autor:** Seu Nome  
**Versão:** 1.0.0  
**Compatível com:** Windows 10 / 11  
**Última Atualização:** Novembro de 2025