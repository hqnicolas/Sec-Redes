# Certificados e Assinaturas Digitais

Os certificados e assinaturas digitais são elementos essenciais para garantir a segurança e autenticidade em comunicações e transações eletrônicas. Eles fornecem meios para validar a identidade de usuários, dispositivos ou servidores, bem como assegurar a integridade e não repúdio de documentos digitais.

---

## Objetivo

* Perceber a importância e usabilidade dos certificados e assinaturas digitais.
* Prática com GPG e OpenPGP.

---

## O que são Certificados Digitais?

Certificados digitais são arquivos eletrônicos que funcionam como uma "identidade digital" em um ambiente digital.

* Permitem que entidades (pessoas, organizações ou dispositivos) se identifiquem de forma segura em redes.
* Garantem a autenticidade das interações das entidades.
* Asseguram que a entidade que se apresenta é realmente quem diz ser.
* Permitem o uso de criptografia para garantir a segurança dos dados.

---

## Componentes de um Certificado Digital

* **Chave Pública:** A chave pública é um componente essencial do certificado digital.
* **Identidade do Titular:** O certificado contém informações sobre a identidade do titular.
* **Autoridade Certificadora (CA):** A CA é responsável por emitir e validar o certificado digital.
* **Período de Validade:** Todo certificado digital possui um período de validade específico.
* **Assinatura Digital da CA:** A assinatura digital da CA garante a autenticidade do certificado.
* **Extensões e Políticas:** Extensões e políticas são componentes adicionais do certificado digital.

---

## Tipos de Certificados Digitais

### Classificação
Os certificados digitais podem ser classificados com base em seu propósito e na autoridade que os emite.

### Tipos Comuns
* Certificados SSL/TLS
* Certificados de Assinatura de Código
* Certificados de E-mail
* Certificados de Cliente
* Certificados AC Raiz

---

## Certificados SSL/TLS

### O que são?
Usados para proteger comunicações na web através do protocolo HTTPS, esses certificados garantem que os dados entre um navegador e o servidor web são transmitidos de forma segura e privada.

### Uso:
Proteção de sites, criptografia de dados trocados entre clientes e servidores.

---

## Tipos de Certificados SSL/TLS

* **Certificado SSL/TLS de Validação de Domínio (DV):** O mais básico, verifica apenas o domínio, garantindo que a conexão seja segura, mas sem verificar a identidade da organização.
* **Certificado SSL/TLS de Validação de Organização (OV):** Além de validar o domínio, também verifica a organização por trás do site. É mais seguro que o DV.
* **Certificado SSL/TLS de Validação Estendida (EV):** Proporciona o mais alto nível de segurança, validando tanto o domínio quanto a organização em um nível muito mais rigoroso. Sites com EV geralmente exibem o nome da empresa na barra do navegador.

---

## Certificados de E-mail

### O que são?
Usados para assinar e criptografar e-mails. Esses certificados garantem que uma mensagem de e-mail não foi modificada e que ela é proveniente do remetente declarado.

### Uso:
Segurança em comunicações via e-mail, especialmente em ambientes corporativos.

---

## Certificados de Cliente

### O que são?
Emitidos para pessoas físicas ou jurídicas, esses certificados permitem que indivíduos ou entidades se autentiquem em sistemas e façam transações seguras.

### Uso:
* Acesso seguro a sistemas corporativos.
* Autenticação em redes privadas ou governamentais.

---

## Certificados AC Raiz

### O que são?
Certificados emitidos por uma Autoridade Certificadora raiz. Eles são usados para assinar outros certificados, como os de servidores ou de usuários.

### Uso:
Esses certificados ficam no topo da cadeia de confiança e são essenciais para o funcionamento de toda a infraestrutura de PKI (Public Key Infrastructure).

---

## Funcionamento dos Certificados Digitais

O processo básico de utilização de um certificado digital envolve a criptografia assimétrica, onde o certificado contém a chave pública da entidade que será usada por terceiros para validar assinaturas digitais ou criptografar informações. A chave privada correspondente fica apenas com o proprietário do certificado e é usada para assinar digitalmente documentos ou desencriptar dados.

---

## Onde são utilizados?

