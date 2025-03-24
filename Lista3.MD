## 4- Suponha que um algoritmo de hash não atende ao requisito de resistência à pré-imagem. Exemplifique um ataque que pode ser feito a uma aplicação que use esse algoritmo. Explique qual aplicação foi considerada e como o ataque funciona.
R: Por não atender a resistência à pré iamgem, significa que é computacionalmente possível encontrar um x tal que H(x) = m. Considere um banco de dados que armazene o hash da senha de usuários. Por meio da força bruta, seria possível encontrar a senha dos usuários, uma vez que não tem resistência à pré imagem.

## 5- Suponha que um algoritmo de hash atende ao requisito de resistência à pré-imagem mas não atende ao requisito de resistência à segunda pré-imagem. Exemplifique um ataque que pode ser feito a uma aplicação que use esse algoritmo. Explique qual aplicação foi considerada e como o ataque funciona.
R: Considere a mesma aplicação. Nesse caso, por não ter resistência à segunda pré-imagem, seria computacionalmente possível encontrar valores diferentes da senha do usuário que gerassem o mesmo hash, sendo possível invadir as contas e afetar a integridade e confidencialidade do sistema.

## 6) Algoritmos de assinatura digital usam algoritmos de criptografia assimétrica. Por que não seria possível usar criptografia simétrica nesse caso?

A **criptografia simétrica** não é usada em assinaturas digitais porque:

1. **Compartilhamento de chave:** A mesma chave é usada para criptografar e descriptografar, o que permite que qualquer um com a chave falsifique assinaturas.
2. **Falta de não repúdio:** Não é possível provar que apenas o remetente assinou a mensagem.
3. **Escalabilidade:** Cada par de usuários precisa de uma chave única, o que é inviável em sistemas grandes.

Já a **criptografia assimétrica** resolve esses problemas:

1. **Chave privada:** Apenas o remetente pode assinar.
2. **Chave pública:** Qualquer um pode verificar a assinatura sem poder falsificá-la.
3. **Escalável:** Cada usuário tem um par de chaves, independentemente do número de usuários.

