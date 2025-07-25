# jq
---
>O comando jq é indispensável para manipulação de dados no formato JSON, como indentar, ordenar, compactar e mostrar as chaves JSON. Ele não vem instalado como padrão na maioria das distribuições.

```
$ cat nomes.json   
{"primeiro_nome":"Sarah","sobrenome":"Silva"}  
{"primeiro_nome":"Ana","sobrenome":"Ferreira"}  
{"primeiro_nome":"Emilio","sobrenome":"Moura"}  
{"primeiro_nome":"Clara","sobrenome":"Martins"}  
{"primeiro_nome":"José","sobrenome":"Pereira"}
```

```bash
# Exibe o conteudo em modo pretty json
cat nomes.json | jq

#ordena a saida pelo campo primeiro_nome
cat nomes.json | jq -s -c 'sort_by(.primeiro_nome) | .[]'
# -s carrega os valores em um array,
# -c compacta o resultado, ao invés de expandi-lo.

#verificar o tamanho de um determinado item:
jq '.primeiro_nome |length' nomes.json

#mostrar somente as chaves únicas de um JSON:
jq -c 'keys' nomes.json  | sort | uniq

#filtrar somente uma chave
cat nomes.json | jq '.sobrenome'

#Criar um array em jq.
echo '[]' | jq '. += ["Apple", "Banana", "Cherry"]'

#Gera o array e recupera o segundo vetor no ultimo pipe
echo '[]' | jq '. += ["Apple", "Banana", "Cherry"]'|jq '.[1]'

# Altera o segundo vetor do array
echo '["Apple", "Banana", "Cherry"]' | jq '.[1]="Blueberry"'

#Acessa o vetor 0 do array e retorna o atributo Id do json  
echo '[{"Id": "19b24489a14bda","Networks": {"bridge": {"Gateway": "172.17.0.1","IPAddress": "172.17.0.2","MacAddress": "02:42:ac:11:00:02"}}}]' |jq '.[] | .Id'

#Acessa o vetor 0 do array e retorna o sub atributo IPAddress do json  
echo '[{"Id": "19b24489a14bda","Networks": {"bridge": {"Gateway": "172.17.0.1","IPAddress": "172.17.0.2","MacAddress": "02:42:ac:11:00:02"}}}]' |jq '.[] | .Networks.bridge.IPAddress'

# Filtrando o array e retornando todas as palavras iniciadas com B  
echo '["Apple", "Banana", "Blueberry", "Cherry"]' | jq '.[] | select(startswith("B"))'

# mapeamento de um array para transformar todos os seus elementos em letras maiúsculas  
echo '["Apple", "Banana", "Blueberry", "Cherry"]' | jq '.[] | ascii_upcase'
```



  
---
### Uma das fontes :https://ioflood.com/blog/jq-array/