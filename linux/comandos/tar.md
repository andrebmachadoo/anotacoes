# tar 

Para compactar arquivos no formato TAR.GZ usando use:
```sh 
tar -zcvf arquivos.tar.gz arquivos/ 
```
Para compactar arquivos no formato TAR.BZ2 usando use:
```sh 
    tar -jcvf arquivos.tar.bz2 arquivos/ 
```
Para descompactar arquivos no formato TAR.GZ, no diretório corrente:
```sh 
    tar -zxvf arquivos.tar.gz 
```
Para descompactar arquivos no formato TAR.BZ2, no diretório corrente:
```sh 
    tar -jxvf arquivos.tar.bz2 
```
Outros exemplos
```sh 
    tar -c pasta > arq.tar 
```

```sh 
    tar -cvf arq.tar arq1 arq2 
    tar -cvf /dev/fd1 /dir1/* 
    tar -cvMf /dev/fd1 /dir1 /dir2/subdir /dir3 /dir4 
    tar -c -v -f arq.tar *.ext 
    tar -cwf arq.tar pasta 
    tar -czvf /pasta/arq.tgz * 
    tar -czwf arq.tar.gz -C /dir1 arq1 -C /dir2 arq2 arq3 
    tar -rf arq.tar arq* 
    tar -tf arq.tar 
    tar -xv -f arq.tar 
    tar -xvMf /dev/fd0 
    tar -xf arq.tar pasta/arq1 
    tar -xzvf /pasta/subdir/arq.tar.gz 
    tar -xzwf arq.tgz 
    tar -xzvf arq.tar.gz -C /home/restaurado (descompacta os arquivos no diretorio especificado) 
```

