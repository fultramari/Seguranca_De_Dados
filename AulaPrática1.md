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
- **`ps`**: O comando `ps` (abreviação de **process status**) é usado para exibir informações sobre os processos que estão em execução no sistema. Ele mostra detalhes como o ID do processo (PID), o tempo de execução, o usuário que iniciou o processo e o comando utilizado. Existem várias opções para personalizar a saída, como `ps -f` para uma visão mais detalhada, ou `ps -ef` para listar todos os processos no sistema.
  
- **`top`**: O comando `top` exibe uma lista dinâmica dos processos que estão sendo executados no sistema. Ele fornece uma visão em tempo real dos processos e seus recursos, como CPU, memória, etc. Ele é mais interativo, permitindo que você interaja com a visualização e classifique ou mate processos diretamente dentro da interface.

### 18. Para que serve o comando “grep”?
- O comando **`grep`** (abreviação de **Global Regular Expression Print**) é usado para buscar texto dentro de arquivos ou a saída de outros comandos que correspondam a um padrão especificado. O `grep` utiliza expressões regulares para encontrar e mostrar as linhas que coincidem com o padrão fornecido. No exemplo `ps -ef | grep nano`, ele procura por processos cujo nome contenha "nano".

### 19. Para que serve o “|” em “ps -ef | grep nano”?
- O **`|`** (pipe) é um operador utilizado para **encadear comandos** no terminal. Ele pega a saída de um comando à esquerda e a passa como entrada para o comando à direita. No caso de `ps -ef | grep nano`, a saída do comando `ps -ef` (que lista todos os processos) é passada como entrada para o comando `grep nano`, que filtra e exibe apenas as linhas que contêm a palavra "nano", ou seja, os processos relacionados ao editor de texto `nano`.

### 20. Para que serve o comando “kill”?
- O comando **`kill`** é utilizado para enviar um sinal a um processo em execução, normalmente com a intenção de **finalizá-lo** (terminar o processo). O uso mais comum do `kill` é passar o **PID (ID do processo)** de um processo que se deseja terminar. Por exemplo, `kill <PID>` envia um sinal padrão (SIGTERM) para o processo, solicitando sua finalização. Em alguns casos, se o processo não responder a SIGTERM, pode-se usar o sinal **SIGKILL** com o comando `kill -9 <PID>` para forçar a finalização.


### 21. Para que serve o comando “man”?
- O comando **`man`** (abreviação de **manual**) é usado para exibir o manual de outros comandos no sistema. Ele fornece uma documentação detalhada sobre como usar um comando, suas opções e exemplos de uso. Para sair da visualização do manual, você pode pressionar a tecla `Q`.

### 22. Para que serve o comando “ping”?
- O comando **`ping`** é usado para testar a conectividade de rede entre o seu computador e outro host (como um servidor ou um site). Ele envia pacotes de **ICMP Echo Request** para o host de destino e espera por uma resposta (**Echo Reply**), ajudando a verificar se o host está acessível e a medir o tempo de resposta da rede.

### 23. Para que serve o comando “history”?
- O comando **`history`** exibe uma lista de todos os comandos executados no terminal anteriormente. Ele ajuda a revisar o histórico de comandos e pode ser útil para repetir ou verificar comandos usados recentemente.

### 24. Qual a diferença entre “>” e “>>”?
- **`>`**: Usado para **sobrescrever** o conteúdo de um arquivo. Se o arquivo já existir, ele será substituído.
  - Exemplo: `seq 1 10 > teste.txt` cria (ou sobrescreve) o arquivo `teste.txt`.
  
- **`>>`**: Usado para **adicionar** (append) conteúdo a um arquivo existente. Se o arquivo não existir, ele será criado.
  - Exemplo: `seq 1 10 >> teste.txt` adiciona os números de 1 a 10 ao final de `teste.txt`.

### 25. O que o comando “wc” faz?
- O comando **`wc`** (abreviação de **word count**) é usado para contar o número de linhas, palavras e caracteres em um arquivo. Exemplo: `wc teste.txt` exibe a quantidade de linhas, palavras e caracteres presentes no arquivo `teste.txt`.


