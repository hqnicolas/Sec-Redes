## Controles de Segurança e Gestão de Acessos
---
### Objetivos

* Compreender os princípios básicos da Gestão de Acessos e Controles de Segurança.
* Prática com o Active Directory (AD).

---
### Fundamentos de Controles de Segurança

**Controles de Segurança:** Medidas para proteger ativos de TI.

* **Objetivo:** Garantir a **Confidencialidade**, **Integridade** e **Disponibilidade** (CID).

**Gestão de Acessos:** Define quem pode acessar o quê e como.

---
### Tipos de Controles de Segurança

**Classificação dos controles:**

<img width="1075" height="1075" alt="image" src="https://github.com/user-attachments/assets/53cb9cc7-75ac-4907-beac-bc068a0cd4a7" />


* **Preventivos:** Evitam incidentes.
* **Detectivos:** Identificam eventos.
* **Corretivos:** Reparam falhas.

---
### Controles Físicos, Lógicos e Administrativos

* **Físicos:** Biometria, catracas, vigilância.
* **Lógicos:** Firewalls, criptografia, autenticação.
* **Administrativos:** Políticas, treinamentos, auditorias.

---
### Princípios de Gestão de Acessos

* Menor Privilégio
* Necessidade de Saber
* Segregação de Funções
* Accountability
* Controle de Sessão

---
### Modelos de Controle de Acesso

| Modelo | Definição | Aplicação |
| :--- | :--- | :--- |
| **DAC** | Controle de Acesso Discricionário | O proprietário do recurso define as permissões de acesso. Comumente usado em sistemas operacionais para gerenciar arquivos e pastas. |
| **MAC** | Controle de Acesso Mandatório | Política de Acesso centralizada e gerida por uma autoridade administrativa. Comumente usado em sistemas militares ou organizações com informações sensíveis. |
| **RBAC** | Controle de Acesso Baseado em Papéis | Permissões atribuídas às funções que um usuário desempenha. Usado em empresas e plataformas de TI. |
| **ABAC** | Controle de Acesso Baseado em Atributos | Permissões com base em atributos (características, propriedades). Usado para proteção de dados sensíveis e personalização de serviços. |

**Vantagens e Desafios dos Modelos de Acesso**

* **DAC:**
    * **Vantagens:** Usuários controlam seus próprios recursos; intuitivo e fácil de usar.
    * **Desafios:** Pode se tornar complexo e propenso a erros em ambientes com muitos usuários.
* **MAC:**
    * **Vantagens:** Segurança reforçada; menor risco de vazamento de informações.
    * **Desafios:** Complexidade de implementação; menor flexibilidade.
* **RBAC:**
    * **Vantagens:** Simplificação; minimiza risco de acesso indevido.
    * **Desafios:** Gestão de Exceções.
* **ABAC:**
    * **Vantagens:** Flexibilidade; adaptação a ambientes complexos; políticas de segurança complexas.
    * **Desafios:** Complexidade; desempenho; gestão de atributos.

---
### Identidade e Autenticação

* **Identificação:** Quem você é.
* **Autenticação:** Provar quem você é.
* **Autorização:** O que você pode fazer.

---
### Métodos de Autenticação

**Fatores:**

* **Algo que você sabe:** Senha.
* **Algo que você tem:** Token, celular.
* **Algo que você é:** Biometria.

**Tipos:** 1FA, 2FA, MFA.

---
### IAM (Identity and Access Management)

* Gerencia o ciclo de vida de usuários.
* Centraliza políticas e auditoria.

---
### Ferramentas e Tecnologias

* **Active Directory / LDAP:** Gerenciamento centralizado de identidades.
* **IAM em nuvem:** Azure AD, AWS IAM, Google IAM.
* **PAM:** Controle de acessos privilegiados.

---
### Políticas de Gestão de Acessos

**Ciclo de vida da conta:**

* Criação
* Manutenção
* Auditoria
* Desativação
