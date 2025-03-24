# Ataque de Descriptografia Cega (Blind Decryption Attack)

Esse cenário descreve um **ataque de descriptografia cega** (ou *blind decryption attack*), onde Eva explora a capacidade de Bob de assinar mensagens para obter a descriptografia de um texto cifrado \( C \) sem que Bob saiba o que está descriptografando. Vamos detalhar como Eva pode fazer isso.

---

## 1. Contexto do Problema

- **Chave pública de Bob:** \( (e, n) \).
- **Chave privada de Bob:** \( d \), onde \( d \equiv e^{-1} \ (\text{mod} \ \phi(n)) \).
- **Texto cifrado interceptado por Eva:** \( C \equiv P^e \ (\text{mod} \ n) \), onde \( P \) é o texto claro que Alice enviou para Bob.
- **Método de assinatura de Bob:** Para uma mensagem \( M \), Bob calcula a assinatura \( S \equiv M^d \ (\text{mod} \ n) \).

Eva quer descobrir \( P \), mas não pode pedir diretamente a Bob para descriptografar \( C \). Em vez disso, ela pede a Bob para assinar uma mensagem \( M \) que ela escolheu de forma especial.

---

## 2. Estratégia de Eva

Eva escolhe um número aleatório \( r \) que é relativamente primo com \( n \) (ou seja, \( \text{mdc}(r, n) = 1 \)). Ela então constrói a mensagem \( M \) da seguinte forma:

\[
M \equiv r^e \cdot C \ (\text{mod} \ n)
\]

Eva pede a Bob para assinar \( M \). Bob, sem saber que \( M \) está relacionado a \( C \), calcula a assinatura \( S \):

\[
S \equiv M^d \ (\text{mod} \ n)
\]

Substituindo \( M \) na equação acima:

\[
S \equiv (r^e \cdot C)^d \ (\text{mod} \ n)
\]

Usando as propriedades do RSA e a definição de \( C \equiv P^e \ (\text{mod} \ n) \), podemos simplificar \( S \):

\[
S \equiv (r^e \cdot P^e)^d \ (\text{mod} \ n)
\]

\[
S \equiv r^{e \cdot d} \cdot P^{e \cdot d} \ (\text{mod} \ n)
\]

Sabemos que \( e \cdot d \equiv 1 \ (\text{mod} \ \phi(n)) \), então:

\[
S \equiv r^1 \cdot P^1 \ (\text{mod} \ n)
\]

\[
S \equiv r \cdot P \ (\text{mod} \ n)
\]

---

## 3. Recuperando o Texto Claro \( P \)

Eva recebe \( S \equiv r \cdot P \ (\text{mod} \ n) \). Como ela escolheu \( r \) e conhece \( r \), ela pode resolver para \( P \):

\[
P \equiv S \cdot r^{-1} \ (\text{mod} \ n)
\]

Aqui, \( r^{-1} \) é o inverso multiplicativo de \( r \) módulo \( n \). Como \( r \) foi escolhido para ser relativamente primo com \( n \), o inverso \( r^{-1} \) existe e pode ser calculado usando o algoritmo estendido de Euclides.

---

## 4. Passos Resumidos

1. **Eva escolhe \( r \):** Um número aleatório relativamente primo com \( n \).
2. **Eva constrói \( M \):** \( M \equiv r^e \cdot C \ (\text{mod} \ n) \).
3. **Eva pede a Bob para assinar \( M \):** Bob retorna \( S \equiv M^d \ (\text{mod} \ n) \).
4. **Eva calcula \( P \):** \( P \equiv S \cdot r^{-1} \ (\text{mod} \ n) \).

---

## 5. Conclusão

Eva consegue recuperar o texto claro \( P \) sem que Bob saiba que ele estava descriptografando \( C \). Esse ataque funciona porque Eva explorou a propriedade homomórfica multiplicativa do RSA e a capacidade de Bob de assinar mensagens sem verificar o conteúdo delas.

---

## 6. Como Evitar Esse Ataque

Para evitar esse tipo de ataque, Bob deve **nunca assinar mensagens cegas** (ou seja, mensagens que ele não conhece ou não verificou). Uma prática comum é exigir que as mensagens a serem assinadas sejam "hasheadas" ou incluam um valor de nonce (número aleatório único) para garantir que Bob não esteja assinando algo que possa ser usado para enganá-lo. Além disso, o uso de esquemas de assinatura mais seguros, como RSA-PSS, pode mitigar esse tipo de vulnerabilidade.
