# ATIVIDADE – Hardening
### ENGENHARIA DE COMPUTAÇÃO - DISCIPLINA DE SEGURANÇA EM REDES DE COMPUTADORES

---

Quando instalamos um sistema operacional — seja um Windows Server, um Linux ou o software de um roteador — ele vem em um estado **"padrão"** (default).

O problema é que **"padrão"** não significa **"seguro"**. O modo padrão é feito para ser fácil de usar e compatível com tudo, não para ser uma fortaleza.

É aí que entra o conceito de Hardenização.

> **"Hardening"** (ou **"Hardenização"**) vem do inglês "fortalecer".
> No contexto de TI, Hardenização é o processo de reduzir a superfície de ataque, ou seja, todos os pontos por onde um invasor pode tentar entrar, de um sistema.

Para isso podemos:

* **Desabilitar serviços desnecessários:** Para que deixar uma porta de Telnet aberta se só usamos SSH?
* **Remover softwares que não usamos:** Menos software = menos bugs para explorar.
* **Aplicar o "Princípio do Menor Privilégio":** Garantir que usuários e serviços só tenham as permissões mínimas necessárias para fazer seu trabalho.
* **Configurar logs e auditoria:** Para sabermos se alguém tentou entrar.
* **Trocar senhas padrão e forçar políticas de senhas fortes.**

Mas como saber o que é ou não seguro? Das milhares de configurações possíveis em um Windows Server, por exemplo, como saber qual se deve alterar?

Precisa-se de um guia. Um manual de melhores práticas que seja confiável, testado e reconhecido por todo o mercado, como o **CIS Benchmark**.

Ele é um documento que nos dá um checklist detalhado, passo a passo, do que devemos configurar em um sistema para torná-lo seguro.

---

A atividade é em dupla.

### Sua tarefa é:

* Leia o conteúdo disponibilizado na aula 07/11 no Teams.
* Escolha um sistema operacional, podendo utilizar uma das VMs disponíveis no Teams.
* Baixar o documento do CIS Benchmark referente ao sistema escolhido - [https://downloads.cisecurity.org/#/](https://downloads.cisecurity.org/#/)
* Aplicar 5 técnicas de hardening de sua escolha. Deve-se registrar (print) como está no sistema e como ficará a configuração após o hardening.
* Após, fazer um artigo de uma ou duas páginas destacando quais técnicas foram utilizadas, evidenciando-as, e explicando o porquê ser importante para a segurança.

