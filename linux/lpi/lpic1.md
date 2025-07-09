## Curso preparatório para  LPIC-1
---

> O Linux Professional Institute é uma organização canadense sem fins lucrativos e voltada para certificações para Linux, BSD e tecnologias baseadas em software de código aberto. Foi fundada em outubro de 1999.

>O Linux Professional Institute é uma organização canadense sem fins lucrativos e voltada para certificações para Linux, BSD e tecnologias baseadas em software de código aberto. Foi fundada em outubro de 1999.
Promove o programa de certificação multinível em sistemas Linux, e as certificações são reconhecidas internacionalmente por empresas, empregadores e profissionais de TI.
As provas são baseadas no Linux Standard Base, um conjunto de normas que mantém a compatibilidade entre as diferentes versões e distribuições do sistema operacional sendo a certificação, é independente da distribuição.

#### Programa de certificação multinivel 

* LPIC-1 ⇒ Válida a proficiência do candidato na administração Linux
* LPIC-2 ⇒ Para quem já tem experiência e implementar servidores
* LPIC-3 ⇒ São especializações para profissionais experientes
    * Mixed environment - Ambientes onde há integrações entre sistemas por exemplo linux e windows utilizando Samba, Active Directory etc…
    * Security - Segurança 
    * Virtualization & HA - Virtualização e projetos de alta performance


#### Sobre a prova

* Cada exame tem 60 questões
* tempo 90 minutos
* Pontuação Mínima para aprovação 500,  máxima 800
* Os exames podem ser feitos nos centros autorizados pela PearsonVue
* Disponiveis em varios idiomas 
* Validade do nível 1 é de 5 anos
* Para renovar pode ser refeito o teste ou fazer a prova para Níveis acima

#### Tópico 103.1 - Linha de comando(Shell) (Seção3 - Peso4)

> Shell é o interpretador de comandos do sistema que produz resultados se os comandos forem válidos.

>Existem diferentes tipos de shells, e cada um possui configurações e funcionalidades específicas. Para saber quais estão disponíveis use o comandos abaixo:
```sh
$ chsh -l 

$ cat /etc/shells
```

> Em um sistema o shell fica posicionado uma camada acima do kernel junto com as bibliotecas

|                                                |
| :--------------------------------------------: |
|               Programas comandos               |
| Shell(Interpretador de comandos) - Bibliotecas |
|                     Kernel                     |
|                                                |

##### Shell bash 

>Também conhecido por Bourne Again Shell, por ter sido desenvolvido por Stephen Bourne, o criador do shell anterior(/bin/sh).

>O bash é compatível com sh, mas contem melhorias nos recursos de função e programação. Ele incormpora recursos do Korn shell (ksh) e do C shell (csh). e se destina a ser compatível com POSIX.

>Após o login o prompt aguarda comandos de entrada para interagir com o sistema, e esses podem ser:

>Internos(Builtins) - São comandos internos do bash

>Externos - Programas armazenados no HD, que podem ser executados por um caminho absoluto ou contidos no PATH das variáveis de ambiente.

>Para saber se o comando é interno ou externo execute o comando type seguido do comandname:

```sh 
$   type pwd
```

>O shell trabalha com níveis de sessões. Para saber a sessão que está logado acesso o valor da variável de ambiente $SHLVL

```sh
echo $SHLVL   
/usr/bin/bash  //inicia uma nova sessão do shell
```

##### Comandos
---

##### alias

> O comando alias é utilizado para criar um apelido para outro comando ou para uma cadeia de comandos.

>O comando  **alias**  ou  **alias -p** exibe a lista de alias para comandos e para criar um novo alias use como no exemplo 

```sh
alias ls=”ls –color=auto”
```

>Os alias criados só permanecem enquanto logado na sessão

### Sequencia de comandos

> Separando por ponto e vírgula  é possível executar uma sequência de comandos no shell veja no exemplo:

```sh
 cat /proc/cpuinfo; ls -l /; date;
```

> Também é possível utilizar AND lógico ou OR lógico, 

> **AND**, os comandos são separados por “&&” e se ocorrer alguma falha na execução do primeiro comando, o  segundo não será executado.

```sh
comando1 && comando2 && comando3
```

