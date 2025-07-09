# Docker pos install
--- 

### Adicionando usuario ao grupo docker
1. Criando  o grupo docker caso nao exista

```$ sudo groupadd docker```

2. Adicionando usuario ao grupo docker

```$ sudo usermod -aG docker $USER```

3. Usando o "newgrp" para nao precisar relogar/reiniciar

```newgrp docker```

4. Testando se o docker pode ser executado fora do usuario root

```$ docker run hello-world```

5. Se nao funcionar tente reiniciar