* **E-commerce:** Certificados SSL/TLS garantem que informações de pagamento sejam transmitidas de forma segura entre o cliente e o site.
* **Sistemas bancários:** Certificados são usados para autenticar usuários e garantir que transações bancárias sejam seguras.
* **Assinatura de documentos:** Certificados são usados para assinar digitalmente documentos legais, contratos e outros arquivos importantes.
* **Infraestrutura de TI:** Empresas utilizam certificados para autenticar usuários, servidores e dispositivos em redes corporativas.

---

## Importância dos Certificados Digitais

* **Confiança:** Eles proporcionam um meio de garantir que as partes envolvidas em uma comunicação digital são quem dizem ser.
* **Segurança:** Oferecem criptografia robusta para proteger dados sensíveis durante a transmissão.
* **Integridade:** Através de assinaturas digitais, certificados asseguram que um documento ou software não foi alterado.
* **Não-repúdio:** Quando uma entidade assina um documento digital, não pode negar ter realizado essa ação.

---

## Certificados Digitais no Brasil

No Brasil, os certificados digitais são categorizados em A1 e A3.

São definidos pelo ICP-Brasil (Infraestrutura de Chaves Públicas Brasileira), que regulamenta a emissão e o uso de certificados digitais no país.

A principal diferença entre eles está no método de armazenamento das chaves criptográficas, na durabilidade e na segurança que oferecem.

Vamos detalhá-los:

---

## Certificado Digital A1

* **Armazenamento:** O certificado A1 é gerado e armazenado no próprio computador do usuário, em um formato de arquivo (geralmente com a extensão ".pfx" ou ".p12"). Esse arquivo contém a chave privada e é protegido por senha.
* **Validade:** O certificado A1 possui validade de 1 ano.

### Mobilidade do Certificado A1
Como o certificado é armazenado no computador, ele pode ser transferido para outros dispositivos, desde que seja exportado corretamente com sua chave privada e importado no novo dispositivo.

### Vantagens do Certificado A1
* **Praticidade:** Pode ser utilizado de forma automática em sistemas e servidores sem a necessidade de um token ou smartcard.
* **Automatização:** É ideal para automação de processos em servidores, como envio automático de documentos fiscais eletrônicos (NF-e, CT-e, etc.).

### Desvantagens do Certificado A1
* **Riscos de Segurança:** Pode trazer riscos, pois como o certificado é armazenado em um arquivo no disco do computador, ele pode estar sujeito a maiores riscos de violação caso o dispositivo seja infectado por malware ou acessado por terceiros indevidamente.

### Exemplo de Uso do Certificado A1
Empresas que precisam emitir notas fiscais eletrônicas (NF-e) de forma automatizada costumam utilizar o certificado A1. O certificado A1 pode ser configurado em sistemas de gestão empresarial (ERP) para emitir documentos sem intervenção humana.

---

## Certificado Digital A3

* **Armazenamento:** O certificado A3 é armazenado em um dispositivo físico, como um token USB ou um smartcard (cartão inteligente). A chave privada nunca deixa esse dispositivo, o que adiciona uma camada extra de segurança.
* **Validade:** O certificado A3 possui validade de até 3 anos.

### Mobilidade do Certificado A3
Como o certificado está vinculado a um dispositivo físico, ele precisa ser conectado ao computador (via USB no caso de tokens, ou leitor de cartões no caso de smartcards) para ser utilizado. Isso significa que o certificado é menos flexível em termos de uso em diferentes dispositivos.

### Vantagens do Certificado A3
* **Segurança:** A chave privada é protegida dentro do dispositivo, tornando muito mais difícil para hackers ou malwares comprometerem o certificado.
* **Durabilidade:** Pode ter uma validade maior (até 3 anos), reduzindo a necessidade de renovação frequente.

### Desvantagens do Certificado A3
* **Praticidade:** Requer o dispositivo físico para funcionar, o que pode ser um obstáculo em cenários de automação ou uso remoto.

### Exemplo de Uso do Certificado A3
Certificados A3 são comumente usados em ambientes que exigem alta segurança e autenticidade, como em assinaturas digitais de contratos, peticionamento eletrônico em tribunais (no caso de advogados), e em sistemas de e-Government (governo eletrônico).

---

## Assinaturas Digitais