**OR**, os comandos são separados por “||” e se ocorrer alguma falha na execução do primeiro comando, o segundo será executado.

```sh
comando1 || comando2 
```

### Substituição de comandos

\`comando\`  ou $(comando)

Exemplo:
```sh
grep -i ext4 /boot/config-`uname -r` 

rpm -qf $(which ifconfig)
```

##### history

> O histórico de comandos do shell fica armazenado no arquivo .bash_history na pasta do usuário. Esse arquivo é atualizado somente quando o usuário finaliza a sessão 
```sh
history       ⇐ Lista os últimos comandos executados na linha de comando
!3            ⇐ Executa o terceiro comando do history
history -c    ⇐ Limpa o histórico de comandos armazenados em buffer “.bash_history”
```

### Variáveis de ambiente

```sh 
$HISTFILE		    ⇐ Armazena o endereço absoluto do .bash_history
$HISTSIZE		    ⇐ Define a quantidade máxima de comandos que ficarão armazenados no buffer de memória
$HISTFILESIZE		⇐ Define a quantidade máxima de comandos que ficarão armazenados no .bash_history

```

### Variáveis em shell (LOCAL e GLOBAL)

> As regras para nomenclatura de variáveis são: Somente letras, números e underline, o nome da variável só pode iniciar com letra ou underline

> Para definir uma variável no escopo global, ou seja, para ser visível em outras sessões sub shell use o comando export antes da atribuição. Ou seja na sessão 1 é possível definir valores para as sessões 2,3,4,5….. o contrário não funciona

```sh
export  variavelx=123	⇐ Exportar a variável para os subshells em níveis abaixo de onde foi definido
unset nome_da_variavel 	⇐ remove variavel
set 				    ⇐ Exibe as variáveis do usuário
env				        ⇐ Exibe as variaveis globais do sistema
echo $nome_da_var		⇐ Comando para exibir o valor da variável (o nome da variável deve ser precedida de $)

$PS1 				    ⇐ Define o formato do prompt de comando
$PS2				    ⇐ Define como será o formato do prompt de comando quando o prompt está aguardando finalizar o comando numa quebra de linhas
```

##### uname 			
Esse comando exibe informações do sistema conforme parâmetros abaixo:

```sh
uname -s 	<== Kernel 
uname -r 	<== Release do kernel (ls -l /boot)
uname -m 	<== Arquitetura da máquina
uname -p 	<== Arquitetura do processador
uname -n 	<== Nome da máquina
uname -a 	<== Exibe todas as informações anteriores

```

### Variáveis especiais

|     |                                                                                         |     |
| --- | --------------------------------------------------------------------------------------- | --- |
| $!  | PID do último processo executado em segundo plano(background).                          |     |
| $$  | PID do shell atual.                                                                     |     |
| $?  | Código de retorno do último comando executado. Veja alguns valores possíveis a seguir:  |     |
|     | 0 -  é para um comando bem sucedido.                                                    |     |
|     | 1 - para a maioria dos erros de comandos.                                               |     |
|     | 126 - Comando não é executável.                                                         |     |
|     | 127 - Comando não encontrado.                                                           |     |
|     | 130 - Quando o comando é interrompido com a combinação de teclas: ctrl + c (control c). |     |


---
### Manuais de comandos

##### whatis
> Descrição curta do que é o comando e o numero da sessão no manual:
>> Exemplo:
```sh
$ whatis passwd
passwd (5)           - arquivo de senhas
passwd (1)           - change user password
passwd (1ssl)        - OpenSSL application commands
```
##### apropos
> Pesquisa por nomes e descrições de páginas de manual
>> Exemplo:
```sh
$ apropos passwd
gpasswd (1)          - administra o arquivo /etc/group
passwd (5)           - arquivo de senhas
chgpasswd (8)        - update group passwords in batch mode
chpasswd (8)         - update passwords in batch mode
grub-mkpasswd-pbkdf2 (1) - generate hashed password for GRUB
openssl-passwd (1ssl) - compute password hashes
pam_localuser (8)    - require users to be listed in /etc/passwd
passwd (1)           - change user password
passwd (1ssl)        - OpenSSL application commands
pwhistory_helper (8) - Helper binary that transfers password hashes from passwd or shadow to opasswd
update-passwd (8)    - safely update /etc/passwd, /etc/shadow and /etc/group

