# ar
---

> O comando ar cria um arquivo(repositório) para armazenar dados de outros arquivos semelhante um merge de arquivos de texto, porem com um padrão especifico que permite listar, deletar e extrair os arquivos conforme comandos a seguir

>Considerando dois arquivos arquivo1.txt arquivo2.txt com seus respectivos conteúdos

arquivo1.txt
```text
conteudo do arquivo1
```
arquivo2.txt
```text
conteudo do arquivo2
```

>Adicionando arquivo1.txt ao repositorio:
```bash
$ ar r arquivo_merge arquivo1.txt
$ cat arquivo_merge
```
>output
```
!<arch>
arquivo1.txt/   0           0     0     644     21        `
conteudo do arquivo1
```

>Adicionando o arquivo2.txt
```bash
$ ar r arquivo_merge arquivo2.txt
$ cat arquivo_merge
```
>output
```
!<arch>
arquivo1.txt/   0           0     0     644     21        `
conteudo do arquivo1

arquivo2.txt/   0           0     0     644     21        `
conteudo do arquivo2
```

>Listando arquivos
```bash
# Exibe nome dos arquivos 
$ ar t arquivo_merge 

#lista arquivos e suas propriedades modo verbose
$ ar tv arquivo_merge 

#Exibe conteudo dos arquivos
$ ar p arquivo_merge 

#extrai o arquivo1.txt do repositorio mergeado
$ ar xv arquivo_merge arquivo1.txt

#extrai todos os arquivos unidos no repositorio
$ ar xv arquivo_merge

#exclui arquivo do repositorio mergeado
$ ar d arquivo_merge arquivo1.txt

```