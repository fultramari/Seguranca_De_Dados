# Lista 2 de exercícios - Segurança de Dados
## Exercício 
### 1a) **Expressão para a decriptação**
A decriptação de uma cifra de fluxo que utiliza XOR é feita de forma simples. Se a cifra é dada por \( C_i = M_i \oplus K_i \), a decriptação é dada por \( M_i = C_i \oplus K_i \). Isso funciona porque a operação XOR é invertível: \( (M_i \oplus K_i) \oplus K_i = M_i \), permitindo recuperar a mensagem original.

### b) **O que precisa ser feito para que a cifra seja one-time pad?**
Para que a cifra seja um **one-time pad** (OTP), a chave precisa ser:
1. **Aleatória**: Deve ser gerada de forma imprevisível, sem padrões.
2. **Do mesmo tamanho que a mensagem**: A chave deve ter o mesmo número de bits da mensagem para garantir que cada bit da mensagem seja cifrado por um bit único da chave.
3. **Usada apenas uma vez**: A chave não pode ser reutilizada em outra mensagem, garantindo que a segurança não seja comprometida.

Essas condições garantem a segurança do OTP, tornando-o incondicionalmente seguro.

### c) **Relação entre o tamanho da mensagem e da chave em uma cifra de bloco**
Em uma cifra de bloco, a chave deve ser do tamanho suficiente para cifrar todos os blocos de dados. Se a mensagem tem \( m \) bits e a cifra opera em blocos de \( n \) bits, então a chave precisa ter pelo menos \( m \) bits, para garantir que não haja reutilização da chave entre os blocos.

### d) **Dificuldades práticas de usar um one-time pad de fluxo**
As principais dificuldades de usar um **one-time pad** de fluxo incluem:
1. **Geração e distribuição da chave**: A chave precisa ser aleatória e tão longa quanto a mensagem, o que é difícil de garantir de forma segura em larga escala.
2. **Armazenamento e gerenciamento de chaves**: A chave precisa ser armazenada de forma segura e descartada após o uso, o que é complexo em sistemas grandes.
3. **Escalabilidade**: A produção e distribuição de grandes quantidades de chaves para mensagens longas ou frequentes é um grande desafio, tornando o uso do OTP prático apenas em casos específicos.