```

##### man
>man é o paginador  de  manual do sistema. A tabela abaixo mostra os números seção do manual seguido pelos tipos de páginas que eles contêm.

|     |                                                                                               |
| --- | --------------------------------------------------------------------------------------------- |
| 1   | Comandos shell ou programas executáveis                                                       |
| 2   | Chamadas de sistema (funções fornecidas pelo kernel)                                          |
| 3   | Chamadas de biblioteca (funções dentro de bibliotecas de programa)                            |
| 4   | Arquivos especiais (geralmente localizados em /dev)                                           |
| 5   | Formatos de arquivo e convenções, ex.: /etc/passwd                                            |
| 6   | Jogos                                                                                         |
| 7   | Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7), man-pages(7) |
| 8   | Comandos de administração do sistema (geralmente apenas para root)                            |
| 9   | Rotinas do kernel [não padrão]                                                                |

> Para entender as sessões do manual usamos como exemplo o comando **passwd** e o arquivo **/etc/passwd**:
>> A documentação do comando passwd fica na sessão 1 e a documentação do arquivo na sessão 5

```sh
$ man 1 passwd
$ man 5 passwd
```

> Para buscar a palavra passwd em todos os manuais utilizamos o ```man -f palavra``` semelhante ao comando **whatis**, e para descrições curtas ```man -k palavra``` semelhante ao **apropos**.


/usr/share/man 	⇐ Pasta onde fica os manuais com seus níveis etc…


##### whereis 

> Localiza o binário do comando, fontes, e as páginas do manual referente ao comando

```sh
$ whereis passwd
passwd: /usr/bin/passwd /etc/passwd /usr/share/man/man5/passwd.5.gz /usr/share/man/man1/passwd.1.gz /usr/share/man/man1/passwd.1ssl.gz
```

##### which

> Localiza o binário do comando, fontes, e as páginas do manual referente ao comando

```sh 
$ which passwd
/usr/bin/passwd
```
---
 Quoting “ ‘ \ ;

> O uso de aspas simples e duplas, contra barra e ponto e vírgula no shell é bem parecido com as linguagens de programação como php por exemplo


* Aspas duplas é uma string porém se inserir uma variável dentro será interpretada como variável
* Aspas simples  os dados serão entendidos como string
* Barras de espaço é para continuar uma linha de comandos na próxima linha, ou seja, representa uma quebra de linha
* Ponto e vírgula é utilizado para separar uma sequência de comandos

### Obs:
> O conteúdo dentro de crases serão interpretados como comando semelhante ao utilizar cifrão com colchetes e o conteúdo dentro $(ls -l)


---
## Fluxos de texto

##### $ cat 

> Exibe o conteudo de um arquivo 
```sh
$ cat  arquivo		    ← Exibe o conteúdo de um arquivo
$ cat -n /etc/passwd	← Enumera todas as linhas 
$ cat -b /etc/passwd 	← Enumera somente as linhas preenchidas
```
##### $ nl
> Enumera a saida de um arquivo. Exemplo:
```sh
$ nl arquivo 		← Enumera a saída do conteúdo de um arquivo
$ cat arquivo | nl 	← Semelhante a opção -n do cat
```

##### $ wc
> Conta o número de caracteres de um ou mais arquivos;

```sh
$ wc -l *.txt
15 file1.txt
15 file2.txt
15 file3.txt
45 total
```

##### $ sort
> Exibe conteudo de um arquivo em ordem alfabética
```sh
$ sort -r file		← Ordena em ordem inversa
$ sort -f file		← Não separa iniciais maiúsculas ou minúsculas 
```

##### $ less
> Faz paginação do conteudo de um arquivo ou de resultado redirecionado ao comando:
```sh
$ cat /var/log/Xorg.1.log |less
```
> Obs: Permite buscar dados dentro do conteudo paginado utilizando ```/conteudo``` e enter

##### $ head  
>Exibe as 10 primeiras linhas de arquivos
```sh
$ head  file1 file2	
$ head	-n 20 file1 	← Exibe 20 linhas
$ head	-n -20  file1 	← Exibe todo o arquivo exceto as últimas 20 linhas

