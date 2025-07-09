# Comandos importantes
---

>Lista proessos(containers) em execução  
`docker ps`                     

>Lista proessos(containers) que foram executado  
`docker ps -a`  

>Lista imagens em execução ou que ja foram executadas (-a)  
`docker images ` ou `docker image ls ` ou `docker image ls -a`  

>Lista containers em execução ou que ja foram executadas (-a)  
`docker container ls ` ou `docker image ls -a`  

>Exibe logs de containers em execução ou que foram executado  
`docker logs container_name_ou_id`      

>Sobe um container em modo terminao(-it) mas que finaliza quando sair(Ctrl+D)  
`docker run -it  container_ou_id`  

> Sobe(-d daemon) um container com um nome "--name meu_container" de uma imagem(alpine) que remove(-rm) quando finalizado  
`docker run -d --name meu_container --rm alpine tail -f /dev/null`
`docker run -itd --name busybox busybox`

>Acessa a linha de comando(-it "interative terminal) de algum container em execução   
`docker exec -it container_name_ou_id /bin/bash_ou_sh`

>Acessa o container iniciado com terminal interativo "-itd"  
`docker attach busybox`

>Acessa a linha de comando(-it "interative terminal) de algum container em execução    
`docker exec -it container_name_ou_id /bin/bash_ou_sh`  

> executa um comando sem entrar no container  
`docker exec meu_container cat /etc/passwd`  

>Lista imagens filtrando por imagens sem tag_name "<none>" ou que nao estao em uso dangling(pendurada)   
`docker images -f "dangling=true" -a`  

>Exibe um json com os dados do container   
`docker container inspect contaniner_name_ou_id`  

>Dica: Instale o pacote (apt install jq) e utilize com pipe ao final do comando para filtrar dados  
`docker container inspect contaniner_name_ou_id | jq`  

>Filtra o resultado que é um array(jq '.[]') e os dados de redo do container (jq '.[] | .NetworkSettings')  
`docker container inspect 105 | jq '.[] | .NetworkSettings'`  

>Retornando o ip do container  
`docker container inspect 105 | jq '.[] | .NetworkSettings.Networks.bridge.IPAddress'`  

> Busca imagens no hub.docker.com pelo nome  
`docker search image_name`

>Baixa a imagem  
`docker pull  image_name`

>Exibe as alterações realizadas no container  
`docker diff container_name_ou_id`

>Semelhante ao commit do git  
`docker commit -a NomeAuthor -m Mensagem container_name_ou_id`

>Carrega uma imagem local para um registro remoto   
`docker push container_name_ou_id`

>Remove uma image
`docker rm container_name_ou_id`

>Força a remoçao mesmo que esteja rodando  
`docker rm -f container_name_ou_id   `

>Remove imagem   
`docker rmi  image_name_ou_id  `

>Fazendo backup do banco no mysql
`docker exec container_name_ou_id  /usr/bin/mysqldump -u username --password=password database_name > backup.sql`

>Restaurando backup do mysql
`cat backup.sql | docker exec -i container_name_ou_id /usr/bin/mysql -u username --password=password database_name`