# 🖥️ SSH-Enabled Ubuntu Desktop (Docker Container)

A lightweight Ubuntu 24.04 container with **SSH access** and a **minimal desktop environment**.  
Ideal for remote GUI sessions, testing, or lightweight desktop development inside Docker.

---

## 🚀 Features

- **Base Image:** `ubuntu:24.04` (official & lightweight)
- **Desktop Environment:** `ubuntu-desktop-minimal`  
  → *(switch to `ubuntu-desktop` for full GUI support)*
- **SSH Server:** Enabled and preconfigured
- **User Access:** 
  - Username: `dockeruser`  
  - Password: `password`
- **SSH Port Mapping:**  
  - `localhost:2222` → `container:22`

---

## 🧱 1. Project Structure

```
SSH_Server/
├── Dockerfile
├── docker-compose.yml
└── README.md
```

---

## ⚙️ 2. Build & Run

Build and start the container using Docker Compose:

```bash
docker compose build
docker compose up -d
```

Check that the container is running:

```bash
docker ps
```

---

## 🔑 3. Access via SSH

Once the container is running, connect to it using:

```bash
ssh dockeruser@localhost -p 2222
# password: password
```

If successful, you’ll be inside your Ubuntu desktop environment (headless mode).  
You can later attach a GUI via **VNC**, **X11 forwarding**, or **RDP**.

---

## 🧩 4. Optional Enhancements

### 🧑‍💻 Connect as Root
If you prefer SSH access as the root user, add the following line to your Dockerfile:

```dockerfile
RUN echo 'root:root' | chpasswd
```

Then connect with:

```bash
ssh root@localhost -p 2222
# password: root
```

---

### 🔐 Use SSH Keys or Custom Configs
Mount your own SSH configuration or keys to the container:

```yaml
volumes:
  - ./sshd_config:/etc/ssh/sshd_config
  - ~/.ssh/authorized_keys:/home/dockeruser/.ssh/authorized_keys
```

---

### 🖼️ Add GUI Access (Optional)
You can enable a desktop session using:

- **X11 Forwarding:**  
  Run SSH with the `-X` flag:  
  ```bash
  ssh -X dockeruser@localhost -p 2222
  ```

- **VNC Server:**  
  Install `tightvncserver` or similar and expose its port via Docker Compose.

---

## 🧰 5. Common Commands

| Task | Command |
|------|----------|
| Stop container | `docker compose down` |
| Restart container | `docker compose restart` |
| Rebuild image | `docker compose build --no-cache` |
| View logs | `docker compose logs -f` |

---

## 🧼 6. Cleanup

To remove everything (containers, images, and volumes):

```bash
docker compose down --rmi all -v
```

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

### 💡 Notes
- For a **full Ubuntu Desktop experience**, replace `ubuntu-desktop-minimal` with `ubuntu-desktop` in the Dockerfile (requires ~2–3 GB).
- Default credentials are for **local development only** — change them before exposing the container to a network.

---

**Author:** Your Name  
**Version:** 1.0.0  
**Last Updated:** November 2025