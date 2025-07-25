
# Chown
---
O comando `chown` permite alterar o nome do dono e/ou do grupo de um arquivo, diretório ou link

## Opções do comando 
* ***-c** : informa quais arquivos estão sendo alterados.
* **-h** : altera o link, não o arquivo apontado pelo link.
* **-v** : informa quais arquivos estão sendo processados (não necessariamente alterados).
* **-R** : altera, recursivamente, dono e/ou grupo de arquivos.
* **−−help** : exibe opções do comando.
- **−−version** : exibe informações sobre o aplicativo.

**Sintaxe básica**

```sh
chown user:group file_directory_link
```

> Nos exemplos abaixo consideramos usuário(**aluno**) e o grupo (**informática**) e o arquivo/diretório/link **teste**

```sh
chown -Rc aluno:informatica teste

chown -Rc aluno teste

chown -Rc :informatica teste

chown -h aluno:informatica teste
```
