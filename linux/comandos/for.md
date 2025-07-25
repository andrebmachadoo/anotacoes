## Comando for

>O comando for no Linux permite que laços (loops) sejam feitos para que um ou mais comandos sejam executados até que uma determinada variável percorra todos os valores de uma dada lista.

```sh
$ for numero in um dois três quatro cinco
do
echo "Contando: $numero"
done 

# Saida
# Contando: um
# Contando: dois
# Contando: três
# Contando: quatro
# Contando: cinco
```

> Percorrendo uma lista de arquivos e executar comandos para cada arquivo

```sh
#Gerando uma lista 
ls -1 > lista_arquivos.txt

# `cat` lendo a lista, `cp` copiando/duplicando com nome `.backup` `mv` movendo o arquivo para /tmp/backup
$ for i in $(cat lista_arquivos.txt); do cp $i $i.backup; mv $i.backup /tmp/backup; done;
```

>Nesta linha abaixo, o resultado do comando ls -1 é colocado na variável $i; Depois cada linha da variável $i é testada para saber se é um arquivo; se for verdadeiro, será exibida uma frase e, se for falso, outra frase.

```sh 
$ for i in `ls -1`; do if test -f $i;  then echo “$i é um arquivo “; else echo “$i não é um arquivo”; fi ; done
```


### for + ping + grep = ipscan

> Combinando os comandos for+ping pode percorrer uma faixa de numeros ip e executar o comando ping, e por fim utilize o comando grep para exibir/filtrando algum valor especifico.


```sh
    for n in {1..5};do ping -n 1 192.168.3.$n; done

	for n in {1..5};do ping -n 1 192.168.25.$n |grep filtro_do_grep; done
```



