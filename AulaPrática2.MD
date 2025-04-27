##Perguntas
### 1) Qual comando decifra o arquivo “criptografado.txt” gerado pelo comando mostrado nesta tarefa?
R: Para decifrar o arquivo, basta usar o comando mostrado no exercício como base. Contudo, para decriptografar, o arquivo de entrada será "criptografado.txt", o parâmetro -e de encriptação se torna -d de de criptação, e o arquivo de saída será "decriptografado.txt".Desse modo, teremos:
```
openssl enc -aes-128-cbc -d -in criptografado.txt -out decriptografado.txt -K 00112233445566778899aabbccddeeff -iv 0102030405060708
```

### 2) Provavelmente você recebeu a mensagem “hex string is too short, padding with zero bytes to length” ao cifrar o arquivo texto. Explique por que isso aconteceu.
R: De acordo com o comando, o algorítmo funciona com 128 bits, o que é um valor alto considerando o tamanho da mensagem do arquivo txt. Por isso, é sugerido que seja feito o padding, para que a mensagem tenha o tamanho de 128 bits.


### 3) Para que serve o vetor de inicialização no modo CBC?
R: Serve para fazer XOR com o primeiro bloco do texto claro

### 4) Além do AES, que outros algoritmos podem ser usados no SSL? E que outros modos de operação podem ser usados?
R: Algorítmos: 3DES, ChaCha20,Camelia,RC4,IDEA 
Modos de operação: CBC,GCM,CCM,ChaCha20-poly1305

### 5) Qual é a sequência de comandos que você usou para gerar as imagens cifradas?
```
head -c 54 pic_original.bmp > header
tail -c +55 pic_original.bmp > body
openssl rand 16 > key.bin
openssl enc -aes-128-ecb -K $(xxd -p key.bin) -nosalt -in body -out body_ecb
cat header body_ecb > pic_ecb.bmp
openssl rand 16 > iv.bin
openssl enc -aes-128-cbc -K $(xxd -p key.bin) -iv $(xxd -p iv.bin) -nosalt -in body -out body_cbc
cat header body_cbc > pic_cbc.bmp
```

### 6) Como ficaram as imagens obtidas depois da criptografia com os modos ECB e
CBC? Qual dos modos é mais seguro para cifrar os arquivos? Por que?
R: No modo ECB, por cifrar blocos de informação semelhante da mesma forma, fez com que as partes da mesma cor fossem criptografadas da mesma forma na imagem, de modo que ainda seja possível ver, ainda que com certo desfoco e dificuldade, a imagem.
Já no modo CBC, por ter maior difusão pelo bloco anterior participar do processo de encriptação do seu bloco sucessor, a cifragem de blocos semelhantes serão distintas, de modo que a imagem fique muito mais difícil de se enxergar. Portanto, o método CBC é melhor para imagens.


### 7) Quais foram os caracteres de preenchimento usados para cada um dos arquivos?
Quantos blocos os arquivos cifrados têm?
Após o preenchimento, os arquivos cifrados de 5 e 10 bytes ficaram com 16 bytes (1 bloco). A escolha do caractere de preenchimento é baseada em quantos bytes faltam para completar 1 bloco. No caso de 5 bytes, como faltam 11 bytes, o caractere de preenchimento é 0B, que é onze em hexadecimal. No caso de 10 bytes, como faltam 6 bytes, o caractere de preenchimento é 06, que é 6 em hexadecimal.
O caso de 16bytes é particular. Apesar de ter um bloco fechado, um bloco a mais é criado por padrão. Como faltam 16 bytes, que é um bloco completo, o segundo bloco é preenchido com 10, que é 16 em hexadecimal.

### 8) Considere o ECB, CBC, CFB, e OFB. Quais deles usam preenchimento? E quais
não usam?
Apenas o ECB e o CBC usaram padding, isso por serem cifras de bloco. Como CFB e OFB são cifras de fluxo, não utilizam padding.

### 9) O que aconteceu ao cifrar o mesmo texto com IVs iguais? E IVs diferentes? Por que
isso acontece?
Cifrando o mesmo texto com IVs iguais, foram obtidos textos criptados iguais. Com IV'S diferentes, os textos criptados são distintos. Isso ocorre por conta do mecanismo do CBC, que antes de criptografar, realiza XOR do IV com o texto claro. Isso faz com que, com o mesmo IV, o XOR tenha o mesmo resultado. Não só isso, mas Mensagens iguais com o mesmo IV serão criptografadas e serão exatamente iguais, o que pode ser problemático. Por isso é importante sempre usar IV's distintos, pois com essa diferença, mensagens iguais são criptadas de formas diferentes.

### 10) Bob enviou “Yes” ou “No” na primeira mensagem?
R: Bob enviou "Yes" na primeira mensagem.

### 11) Escreva a equação que representa a mensagem enviada ao oráculo para descobrir a resposta. Explique cada termo da equação e por que o ataque funciona.
R: * Uma primeira informação importante é que foi restringido a possibilidade de resposta. Ou era "Sim", ou "Não". Essa redução de escopo que viabiliza a tentativa e erro.
  * Saber os vetores de inicialização é um segundo fator que possibilita a descoberta.
  * Ter a mensagem cifrada do bob é o terceiro fator que possibilidade a descoberta.

#### RESOLUÇÃO: Vamos considerar, por chute, que Bob escreveu "Sim". 
1) Considere C1 a mensagem encripatada do Bob, IV o vetor utilizado por ele, P2 a mensagem que vamos passar para o oráculo e IV' nosso vetor de inicialização. A equação que possibilita descobrir é:
(P2 ⊕ IV') ⊕ IV

2)  Como essa mensagem toda vai passar pelo processo CBC, ela sofrerá XOR com o IV' e depois será criptografada usando AES:
AES(Mensagem ⊕ IV') = AES( ((P2 ⊕ IV') ⊕ IV) ⊕ IV') = AES (P2 ⊕ IV).

3) Considere o cenário em que, por chute, acertamos que Bob escreveu "Sim". Perceba que nesse caso, a mensagem P2 será criptografada e ficará idêntica ao texto criptografado C1 de Bob:  
C1 = AES(P1 ⊕ IV)  
C2 = AES( P2 ⊕ IV' ⊕ IV ⊕ IV') = AES (P2 ⊕ IV).  
Partindo da ideida de que P1 = P2, logo:  
AES(P1 ⊕ IV) = AES (P2 ⊕ IV), e portanto, as mensagens criptografadas serão iguais.


