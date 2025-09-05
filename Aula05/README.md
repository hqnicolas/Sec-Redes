# 📖 Criptografia

## 🎯 Objetivos

- Distinguir entre **criptografia simétrica** e **assimétrica**, explorando seus pontos fortes e fracos.
- Realizar práticas com **OpenSSL**.

---

## 🔒 Objetivos da Criptografia

### 🤫 Confidencialidade
Garantir que apenas pessoas autorizadas possam acessar as informações.

### 🛡️ Integridade
Assegurar que as informações não sejam alteradas durante a transmissão ou armazenamento.

### 🌐 Disponibilidade
Garantir que as informações estejam acessíveis quando necessário para usuários autorizados.

---

## 📜 Criptografia na Antiguidade

### 🏺 400 a.C. - Escítala Espartana
Utilizada por espartanos para enviar mensagens cifradas usando um bastão e uma tira de couro. Esse método é um dos primeiros exemplos documentados de **criptografia de transposição**, onde a ordem das letras é modificada para ocultar a mensagem original.

### 🏛️ 50 a.C. - Cifra de César

- **Utilização:** Um dos primeiros métodos de criptografia substitutiva, utilizado por Júlio César para proteger comunicações militares.
- **Método:** Substituição de cada letra do alfabeto por outra que se encontrava três posições à frente.
- **Exemplo:** `"Seguranca em Redes"` se torna `"Vhjxudqfd hp Uhghv"`.

---

## 📜 Cifra de Vigenère (1586)

1.  **Desenvolvimento:** Criada pelo diplomata francês Blaise de Vigenère.
2.  **Características:** Cifra polialfabética que utiliza uma **palavra-chave** para cifrar e decifrar mensagens.
3.  **Inovação:** Ao contrário da Cifra de César, o deslocamento das letras varia com base na sequência determinada pela palavra-chave.

### 🛠️ Funcionamento da Cifra de Vigenère

- **Quadrado de Vigenère:** Utiliza uma tabela com as 26 letras do alfabeto, onde cada linha representa um deslocamento de uma letra em relação à anterior.
- **Processo de Cifragem:** Combina a letra do texto claro com a letra correspondente da palavra-chave.
- **Repetição:** O processo é repetido para cada letra subsequente, reiniciando a palavra-chave quando necessário.

