# Hardening

Procedimentos que profissionais de Segurança da Informação faz para aprimorar a segurança de um sistema, serviço ou hardware.

Hardening = Endurecimento = Fortalecimento

---

## Importante!
* Todo Hardening deve ser documentado, afim de se manter um histórico de configurações de todo o parque.
* Não aplicar técnicas de Hardening em ambientes de produção. Homologar primeiro.

## Objetivo do Hardening

O objetivo principal do processo de hardening é:

* Manter o mesmo nível de segurança em todos os servidores
* Garantir consistência de segurança em sistemas operacionais
* Assegurar proteção uniforme em aplicações
* Estabelecer padrões de segurança consistentes para serviços

---

## Dicas para Hardening

### Configurar senhas de BIOS
Estabeleça senhas fortes para o BIOS do sistema, adicionando uma camada extra de segurança contra acesso não autorizado.

### Definir prioridades de BOOT
Configure corretamente a ordem de inicialização do sistema para garantir que apenas dispositivos autorizados sejam usados durante o processo de boot.

### Utilizar o CIS Benchmark
Implemente as recomendações do CIS Benchmark para fortalecer a segurança do sistema de acordo com as melhores práticas.

---

## Visão Geral do CIS Benchmark

* **CIS:** Center of Internet Security
* São um conjunto de práticas recomendadas globalmente.
* Ajudam os profissionais de segurança da informação a implementar e gerenciar suas defesas.

---

## Importância do CIS Benchmark

O CIS Benchmark é de extrema importância por várias razões fundamentais.

Primeiramente, esses benchmarks descrevem as melhores práticas de segurança da informação, fornecendo um guia valioso para organizações que buscam fortalecer sua postura de segurança.

Um aspecto crucial é que os CIS Benchmarks são desenvolvidos por profissionais e especialistas no assunto. Isso garante que as recomendações sejam baseadas em conhecimento profundo e experiência prática, tornando-os uma fonte confiável de orientação em segurança.

Além disso, os documentos CIS Benchmarks gozam de amplo reconhecimento e aceitação. Eles são adotados por uma variedade de entidades, incluindo governos, empresas, instituições de pesquisa e acadêmicas. Essa ampla aceitação ressalta a credibilidade e a eficácia das diretrizes fornecidas pelo CIS Benchmark.

---

## Conformidade com Padrões

### Alinhamento com NIST
Os documentos CIS Benchmarks se alinham com a Estrutura de segurança cibernética do Instituto Nacional de Padrões e Tecnologia (NIST).

### Conformidade com HIPAA
Os CIS Benchmarks estão em conformidade com a Lei de Portabilidade e Responsabilidade de Seguros de Saúde (HIPAA).

### Alinhamento com PCI DSS
Os documentos CIS Benchmarks também se alinham com o Padrão de segurança de dados do setor de cartões de pagamento (PCI DSS).

---

## Sistemas Cobertos pelo CIS Benchmarks

| | |
| --- | --- |
| Sistemas Operacionais | Infraestrutura e Serviços em Nuvem |
| Software de Servidor | Software de Estação de Trabalho |
| Dispositivos Móveis | Dispositivos de Rede |
| Dispositivos de Impressão Multifuncionais | |

---

## Estrutura do Documento CIS Benchmark

**Profile Applicability:** Pode ser traduzido como Perfil de Aplicabilidade. Esse campo indica qual o perfil em que o procedimento pode ser aplicado.
* Exemplos: Corporativo/Empresarial, pessoal etc.

**Description:** Pode ser traduzido como Descrição. Esse campo descreve brevemente o que será realizado no procedimento.

**Rationale:** Pode ser traduzido como Justificativa. Esse campo descreve a razão ou importância para estar realizando esse procedimento.

**Impact:** Pode ser traduzido como Impacto. Esse campo descreve quais seriam os impactos ao realizar o procedimento.

---

