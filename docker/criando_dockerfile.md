# Dockerfile
--- 

> Explicando os parametros do arquivo(Dockerfile) que gera imagem no docker 

|**FROM** debian                                                                                |Qual imagem será utilizada para montar uma imagem|
|:-|:-|
|**ADD** opa.txt /diretorio/                                                                    |Adciona um arquivo para dentro de um diretorio no container|
|**COPY** opa.txt /diretorio/                                                                   |Parecido com o ADD porem so copia arquivos e diretorios|
|**CMD** ["sh","-c","echo","$HOME"]                                                             |Comando ou parametro do entry point ou para o principal processo do container|
|**LABEL** Description =" bla bla bla"                                                          |Usado para inserir metadados ....|
|**ENTRYPOINT**["/usr/bin/apache2ctl","-D","FOREGROUND"]                                        |Entrypoint serve para determinar que um processo seja o principal processo do container,sendo assim se o processo cair o container deixa de existir|
|**ENV**                                                                                        |Seta variaveis de ambiente para dentro do container|
|**EXPOSE** 8080                                                                                |Expoe a porta do container|
|**RUN** apt-get update && apt-get install pacote && apt-get install pacote2 && apt-get clean   |Executa comandos ai criar a imagem como por exemplo instalar pacotes |
|**USER** nome_do_usuario                                                                       |Indica qual sera o usuario default da imagem|
|**WORKDIR** diretorio                                                                          |Diretorio de trabalho do container Diretório que sera acessado primeiro quando entrar no container |
|**VOLUME** /diretorio                                                                          |Diretorio compartilhando entre container e host|
|**MAINTAINER** nome email@x.com                                                                |Quem é que escreveu o dockerfile |
|                                                                                               |                                 |

## Sobre o RUN

> Evite inserir varios RUN no dockerfile, porque dessa forma os comandos sao executados em camadas diferentes e uma camanda nao sabe o que foi feito na camada anterior

> Ao final da criação da imagem provavelmente foram executados varias instalações de pacotes com `apt-get install pacote` por exemplo. Por isso é importante executar o `apt-get clean` para apagar lixos da instalação

**Forma errada**
```sh
//Dockfile
FROM ubuntu:16.10
RUN apt-get -y update
RUN apt-get -y install net-tools # Essa camada nao detecta o update
RUN apt-get -y install iputils-ping # Essa camada nao detecta as alterações anteriores
```
**Forma certa**

```sh
//Dockfile
FROM ubuntu:16.10
RUN apt-get -y update && \
    apt-get -y install net-tools && \
    apt-get -y install iputils-ping &&\
    apt-get clean
```

## Criando o Dockerfile

**Exemplo 1**

```sh
# Arquivo Dockerfile
FROM nginx
RUN /bin/echo "Hello Dockerfile"
```

**Exemplo 2** 

> O arquivo Dockerfile abaixo esta alterando a imagen do nginx e criando um index.html para o servidor

```yml
FROM nginx
RUN echo '<h1>Hello World !</h1>' > /usr/share/nginx/html/index.html
```

> Os comandos abaixo gera a imagem, lista, e sobe um container utilizando a imagem

```sh
$ docker image build -t minha_image1 ./
$ docker image ls
$ docker container run -p 80:80 minha_image1 
$ http://localhost
```

**Exemplo 3**