```


##### $ tail
> Exibe todo conteúdo de um arquivo e para no final. O tail é um comando muito util para analisar arquivos de logs
>> A opção -f mantem o arquivo aberto na linha de comando aguardando novas linhas para serem exibidas

> Uma alternativa ao tail é o multitail, com esse comando é possível monitorar mais de um arquivo simultaneamente.

```sh
$ tail file1.txt file2.txt file3.txt 
$ tail file.txt -n +10           # exibe todas as linhas do arquivo a partir da décima linha.
$ tail file.txt -n 15            # Exibe as últimas 15 linhas
$ tail file.txt -f		         # Exibe as últimas linhas do arquivo e fica aguardando mudanças no arquivo para exibir
$ nl file.txt | tail  -n +15 	 # Exibe o arquivo a partir da linha 15 
```


##### $ unique

```sh
$ unique file.txt		# suprime linhas repetidas que são iguais ()
$ unique file.txt	-d	# Exibe somente as linhas que se repetem e estão em sequência 
$ unique file.txt	-c	# A quantidade de vezes que uma ocorrência se repete 
```

##### $ od

> Exibe um conteúdo de arquivos em formatos como, octal, hexadecimal etc…

```sh
$ od filename  
```

> ```-t tipo``` Especifica o tipo de saída que o comando od deve gerar conforme lista abaixo:
>>* a - Nome do caractere;
>>* c - ASCII;
>>* o - Octal;
>>* x - Hexadecima

##### $ paste 			

> > Comando util para concatenar as linhas de diversos arquivos em colunas verticais. Ótimo para comparar arquivos

>Opções:
>>-  -d's'  Separa as colunas com o símbolo s nas aspas simples;
>>- -s       Concatena todo o conteúdo de um arquivo com uma linha para cada arquivo.

Exemplos:
```
# paste -s file1.txt file2.txt
linha1_file1  linha2_file1  linha3_file1  linha4_file1  linha5_file1  linha6_file1
linha1_file2  linha2_file2  linha3_file2  linha4_file2  linha5_file2  linha6_file2

# paste file1.txt file2.txt
linha1_file1  linha1_file2
linha2_file1  linha2_file2
linha3_file1  linha3_file2
linha4_file1  linha4_file2
linha5_file1  linha5_file2
linha6_file1  linha6_file2

# paste -d'@' file1.txt file2.txt
linha1_file1@linha1_file2
linha2_file1@linha2_file2
linha3_file1@linha3_file2
linha4_file1@linha4_file2
linha5_file1@linha5_file2
linha6_file1@linha6_file2
```

##### $ split

> divide um arquivo em outros menores 

```sh
split -l 3 file.txt  /destino/file_name_	#  Irá gerar arquivos menores com 3 linhas 
``` 

##### $ wc
```sh
$ wc -l /destino/file_name*    #Mostra o numero de linhas geradas nos arquivos 
```

##### Comandos uteis para gerar hash de arquivos

```sh
$ md5sum filename
# b67ad19397d41ea69b1156e03c066c37

$ sha256sum filename
# 941ffd73aab75eeed34dbe22012e7edde6606ba96398080196419ce14fd6c2a7

$ sha512sum filename
# 74323b475733cdcd39553dcb3af1fb266372210bd666e9346182e44e4a2430d0bf463a4dc1c49e19977d5b06f75b57814095091597cf9ebc21a43b406ad7f7a7

# Gerando hash de varios arquivos num diretorio:
$ md5sum *
```

##### $ sed

>Editor de texto não interativo

```sh
$ sed 's/conteudo_busca/conteudo_replace/' filename
```

> Observação: 
>> 1. A alteração só é efetiva no arquivo utilizando o parametro -i  ```sed -i ‘s/string/stringreplace/g’```
>> 2. No formato básico substitui somente a primeira ocorrencia da linha

```sh
$ sed 's/palavra/substituta/2'             # Substitui as duas primeiras ocorrencias
$ sed 's/palavra/substituta/g'             # Substitui todas as ocorrências da linha
$ sed '1,25d' filename                     # Exclui da linha 1 à 25
```

##### $ tr

> Transforma textos redirecionados de outros comandos
>> Opções:
>> 1. -d Apaga as ocorrências da variável de busca;
>> 2. -s Suprime as ocorrências repetidas da variável de busca;

> Exemplos

```sh
$ tr variavel_busca variavel_troca < arquivo.txt

