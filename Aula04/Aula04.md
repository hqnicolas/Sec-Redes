# Guia: Criação e Ingresso em um Domínio

Este guia descreve os passos para configurar um ambiente com **Active Directory**, **File Server**, **Group Policy** e **Auditoria de Logon** utilizando servidores Windows e clientes Windows 10.

---

## 🖥️ Active Directory (AD)

### Etapas Iniciais

1. Definir IP estático
2. Definir hostname
3. Instalar a Role **Active Directory Domain Services**
4. Promover o servidor a **Domain Controller**
   - Criar uma nova floresta

### Criar Unidades Organizacionais (OUs)

- Servidores  
- Computadores  
- Usuários  
- Grupos  
- Departamentos:
  - RH  
  - TI  
  - Contabilidade  

### Criar Grupos

- `GG-RH`
- `GG-TI`
- `GG-Contabilidade`

### Criar Usuários

| Nome         | Login        | Grupo            |
|--------------|--------------|------------------|
| Maria Silva  | maria.rh     | GG-RH            |
| João Souza   | joao.ti      | GG-TI            |
| Ana Lima     | ana.cont     | GG-Contabilidade |
| Administrador| (Domain Admins) |               |

---

## 📁 File Server (FS)

### Etapas

1. Definir IP Estático
2. Definir Hostname
3. Ingressar no Domínio

### Estrutura de Pastas

- `\\FILESERVER\Dados`
  - `RH`
  - `TI`
  - `Contabilidade`

> **Permissões:**
> - Raiz (`Dados`): Leitura e Execução
> - Subpastas: Modificação para seus respectivos grupos

### Compartilhamento

- Compartilhar a pasta `Dados`
  - `Full Access` para Administradores
  - `Change` para grupos:
    - GG-RH
    - GG-TI
    - GG-Contabilidade

---

## 🛠️ GPO de Mapeamento de Drives

### Criar GPO: `GPO-MapDrives`

**Caminho:**  
`OU Departamentos > Create a GPO in this domain`

### Configuração:

1. **User Configuration > Preferences > Windows Settings > Drive Maps**

2. Criar mapeamentos por departamento:

```
Action: Replace
Location: 
 - \\FILESERVER\Dados\RH
 - \\FILESERVER\Dados\TI
 - \\FILESERVER\Dados\Contabilidade
Label: RH / TI / Contabilidade
Reconnect: ✅
Item-level targeting: Grupo correspondente (GG-RH, GG-TI, etc.)
```

3. **Computer Configuration > Policies > Administrative Templates > System > Logon**

- Habilitar:
  ```
  Always wait for the network at computer startup and logon = Enabled
  ```

---

## 💻 Clientes Windows 10

1. Definir IP Estático
2. Definir Hostname
3. Ingressar no Domínio
4. Testar login com cada conta de usuário criada

---

## 🔍 Habilitar Auditoria de Logon

### Criar GPO: `GPO-LogLogin`

**Caminho:**  
`OU Computadores > Create a GPO in this domain`

### Configuração:

`Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Audit Policy`

- Habilitar:
  - **Audit Logon Events**: Success e Failure

---

## 🧪 Testes com Windows 10

1. Simular login incorreto com um usuário comum
2. Logar como Administrador
3. Abrir o Event Viewer (`eventvwr.msc`)
4. Ir até:
   ```
   Logs do Windows > Segurança
   ```

---

> ⚠️ **Observação:** Este guia é indicado para ambientes de laboratório e estudo. Para ambientes de produção, é essencial seguir boas práticas de segurança, aplicar atualizações e manter backups regulares.
