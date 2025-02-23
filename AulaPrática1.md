# Segurança de Dados
* Anotações da parte prática da disciplina Segurança de Dados, com o professor Rodrigo Augusto Cardoso, 2025.1

## Exercícios

### 6. O que faz o comando cd, pwd, ls?
* Comando cd: O comando é uma abreviação para "Change Directory". O comando permite acessar um diretório/pasta do computador, e caso o nome da pasta não exista, uma nova é criada.
* Comando pwd: O comando é uma abreviação para "Print Working Directory". O comando permite visualizar todo o caminho do diretório em que o terminal se encontra
* ls : o Comando é uma abreviação para "List fileS". O comando permite visualizar todos os arquivos de determinado diretório/pasta/caminho.

### 7. Por que o comando “cd /tmp” foi usado em vez de “cd tmp”?
* Posteriormente, o diretório acessado era o "etc". Ao utilizar o comando "cd tmp", o linux presume um caminho relativo, ou seja, a pasta tmp está dentro da pasta tmp (o que não é verdade). Logo, ao rodar cd tmp, o comando resulta em "no such file or directory"
* O comando cd /tmp informa o caminho absoluto, mencionando explicitamente que o tmp não se encontra no diretório /etc/tmp( o que é presumido caso tente rodar apenas cd tmp).


### 8. Para que servem os parâmetros "-a" e "-l" do comando ls
    * ls -a : list "all" files. Lista todos os arquivos, inclusive os ocultos
    * ls -l: list "long" files. Lista os arquivos de forma mais detalhada, mas não mostra os arquivos ocultos.
    * la -la : list "all" e "long" files. Lista todos os arquivos de forma mais detalhada, incluindo os arquivos ocultos


### 9. O que os comandos “seq”, “cat”, “head”, “tail” fazem?
  * seq : "Sequence". Imprime uma sequência de números dado um intervalo. (Exemplo : seq 1 10)
  * cat: "catch = pegar". Pega as informaçoes do arquivo txt e exibe no terminal. (Exemplo: cat teste.txt)
  * head: exibe os primeiros 10 elementos da lista. É possível especificar a quantia utilizando head -n 5. Nesse caso, apenas os 5 primeiros seriam impressos. (Exemplo: head n-5 teste.txt)
  * tail: Exibe os 10 últimos elementos da lista; É possíel espeficiar a quantia utilizando tail -n 5 (nesse caso, apenas os 5 últimos seriam impressos).

### 10. O que os comandos “cp” e “rm” fazem?
  * cp : Copia o conteúdo de um arquivo para um outro arquivo. (Exemplo: cp teste1.txt teste2.txt
  * rm : Remove/deleta um determinado arquivo. (Exemplo: rm teste1.txt)

### 11. Como a opção “-n” dos comandos “head” e “tail” funciona?
  * head: exibe os primeiros 10 elementos da lista. É possível especificar a quantia utilizando head -n 5. Nesse caso, apenas os 5 primeiros seriam impressos. (Exemplo: head n-5 teste.txt)
  * tail: Exibe os 10 últimos elementos da lista; É possíel espeficiar a quantia utilizando tail -n 5 (nesse caso, apenas os 5 últimos seriam impressos).


### 12. Qual a diferença entre “seq 1 20” e “seq 1 20 > teste.txt”?
O primeiro comando lista os números do intervalo dado no terminal e não armazena em nenhum lugar. Já o segundo salva a sequência no arquivo de texto, mas não exibe no terminal.

### 13. O que os comandos “mkdir” e “mv” fazem?
  * mkdir : "make directory". Cria uma nova pasta/diretório. (Exemplo: mkdir pasta1)
  * mv : "move". Move ou renomeia um determinado arquivo. Quando um ou dois parâmetros são diretórios, a ideia é de mover. Quando ambos parâmetros são nomes, ocorre a renomeação.

### 14. Para que serve a opção “-r” dos comandos “cp” e “rm”?
  * cp -r : Viabiliza a cópia de todo um diretório para um outro diretório. sem o -r, é possível apenas copiar um arquivo. com o -r (o "r" vem de recursão) todos os arquivos são copiados.
  * rm -r : Enquanto o comando rm apenas remove arquivos, o comando rm -r remove todo o conteúdo do diretório 


### 15. O que significa “..” no comando “cd ..”?
.. Indica que volte para o caminho superior.

### 16. Para que serve o caracter “#” no terminal?
Para digitar comentários.


## Editores vi, vim e nano
* vi: vi "Nome do arquivo".txt
  * ao Acessar o arquivo, aperte "i" para poder editar o arquivo. após isso, aperte a tecla ctrl c para sair do modo editor, e digite :wq para salvar e sair.

* vim : Mesma coisa que o vi, sendo o "vi" Melhorado.

* nano: Interface intuítiva, mais fácil de mexer.



### 17. Para que servem os comandos “ps” e “top”?
### 18. Para que serve o comando “grep””?
### 19. Para que serve o “|” em “ps -ef | grep nano””?
### 20. Para que serve o comando “kill”?