### O que são?
Uma assinatura digital é um mecanismo de criptografia que permite que o remetente de um documento ou mensagem comprove sua identidade e garanta a integridade do conteúdo. Assim, o destinatário pode verificar se a mensagem ou o documento não foi alterado após a assinatura e se realmente foi enviado pela pessoa ou entidade que afirma ter enviado.

### A Assinatura Digital Fornece:
* **Autenticidade:** Confirma que o documento ou mensagem veio de uma fonte legítima.
* **Integridade:** Assegura que o conteúdo não foi alterado desde que foi assinado.
* **Não-repúdio:** Garante que o autor da assinatura não pode negar posteriormente a autoria da assinatura.

---

## Como funciona?

A assinatura digital utiliza criptografia assimétrica, que envolve um par de chaves:

* **Chave privada:** Usada para assinar o documento.
* **Chave pública:** Usada para verificar a assinatura.

---

## Processo de Assinatura Digital

1.  **Geração de Hash:** O remetente cria um hash do documento ou mensagem a ser enviado.
2.  **Criptografia do Hash:** O remetente criptografa o hash com sua chave privada. Isso cria a assinatura digital.
3.  **Envio do Documento e Assinatura:** O remetente envia o documento original (ou mensagem) junto com a assinatura digital.
4.  **Verificação do Destinatário:**
    * O destinatário gera um novo hash do documento recebido.
    * O destinatário também descriptografa a assinatura digital usando a chave pública do remetente, o que revela o hash original criado pelo remetente.
    * O destinatário compara os dois hashes (o gerado por ele e o enviado pelo remetente). Se forem iguais, isso confirma que o documento não foi alterado e que foi realmente assinado pelo remetente.

---

## Usos das Assinaturas Digitais

* Assinatura de Documentos Legais
* Assinatura de E-mails
* Assinatura de Software
* Transações Bancárias e Financeiras
* Blockchain e Criptomoedas

### Assinatura de Documentos Legais
As assinaturas digitais substituem as assinaturas manuscritas em contratos eletrônicos. Elas são juridicamente válidas e aceitas em muitos países, incluindo o Brasil, desde que sigam os padrões estabelecidos por legislações.
**Exemplo:** Um contrato de prestação de serviços pode ser assinado digitalmente por ambas as partes, assegurando que o documento não será alterado e provando a autoria da assinatura.

### Assinatura de E-mails
E-mails podem ser assinados digitalmente para garantir que o remetente é realmente quem afirma ser e que a mensagem não foi modificada no caminho até o destinatário.
**Exemplo:** Em empresas, executivos ou departamentos de TI podem assinar digitalmente e-mails confidenciais, protegendo a comunicação.

### Assinatura de Software
Desenvolvedores de software usam assinaturas digitais para garantir que o código não foi alterado após a sua criação. Isso é fundamental para a distribuição de softwares, pois permite que os usuários verifiquem a autenticidade do programa e evitem malware.
**Exemplo:** Sistemas operacionais, como o Windows e o macOS, exigem que aplicativos sejam assinados digitalmente para que possam ser instalados sem alertas de segurança.

### Transações Bancárias
Bancos e sistemas financeiros utilizam assinaturas digitais para autenticar transações online, garantindo que as transações não possam ser alteradas e que o usuário é quem realmente está autorizando a operação.
**Exemplo:** Um pagamento online pode ser autenticado por meio de uma assinatura digital para evitar fraudes.

### Blockchain e Criptomoedas
As assinaturas digitais são um componente central em transações de criptomoedas, como o Bitcoin, onde cada transação é assinada digitalmente para garantir que somente o proprietário da chave privada pode autorizar o envio de fundos.
**Exemplo:** Quando um usuário de Bitcoin envia uma transação, ele assina a transação digitalmente com sua chave privada, provando que tem o direito de mover os fundos.

---

## Importância das Assinaturas Digitais

* **Segurança:** As assinaturas digitais garantem que o conteúdo de um documento ou transação não possa ser alterado após a assinatura.
* **Confiança:** O uso de assinaturas digitais permite que o destinatário confie na identidade do remetente e tenha certeza de que o documento ou transação é legítima.
* **Economia de Tempo e Recursos:** O uso de assinaturas digitais elimina a necessidade de imprimir, assinar e enviar fisicamente documentos.
* **Validade Jurídica:** Em muitos países, como o Brasil, assinaturas digitais têm validade legal e são reconhecidas pela legislação.
