# Docker pos install

```sh

#Cria um grupo do docker 
sudo groupadd docker

#Adciona o usuario ao grupo do docker para nao precisar executar sudo antes dos comandos.
sudo usermod -aG docker $USER

# Inicializar o docker no ubuntu
sudo service docker start

#Testa se a instalação esta ok 
docker run hello-world

#Verifica o status do serviço 
sudo service docker status


```