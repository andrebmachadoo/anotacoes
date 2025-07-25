## Comando tail 
---

> O comando tail Linux exibe a última parte – por padrão, são 10 linhas que aparecem ao final – de um ou mais arquivos ou dados de saída no prompt Linux. Também pode ser usado para monitorar as alterações do arquivo em tempo real.

```sh
#Exibindo mais do que as e10 linhas padrao

$ tail -n 50 /path/log.txt
$ tail -n 20 arquivoexemplo1.txt arquivoexemplo2.txt
```

```sh
#Exibir os últimos bytes ou kbytes do arquivo

$ tail -c 500 arquivoexemplo.txt
$ tail -c 2k filename.txt
```

```sh
#Monitorando em alterações de um arquivo 

$ tail -f /path/log.txt

# Reabre o arquivo se recriado 
$ tail -F arquivoexemplo.txt
```

### tail e grep combinados 

```bash
#Monitorando arquivo e recuperando um conteudox e atribuindo o resultado ao final de outro arquivo

$ tail -f /path/log.txt |grep -n -B 1 -A 2 'CONTEUDOX' >> /path/resultado.txt
```


## Exemplos de uso pratico

> Monitorar o arquivo de registro de acesso do apache e exibir apenas as linhas que contêm o endereço IP, você usaria
```bash
$ tail -f /var/log/apache2/access.log | grep 000.000.00.00
```
>Exibir os dez principais processos em execução classificados por uso de CPU:

```bash
$ ps aux | sort -nk +3 | tail -5
```

> Lendo as linhas de 2 a 6 do arquivoexemplo.txt. A princípio, o comando head recuperará as primeiras 6 linhas, omitindo as 5 últimas linhas para o valor negativo, enquanto o comando tail recuperará as últimas 5 linhas da saída do comando head. Veja:

```bash
$ head -n -5 arquivoexemplo.txt | tail -n 5
```
