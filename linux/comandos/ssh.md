# Dicas SSH
---

### Gerando chaves RSA

```sh 
	ssh-keygen -t rsa -C 'user@email.com'
	ssh-keygen -t rsa -b 4096 -C 'user@email.com'
```

### Ativando gerenciador de chaves ssh

```sh 
	eval $(ssh-agent)
	eval $(ssh-agent -s)
```

### Copiando chave para servidor remoto

```sh 
	ssh-copy-id -i ./id_key.pub user@host_ou_ip
```

### Acessando servidor e executando comandos

```sh 
	ssh user@host_ou_ip -p22 -o PasswordAuthentication=no 'mkdir /home/user && chmod 600 ~/.ssh/id_key.pub'
```

### Criar uma chave ed25519, executar:

```sh 
	ssh-keygen -t ed25519 -C
```
  
### Copy ssh keys for other server

```sh
	ssh-copy-id -i /home/username/.ssh/filename.pub user@server_origin_keys
```

> Obs: The -i parameter is because the keys be created with other name. So when will be access is necessary set -i to access server that copy keys


```sh
	ssh -i /home/username/.ssh/filename.pub user@server_dest
```

> After  sshd_config file don't restart the daemon because if has error we can undo configs