## Estrutura do Documento CIS Benchmark (Continuação)

**Audit:** Pode ser traduzido como Auditoria. Esse campo fornece uma maneira de verificar se esse procedimento já foi aplicado.
* Geralmente, existem outras maneiras de verificar.

**Remediation:** Pode ser traduzido como Remediação. Esse campo descreve como aplicar o procedimento em questão.

**Default Value:** Pode ser traduzido como Valor padrão. Esse campo exibe qual é o valor de fábrica antes de uma alteração.
* Geralmente é utilizado para comparação ou restauração.

**CIS Controls:** Esse campo relaciona esse procedimento com as diretrizes dos Controles CIS ou CIS Controls.

---

## Exemplo: `2.2.1 (L1) Ensure 'Access Credential Manager as a trusted caller' is set to 'No One' (Automated)`

### Profile Applicability:
* Level 1-Domain Controller
* Level 1 Member Server

### Description:
This security setting is used by Credential Manager during Backup and Restore. No accounts should have this user right, as it is only assigned to Winlogon. Users' saved credentials might be compromised if this user right is assigned to other entities.
The recommended state for this setting is: No One.

### Rationale:
If an account is given this right the user of the account may create an application that calls into Credential Manager and is returned the credentials for another user.

### Impact:
None this is the default behavior.

### Audit:
Navigate to the UI Path articulated in the Remediation section and confirm it is set as prescribed.

### Remediation:
To establish the recommended configuration via GP, set the following Ul path to No One:
Computer Configuration\Policies\Windows Settings Security Settings\Local Policies\User Rights Assignment Access Credential Manager as a trusted caller

### Default Value:
No one.

---

## Appendix: Recommendation Summary

Ao final tem um Apêndice com uma tabela onde se pode registrar se a configuração recomendada foi aplicada ou não. Como um relatório.
Esta tabela permite que os administradores de sistemas documentem facilmente o status de implementação de cada recomendação do CIS Benchmark, fornecendo uma visão geral clara do progresso de hardening do sistema.

**Exemplo de Tabela:**

| Control | Set Correct |
| :--- | :---: |
| **Account Policies** | |
| **Password Policy** | |
| (L1) Ensure 'Enforce password history' is set to '24 or more password(s)' (Automated) | [ ] |
| (L1) Ensure 'Maximum password age' is set to '365 or fewer days, but not 0' (Automated) | [ ] |
| (L1) Ensure 'Minimum password age' is set to '1 or more day(s)' (Automated) | [ ] |
| (L1) Ensure 'Minimum password length' is set to '14 or more character(s)' (Automated) | [ ] |
| (L1) Ensure 'Password must meet complexity requirements' is set to 'Enabled' (Automated) | [ ] |
| (L1) Ensure 'Relax minimum password length limits' is set to 'Enabled' (Automated) | [ ] |
| (L1) Ensure 'Store passwords using reversible encryption' is set to 'Disabled' (Automated) | [ ] |
| **Account Lockout Policy** | |
| (L1) Ensure 'Account lockout duration' is set to '15 or more minute(s)' (Automated) | [ ] |
| (L1) Ensure 'Account lockout threshold' is set to '5 or fewer invalid logon attempt(s), but not 0' (Automated) | [ ] |
| (L1) Ensure 'Reset account lockout counter after' is set to '15 or more minute(s)' (Automated) | [ ] |
| **Local Policies** | |
| **Audit Policy** | |
| **User Rights Assignment** | |
| (L1) Ensure 'Access Credential Manager as a trusted caller' is set to 'No One' (Automated) | [ ] |
| (L1) Ensure 'Access this computer from the network' is set to 'Administrators, Authenticated Users, ENTERPRISE DOMAIN CONTROLLERS' (DC only) (Automated) | [ ] |
| (L1) Ensure 'Access this computer from the network' is set to 'Administrators, Authenticated Users' (MS only) (Automated) | [ ] |

---