#Transformar espaços para TABS em um arquivo
$ cat filename | tr ':[space]:' '\t' > out.txt

# Removendo espaços
$ cat filename | tr -d ' '

$ cat domains.txt
www.certificacaolinux.......com.br
www.kernel.org
www.nic.br

$ cat domains.txt | tr -s '.'
www.certificacaolinux.com.br
www.kernel.org
www.nic.br
```

##### $ cut

> Corta partes de um texto, baseado em caracteres, tabulações etc

```sh 
# -d’:’ o caractere que delimita as linhas, e -f 1,3 colunas a ser exibidas
$ cut -d’:’ -f 1,3	
# -c1-6 recorta da coluna 1 à 6 do arquivo
$ cut -c1-6		    

```
Exemplo:

```sh
# Pega só os logins das contas de usuários no arquivo /etc/passwd. Neste caso o delimitador será o ":" e a primeira coluna.
$ cut –d":" -f 1 /etc/passwd

# Imprime a primeira coluna de todas as linhas do arquivo
cut -b 1 file.txt                   

# As colunas 1, 3 e 5
cut -b 1,3,5 file.txt               

# As 12 primeiras colunas
cut -b 1-12 file.txt                

```

Opções:

* -b número: Imprime uma lista vertical com o byte número (da esquerda para direita);
* -c número: Imprime uma lista vertical com o caractere número (da esquerda para direita);
* -d delimitador: Configura o delimitador que separa uma coluna da outra. O padrão é o Tab;
* -f número: Imprime a coluna número.


##### $ file

> Verifica o tipo de arquivo

>No Linux é utilizado para se determinar qual é o tipo de arquivo informado como parâmetro com base no Magic Number (dois primeiros bytes).

> Ao contrário do Windows, as extensões de arquivo nada significam no Linux. O comando file faz três tipos de checagem para determinar qual é o tipo do arquivo:
>>* Teste de sistema de arquivos;
>>* Teste de Magic Number;
>>* Teste de Linguagem

>O primeiro teste de sistema de arquivos é feito para determinar se o arquivo é um arquivo comum, um diretório, um link, um dispositivo, um socket de conexão, etc. No Linux absolutamente tudo é um arquivo. O tipo de arquivo no sistema de arquivos determina se ele é um arquivo comum ou outro tipo especial.

> O segundo teste de Magic Number verifica os dois primeiros bytes do arquivo para determinar o seu tipo. Existe uma convenção na computação que determina que os dois primeiros bytes do arquivo devem conter um código que indica o seu tipo. Por exemplo, os scripts começam com o código “#!”, seguido do caminho completo do interpretador que irá interpretar e executar o script.

> O terceiro teste, uma vez que foi determinado que o arquivo é um programa, script ou código fonte, indica qual é a linguagem do programa.

##### $ ls

> Lista arquivos de diretorios

Exemplo:

```sh
ls -lh /var/
total 36K
drwxr-xr-x  2 root root  4,0K jul  7 18:30 backups
drwxr-xr-x 16 root root  4,0K jun 28 14:20 cache
drwxr-xr-x 51 root root  4,0K jul  5 19:15 lib
drwxrwsr-x  2 root staff 4,0K mar  2 10:55 local
lrwxrwxrwx  1 root root     9 jun 27 07:52 lock -> /run/lock
drwxr-xr-x 11 root root  4,0K jul  6 01:51 log
drwxrwsr-x  2 root mail  4,0K jun 27 07:52 mail
drwxr-xr-x  2 root root  4,0K jun 27 07:52 opt
lrwxrwxrwx  1 root root     4 jun 27 07:52 run -> /run
drwxr-xr-x  6 root root  4,0K jun 27 08:10 spool
drwxrwxrwt  6 root root  4,0K jul  8 00:00 tmp

```

Opções:
* -l 	lista com detalhes onde a primeira coluna especifica o tipo de arquivo(c=Caracter, d=diretorio, l=link )
* -d 	somente diretórios
* -h	Exibe o tamanho dos arquivos em Kb,Mb,Gb…
* -a 	arquivos ocultos

##### $ touch

> Criar arquivos 

Exemplos:
```sh
touch arquivo.txt 

