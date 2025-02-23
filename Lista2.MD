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

