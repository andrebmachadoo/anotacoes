## Criando diretorios recursivamente 

```sh
$ mkdir -p /test/a/b/c    
```
> With above exemple the comand create directory test and your subdirectory 
>
> test>a>b>c


## Cria o diretorio e copia o arquivo 

> mkdir -p ../bkp/diretoriox/subdirx && cp diretoriox/subdirx/arquivoNoDiretoriox.txt $_

No comando acima:

O parametro -p do mkdir cria a estrutura de diretorios conforme path

&& = possibilita que seja execuado mais de um comando na linha 

cp diretoriox/sub...... = copia o arquivo 

$_ recupera o parametro do comando anterior


>Dessa forma o arquivoNoDiretoriox.txt será copiado para uma pasta no diretorio anterior ao atual  ../bkp/diretorio/subdirx


Fonte:
https://stackoverflow.com/questions/1529946/linux-copy-and-create-destination-dir-if-it-does-not-exist