# Cria 10 arquivos com o nome arquivoN.txt onde N é o intervalo entre {1..10}
touch arquivo{1..10}.txt

touch -a  filename    # altera somente o horário de acesso
touch -m  filename    # altera apenas o horário de modificação
```

##### $ mv

> Move ou renomeia arquivos conforme opções
>> * -v  (verboso) //mostra o que foi feito
>> * -i  (interativo) // pergunta antes de realizar algo
>> * -f  (força)       // força a execução do comando e sobrescreve os arquivos 

```sh
# Move o arquivo porem se no destino existe o arquivo o -i pergunta se deseja sobrescrever
mv -iv origem/filename1 destino/filename1 

```

##### $ cp 

> Copia arquivos entre diretórios com algumas opções:

```-s``` Cria link simbólico para o arquivo copiado
```sh
$ cp -s script.sh scriptx
```

```-b``` faz um backup(sources.list~) caso exista o arquivo no destino
```sh
$ cp -b sources.list /etc/apt/
```

```-p``` preserva os atributos/permissões do arquivo 
```sh
$ cp -p filenamex destino/filenamex
```

##### $ mkdir

> Cria diretorios confome exemplos abaixo:

```sh
$ mkdir -p dir1/dir2/dir3            # Cria diretorios recursivamente
$ mkdir -p -m 555  dir1/dir2/dir3    # Cria diretorios recursivamente com permissões no padrao chmod
```

##### $ rm

> Remove arquivos e diretorios

```sh
rm -rfv diretorio    # Remove arquivos -r recursivamente e -f forçado
```
##### $ rmdir

> Remove diretorios vazios

```sh
rmdir diretorio
```

##### $ find

> O find faz pesquisa por arquivos em uma hierarquia de diretórios. O que os parametros abaixo representa

```sh
$ find / -name  'filename'    # busca exatamente o arquivo com o nome entre aspas
$ find / -name  '*.Conf'      # qualquer arquivo com sufixo .Conf 
$ find / -iname '*.Conf'      # qualquer arquivo com sufixo .conf ou .Conf ignora case-sensitive
$ find / -name '*' -type l    # odos os arquivos do tipo link onde -type pode ser (d)diretorios,(l)link,(s)socket etc...
$ find /  -amin -10           # arquivos acessados a menos de 10 minutos 
$ find /  -ctime 3            # arquivos alterados exatamente a 3 horas
$ find /  -mmin -3            # arquivos modificados a menos de 3 minutos
```

* +n Mais de, n Exatamente, n Menos de
* atime (accessed), ctime (changed), mtime (modified)
* min(minutos), time(horas)

Tipos(-type)
- ```b``` especial de bloco (com buffer)
- ```c``` especial de caractere (sem buffer)
- ```d``` diretório
- ```p``` encadeamento com nome (FIFO)
- ```f``` arquivo regular
- ```l``` link simbólico; isso nunca é verdadeiro se a opção -L ou a opção -follow estiver em vigor, a menos que o link simbólico esteja  quebrado.  Se você deseja procurar links simbólicos quando -L estiver em vigor, use -xtype.
- ```s``` socket
- ```D``` door (Solaris)

Combinações -type d,l,s

##### $ tar

> Agrupa arquivos. Opções: 

- ```c``` criar
- ```x``` extrair
- ```f``` arquivo
- ```v``` de forma verbosa
- ```p``` preservando os atributos
- ```t``` o mesmo que --list

Exemplos:

```sh
tar cvpf arquivo.tar diretoriox/      # Cria um arquivo.tar com os dados do diretoriox
tar xvpf arquivo.tar -C /destinox     # Extrai o arquivo.tar no diretoriox
tar tvf arquivo.tar                   # Visualiza conteudos do arquivo.tar
```


##### $ gzip

Gera um arquivo compactado.gz conforme exemplos abaixo:

```sh
# -k preserva o arquivo original
$ gzip -k filename

# -c concatena arquivos de texto gerando um unico arquivo compactado 
$ gzip -c file1.txt file2.txt > file3.gz
```



#linux #lpi