> Para uma demonstração prática, acesse: [Cifra de Vigenère na Prática](https://cifradevigenere.vercel.app/artigo#cifra-de-vigenere-na-pratica)

### 🌍 Significado Histórico

- **Comunicações Militares:** Proteção de informações estratégicas em conflitos.
- **Fundamentos para o Futuro:** Base para o desenvolvimento de técnicas modernas de criptografia.
- **Cultura e Religião:** Preservação de conhecimentos sagrados e culturais.

---

## 📜 Cilindro de Jefferson (1795)

Inventado por Thomas Jefferson, é um dispositivo mecânico para cifragem e decifragem de mensagens.

- **Composição:** 36 discos rotativos, cada um com as 26 letras do alfabeto dispostas aleatoriamente.
- **Montagem:** Os discos são montados em um eixo, e a ordem pode ser ajustada para uma configuração específica (a chave).

### 🛠️ Funcionamento do Cilindro

1.  **Configuração da Chave:** Os discos são ajustados de acordo com uma ordem predeterminada.
2.  **Criptografando:** A mensagem clara é alinhada em uma linha. Uma linha diferente de caracteres é lida como a mensagem cifrada.
3.  **Decifrando:** O processo é revertido, usando a mesma configuração de discos e procurando a linha que contém uma mensagem que faça sentido.

---

## ⚙️ A Era das Máquinas

### 🇩🇪 Máquina Enigma (1918-1920s)

Desenvolvida por Arthur Scherbius, a Enigma foi uma invenção revolucionária. Inicialmente comercial, foi amplamente adotada pelo exército alemão na Segunda Guerra Mundial.

- **Componentes:**
  - **Rotores (3 a 5):** Cada rotor continha um alfabeto completo e girava a cada tecla pressionada, alterando a substituição das letras.
  - **Painel de Conectores:** Permutava pares de letras, aumentando a complexidade da cifra.
- **Decifragem:** A máquina receptora precisava ter a mesma configuração de rotores, posições iniciais e painel de conectores.

#### 💣 Bombe
O centro de criptoanálise britânico de **Bletchley Park**, liderado por figuras como **Alan Turing**, foi responsável pela quebra das cifras da Enigma. Utilizando técnicas matemáticas e uma máquina chamada **Bombe**, os criptoanalistas conseguiram decifrar mensagens alemãs, o que é considerado um fator que encurtou a guerra em vários anos e salvou inúmeras vidas.

### 🇩🇪 Máquina Lorenz (1941)

Utilizada pelo exército alemão para comunicações de alto nível, como as enviadas entre Hitler e seus comandantes. Era mais complexa que a Enigma, utilizando 12 rotores.

#### 💻 Decifragem da Lorenz
Para decifrar as mensagens da Lorenz, os criptoanalistas de Bletchley Park desenvolveram o **Colossus**, considerado o primeiro computador eletrônico digital programável do mundo. O Colossus utilizava técnicas de criptoanálise estatística para identificar padrões nas cifras de fluxo da Lorenz.

---

## 💻 Criptografia Digital

### 📦 Cifras de Bloco
Algoritmos que transformam dados em blocos de tamanho fixo. Cada bloco é cifrado individualmente por meio de uma chave secreta.

#### **DES (Data Encryption Standard)**
Desenvolvido pela IBM e adotado como padrão pelo governo dos EUA em 1977. Com uma chave de 56 bits, tornou-se vulnerável a ataques de força bruta e foi oficialmente substituído pelo AES em 1999.

#### **AES (Advanced Encryption Standard)**
1.  **Sucessor do DES:** Tornou-se o novo padrão de criptografia do governo dos EUA em 2001.
2.  **Tamanhos de Chave Flexíveis:** Oferece opções de **128, 192 ou 256 bits**, proporcionando diferentes níveis de segurança.
3.  **Amplamente Utilizado:** Padrão em aplicações modernas como criptografia de discos, comunicações sem fio e proteção de dados em bancos de dados.

### 🌊 Cifras de Fluxo
Geram um fluxo pseudoaleatório de bits que é combinado com os dados a serem cifrados (usando uma operação XOR, por exemplo).

- **Exemplo:** O **RC4** é um dos exemplos mais conhecidos, embora hoje seja considerado inseguro. Era usado em protocolos como SSL e WEP.

---

## 🔑 Criptografia de Chave Pública

Introduzida por Whitfield Diffie e Martin Hellman, utiliza duas chaves distintas: uma **chave pública** para cifrar e uma **chave privada** para decifrar.

### **RSA (Rivest-Shamir-Adleman)**
- **Criadores:** Desenvolvido por Ron Rivest, Adi Shamir e Leonard Adleman em 1977.
- **Chaves:** Utiliza um par de chaves: uma pública (compartilhada livremente) e uma privada (mantida em segredo).
- **Segurança:** Baseia-se na dificuldade matemática de fatorar grandes números primos.
- **Aplicações:** Assinatura digital, segurança de comunicação (TLS/SSL) e autenticação de usuários.

### **ECC (Criptografia de Curvas Elípticas)**
- **Matemática Avançada:** Baseia-se em propriedades complexas de curvas elípticas.
- **Segurança Aprimorada:** Oferece níveis de segurança comparáveis ao RSA, mas com **chaves menores**, tornando-a ideal para dispositivos com recursos limitados (como smartphones e IoT).
- **Eficiência:** Para atingir a segurança de uma chave RSA de 2048 bits, a ECC necessita apenas de uma chave de 224 bits.
- **Aplicações:** Criptografia de dispositivos móveis, autenticação de sites e transações financeiras seguras.

---

## ⚛️ O Futuro: Criptografia Pós-Quântica

A computação quântica tem o potencial de quebrar muitos dos sistemas de criptografia atuais (como RSA e ECC) ao resolver problemas matemáticos complexos de forma muito mais rápida.

**Criptografia Pós-Quântica (PQC)** refere-se a algoritmos criptográficos que são seguros contra ataques de computadores quânticos.

### Algoritmos Padrão (NIST PQC Standardization)
| Algoritmo | Baseado em | Uso Principal |
| :--- | :--- | :--- |
| **CRYSTALS-Kyber** | Redes (Lattices) | Troca de Chaves |
| **FALCON** | Redes (Lattices) | Assinaturas Digitais |
| **SPHINCS+** | Funções de Hash | Assinaturas Digitais |

> **Nota:** Muitos desses algoritmos estão em fase avançada de padronização, mas a implementação em larga escala ainda está em andamento.

---

## 🔄 Criptografia Simétrica vs. Assimétrica

###  Symmetric Criptografia Simétrica
Método de cifragem onde a **mesma chave** é utilizada tanto para cifrar quanto para decifrar a informação.

- **Funcionamento:**
  - **Cifragem:** `Texto Claro + Chave Secreta -> Texto Cifrado`
  - **Decifragem:** `Texto Cifrado + Mesma Chave Secreta -> Texto Claro`

#### Algoritmos Comuns
| Algoritmo | Descrição | Tamanho da Chave |
| :--- | :--- | :--- |
| **AES** | Padrão moderno e seguro. | 128, 192, 256 bits |
| **DES** | Antigo e inseguro. | 56 bits |
| **3DES** | Aplica o DES três vezes, mais seguro que o DES mas lento. | 168 bits efetivos |

#### 👍 Vantagens
- **Rapidez:** Muito mais rápido que a criptografia assimétrica. Ideal para grandes volumes de dados.
- **Eficiência:** Requer menos poder computacional.

#### 👎 Desvantagens
- **Distribuição de Chaves:** O maior desafio é compartilhar a chave secreta de forma segura.
- **Escalabilidade:** Em uma rede com *n* usuários, são necessárias `n(n-1)/2` chaves para comunicação par a par.
- **Gerenciamento de Chaves:** Complexo em grandes redes.

#### 💼 Usabilidade
- **Comunicações Internas:** Redes corporativas, Wi-Fi (WPA2/3).
- **Criptografia de Disco/Arquivos:** BitLocker, FileVault.

### 👥 Criptografia Assimétrica
Utiliza um par de chaves matematicamente relacionadas: uma **chave pública** para cifrar e uma **chave privada** para decifrar.

- **Funcionamento:**
  - A chave pública pode ser distribuída livremente.
  - A chave privada deve ser mantida em segredo absoluto pelo proprietário.

#### Algoritmos Comuns
| Algoritmo | Descrição |
| :--- | :--- |
| **RSA** | Baseado na dificuldade de fatorar números primos. |
| **DSA** | Usado para assinaturas digitais. |
| **ECC** | Baseado em curvas elípticas, mais eficiente que o RSA. |

#### 👍 Vantagens
- **Distribuição de Chaves Segura:** Resolve o problema da distribuição de chaves da criptografia simétrica.
- **Autenticação e Assinatura Digital:** Permite verificar a identidade do remetente e a integridade da mensagem.
- **Escalabilidade:** Mais fácil de gerenciar em sistemas com muitos usuários.

#### 👎 Desvantagens
- **Desempenho:** É computacionalmente mais intensiva e muito mais lenta que a simétrica.
- **Complexidade:** Requer maior poder de processamento.

#### 💼 Usabilidade
- **Troca de Chaves:** Usada para estabelecer um canal seguro e trocar uma chave simétrica (ex: TLS/SSL).
- **E-mails Seguros:** PGP (Pretty Good Privacy).
- **Certificados Digitais:** Autenticação de websites.
- **Assinaturas Digitais:** Garante autenticidade e integridade de documentos.

---

### 📊 Tabela Comparativa

| Característica | Criptografia Simétrica | Criptografia Assimétrica |
| :--- | :--- | :--- |
| **Chaves** | Mesma chave para cifrar e decifrar | Chave pública para cifrar, privada para decifrar |
| **Velocidade** | 🚀 Mais rápida | 🐢 Mais lenta |
| **Complexidade** | Menor | Maior |
| **Distribuição de Chaves**| Difícil e arriscada | Fácil e segura |
| **Usabilidade** | Grandes volumes de dados (streaming, arquivos) | Troca de chaves, assinaturas, autenticação |
| **Segurança** | Vulnerável se a chave for comprometida | Maior segurança devido à separação das chaves |
| **Escalabilidade**| Menos escalável | Mais escalável |