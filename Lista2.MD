# Lista 2 de exercícios - Segurança de Dados
## Exercício 1
### a) **Expressão para a decriptação**
A decriptação de uma cifra de fluxo que utiliza XOR é feita de forma simples. Se a cifra é dada por `C_i = M_i ⊕ K_i`, a decriptação é dada por `M_i = C_i ⊕ K_i`. Isso funciona porque a operação XOR é invertível: `(M_i ⊕ K_i) ⊕ K_i = M_i`, permitindo recuperar a mensagem original.

### b) **O que precisa ser feito para que a cifra seja one-time pad?**
Para que a cifra seja um **one-time pad** (OTP), a chave precisa ser:
1. **Aleatória**: Deve ser gerada de forma imprevisível, sem padrões.
2. **Do mesmo tamanho que a mensagem**: A chave deve ter o mesmo número de bits da mensagem para garantir que cada bit da mensagem seja cifrado por um bit único da chave.
3. **Usada apenas uma vez**: A chave não pode ser reutilizada em outra mensagem, garantindo que a segurança não seja comprometida.

Essas condições garantem a segurança do OTP, tornando-o incondicionalmente seguro.

### c) **Relação entre o tamanho da mensagem e da chave em uma cifra de bloco**
Em uma cifra de bloco, a chave deve ser do tamanho suficiente para cifrar todos os blocos de dados. Se a mensagem tem `m` bits e a cifra opera em blocos de `n` bits, então a chave precisa ter pelo menos `m` bits, para garantir que não haja reutilização da chave entre os blocos.

### d) **Dificuldades práticas de usar um one-time pad de fluxo**
As principais dificuldades de usar um **one-time pad** de fluxo incluem:
1. **Geração e distribuição da chave**: A chave precisa ser aleatória e tão longa quanto a mensagem, o que é difícil de garantir de forma segura em larga escala.
2. **Armazenamento e gerenciamento de chaves**: A chave precisa ser armazenada de forma segura e descartada após o uso, o que é complexo em sistemas grandes.
3. **Escalabilidade**: A produção e distribuição de grandes quantidades de chaves para mensagens longas ou frequentes é um grande desafio, tornando o uso do OTP prático apenas em casos específicos.


# Exercício 2 : Não vou fazer essa merda. Cornojob e não aprende nada.
---
# Exercício 3
### Passo 1: Explorar a linearidade da cifra

Dada a propriedade linear da cifra \( E_L \):

```
E_L(k, m1 ⊕ m2) = E_L(k, m1) ⊕ E_L(k, m2)
```

Isso significa que a cifra preserva a operação XOR entre os textos claros. Essa propriedade permite que um adversário construa um sistema de equações lineares para determinar a relação entre os textos claros e os textos cifrados.

---

### Passo 2: Obter 128 pares de texto claro/texto cifrado

O adversário pode escolher 128 textos claros \( m_1, m_2, ..., m_{128} \), onde cada \( m_i \) é um vetor de 128 bits com um único bit definido como 1 e os demais como 0. Por exemplo:

```
m1 = 100...0, m2 = 010...0, ..., m128 = 000...1
```

Para cada \( m_i \), o adversário obtém o texto cifrado correspondente \( c_i = E_L(k, m_i) \).

---

### Passo 3: Construir uma matriz de transformação linear

Como a cifra é linear, ela pode ser representada como uma transformação linear sobre o espaço vetorial de 128 bits. Isso significa que existe uma matriz \( A \) de tamanho 128x128 (que depende da chave \( k \)) tal que:

```
E_L(k, m) = A · m
```

Onde \( m \) é um vetor de 128 bits (texto claro) e \( A · m \) é a multiplicação da matriz \( A \) pelo vetor \( m \).

---

### Passo 4: Determinar a matriz \( A \)

Com os 128 pares \( (m_i, c_i) \), o adversário pode determinar a matriz \( A \). Como cada \( m_i \) tem um único bit definido como 1, o texto cifrado \( c_i \) corresponde à \( i \)-ésima coluna da matriz \( A \). Assim, a matriz \( A \) pode ser construída diretamente a partir dos textos cifrados \( c_1, c_2, ..., c_{128} \).

---

### Passo 5: Decifrar qualquer texto cifrado

Uma vez que a matriz \( A \) é conhecida, o adversário pode decifrar qualquer texto cifrado \( c \) resolvendo o sistema linear:

```
c = A · m
```

Como \( A \) é uma matriz 128x128 e foi construída a partir de 128 pares linearmente independentes, ela é invertível. Portanto, o texto claro \( m \) pode ser obtido por:

```
m = A^{-1} · c
```

Onde \( A^{-1} \) é a matriz inversa de \( A \).

---

### Resumo

1. O adversário escolhe 128 textos claros \( m_i \) com um único bit definido como 1.
2. Obtém os textos cifrados correspondentes \( c_i = E_L(k, m_i) \).
3. Constrói a matriz \( A \) a partir dos \( c_i \).
4. Inverte a matriz \( A \) para obter \( A^{-1} \).
5. Decifra qualquer texto cifrado \( c \) usando \( m = A^{-1} · c \).

---


5 - Suponha que você fez um algoritmo baseado em cifra de Feistel. Para deixá-lo mais
seguro, o que você pode alterar em relação...

### a) **Número de rodadas**
**Alteração**: Aumentar o número de rodadas na cifra de Feistel.

**Como melhora a segurança**: 
O número de rodadas afeta diretamente a complexidade da cifra. Ao aumentar as rodadas, a cifra se aproxima mais de uma permutação e difusão total, o que torna mais difícil para um atacante realizar uma análise criptográfica eficaz (como análise diferencial ou linear). Mais rodadas aumentam o esforço necessário para realizar uma chave de recuperação ou uma análise de criptoanálise, dificultando o ataque.

**Por que isso melhora a segurança?**: Aumentando as rodadas, o algoritmo passa a espalhar melhor a informação através do bloco de dados, tornando mais difícil para o atacante identificar padrões e extrair informações úteis sobre a chave ou o texto original.

### b) **Tamanho do bloco**
**Alteração**: Aumentar o tamanho do bloco.

**Como melhora a segurança**: 
Um bloco maior aumenta o número de combinações possíveis de blocos de texto. Com um bloco maior, a criptografia pode distribuir melhor a informação e a diferença entre as entradas e saídas de uma rodada é mais pronunciada. Além disso, o aumento do tamanho do bloco reduz a probabilidade de colisões (duas entradas diferentes gerando a mesma saída), o que dificulta ataques baseados em tentativas de correspondência de blocos.

**Por que isso melhora a segurança?**: Com blocos maiores, a complexidade do algoritmo aumenta, tornando mais difícil realizar um ataque de força bruta ou de análise de blocos repetidos. O atacante teria que tentar um número muito maior de combinações para quebrar o sistema.

### c) **Tamanho da chave**
**Alteração**: Aumentar o tamanho da chave.

**Como melhora a segurança?**
Aumentar o tamanho da chave aumenta o número de possíveis chaves que podem ser utilizadas no algoritmo, tornando os ataques de força bruta mais difíceis. Se o tamanho da chave for muito pequeno, a chave pode ser quebrada rapidamente, mesmo com uma grande quantidade de poder computacional. Aumentar a chave torna o sistema mais robusto contra ataques desse tipo.

**Por que isso melhora a segurança?**: Chaves maiores resultam em mais combinações possíveis, o que dificulta a tentativa de adivinhar a chave correta (força bruta). Quanto maior a chave, maior o esforço necessário para tentar todas as possibilidades.

### d) **Função F**
**Alteração**: Alterar a função de mistura \( F \) usada na cifra de Feistel (como a função de expansão, substituição e permutação).

**Como melhora a segurança?**: 
A função \( F \) é crucial para criar a confusão e a difusão no algoritmo. Ao tornar a função \( F \) mais complexa e não linear, você aumenta a dificuldade de ataques como análise linear ou diferencial. A ideia é garantir que cada bit do texto cifrado dependa de todos os bits da chave e do texto claro de maneira não trivial. A função \( F \) é onde ocorre a maioria da "mistura" de dados, então, uma função forte e bem projetada é essencial para segurança.

**Por que isso melhora a segurança?**: Uma função \( F \) mais robusta torna o algoritmo mais resistente a ataques de criptoanálise. Quanto mais difícil for encontrar padrões ou relações simples entre a entrada e a saída da função \( F \), mais seguro será o algoritmo como um todo.

### e) **Efeitos indesejados das melhorias de segurança**
Embora o aumento da segurança através desses parâmetros seja benéfico, há efeitos colaterais que podem surgir:

1. **Desempenho**: 
   - **Aumento do número de rodadas** ou do **tamanho do bloco** geralmente resulta em um aumento significativo no tempo de processamento, o que pode ser um problema em sistemas com recursos limitados (como dispositivos móveis ou em tempo real).
   - Aumentar o **tamanho da chave** também pode impactar o desempenho, especialmente quando se precisa realizar operações de chave grandes ou de gerenciamento de chaves em grandes volumes de dados.
   
