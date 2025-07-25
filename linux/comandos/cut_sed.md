# Usando o comando cut e sed 

#### Recortando parte de uma string delimitada por virgula com o CUT

```sh
	cut -d ',' -f 1,2 <<< 'string1,string2,string3'
```

#### Substituindo um caracter de uma string com SED
```sh
	sed 's/,/ /g' <<< 'string1,string2'
```
#### Usando o CUT e SED juntos para recortar dados e substituir caracteres
```sh
	dados='string1,string2,string3'
	cut -d ',' -f 1,2 <<< $dados | sed 's/,/ /g'
```

