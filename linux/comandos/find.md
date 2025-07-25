# Comandos importantes
---

## **find**

Busca uma string(texto) dentro de arquivos onde * significa todos os arquivos
```sh
     find * -type f -exec grep -l FindThisText {} \;
```

Busca pelo arquivo informado em letras maiusculas ou minusculas  e executa o comando md5sum do retorno do find

```sh
    find -iname "filename.txt" -exec md5sum {} \;
```

Encontre os arquivos escondidos no seu diretório pessoal (home):

```sh
    find ~ -type f -name ".*"
```

Para encontrar arquivos do tipo socket:

```sh
    find . -type s
```

Para ver a relação de diretórios:

```sh
    find . -type d
```

Busca os 7 maiores arquivos no diretório /usr/bin, incluindo seus subdiretórios

```sh
    find /usr/bin/ -type f -exec ls -s {} \; | sort -n -r | head -7
```


Busca arquivos vazios com o parâmetro -empty (vazio):

```sh
    find ~ -empty
```

Somente diretório atual evitando a recursividade:

```sh
    find . -maxdepth 1 -empty
```


Encontre os arquivos escondidos no seu diretório pessoal (home):

```sh

    find ~ -type f -name ".*"

```


Quantidade de arquivos dentro de um diretório no Linux

```sh

	find DIR_NAME -type f | wc -l

	find . -maxdepth 1 -type f | wc -l 

```

Obter a lista de subdiretórios do diretório corrente
```sh
	find . -type d
```
 
 Obter em txt a lista de subdiretórios do diretório corrente
	
 ```sh
	find . -type d > lista.txt
```

Se desejar obter a lista, excluindo algum padrão de nome de subdiretório

 ```sh
	find . -type d ! -name "~DIRETORIO_EXCLUIR" > lista.txt
```

Copiar somente uma estrutura de diretórios para dentro de uma pasta, sem copiar os arquivos

```sh
    find -type d -links 2 -exec mkdir -p "/path/to/backup/{}" \;
```


Excluir os arquivos mais antigos.


```sh
    find /path/to/files* -mtime +X -exec rm {} \;

```