2. **Complexidade de implementação**:
   - Alterar a **função \( F \)** pode aumentar a complexidade da implementação e da verificação de correção do algoritmo. Funções mais complexas podem ser mais difíceis de testar e certificar que estão seguras, além de aumentar o custo computacional.

3. **Compatibilidade**:
   - Se o sistema criptográfico for usado em uma rede ou em dispositivos com recursos limitados, aumentar parâmetros como o **tamanho do bloco** ou **o número de rodadas** pode causar problemas de compatibilidade, já que sistemas legados podem não ser capazes de processar blocos maiores ou funções mais complexas de forma eficiente.

Em resumo, embora aumentar a segurança através desses parâmetros melhore a resistência contra ataques, pode haver trade-offs, especialmente em termos de desempenho e implementação.



## 6) Para uma cifra de bloco com uma chave de tamanho n bits, quantas tentativas um ataque de força bruta precisa, em média, para ter sucesso? Explique.
Para uma cifra de bloco com uma chave de tamanho **n bits**, um ataque de força bruta precisaria de, em média, **2^(n-1)** tentativas para ter sucesso. Isso ocorre porque, em um ataque de força bruta, todas as possíveis combinações de chaves são testadas até que a correta seja encontrada. Como há **2^n** possíveis chaves (já que cada bit pode ser 0 ou 1), e o ataque testa as chaves de forma aleatória ou sequencial, em média, ele precisará testar metade do espaço de chaves (2^(n-1)) antes de encontrar a chave correta. Por exemplo, para uma chave de 128 bits, seriam necessárias, em média, 2^127 tentativas. Esse valor exponencial é o que torna o ataque de força bruta inviável para chaves grandes em termos de tempo e recursos computacionais.

## 7) Com o modo ECB, se houver um erro em um bloco do texto cifrado transmitido, somente o de texto claro correspondente é afetado; porém, no modo CBC, esse erro se propaga. Por exemplo, um erro no C1 transmitido (figuras abaixo) obviamente adultera P1 e P2.

a) Algum bloco além de P2 é afetado? Suponha que haja um bit errado na versão fonte de P1. Por quantos blocos
de texto cifrado esse erro é propagado? Qual é o efeito no receptor?
No modo CBC, um erro em C1 afeta diretamente P1 e P2, pois a decifra de P1 depende de C1 e P2 depende de C1. Se houver um erro em P1 antes de ser cifrado, ele causará um erro em C1 e propagará para C2, afetando tanto P1 quanto P2 no receptor. O erro se propaga para dois blocos: C1 e C2. O receptor decifrará a mensagem com erros.


| Modo de Operação | a) Gera blocos cifrados iguais para blocos de texto claro iguais? | b) Permite paralelização da encriptação? | c) Permite paralelização da decriptação? | d) Efeito de um erro de bit na decriptação |
|------------------|-------------------------------------------------------------|----------------------------------------|----------------------------------------|------------------------------------------|
| **ECB**          | Sim, pois cada bloco é cifrado independentemente.           | Sim, pois cada bloco é cifrado de forma independente. | Sim, pois cada bloco é decifrado de forma independente. | Erro afeta apenas o bloco com o erro. |
| **CBC**          | Não, pois usa o bloco cifrado anterior como feedback (XOR).   | Não, pois a cifração de cada bloco depende do bloco cifrado anterior. | Sim, pois a decifração pode ser feita em paralelo após o XOR com o bloco cifrado anterior. | Erro afeta o bloco atual e o próximo, devido ao encadeamento. |
| **CFB**          | Não, pois usa o bloco cifrado anterior como feedback.         | Não, pois a cifração de cada bloco depende do bloco cifrado anterior. | Não, pois a decifração de cada bloco depende do bloco cifrado anterior. | Erro afeta o bloco atual e propaga para os próximos. |
| **OFB**          | Não, pois usa um keystream gerado a partir do vetor de inicialização (IV). | Não, pois o keystream é gerado sequencialmente. | Não, pois o keystream é gerado sequencialmente. | Erro afeta apenas o bit correspondente, sem propagação. |
| **CTR**          | Não, pois usa um contador único para cada bloco.               | Sim, pois cada bloco pode ser cifrado independentemente usando o contador. | Sim, pois cada bloco pode ser decifrado independentemente usando o contador. | Erro afeta apenas o bit correspondente, sem propagação. |

