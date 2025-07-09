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

## Dockerignore

> Ao utilizar a opção COPY seguido de * é copiado tudo para dentro do container exceto o que esta no *.dockerignore*. Ou seja todos os arquivos que estao na lista do .dockerignore serão ignorados pelo comando COPY. Semelhante ao .gitignore

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

# Informando o dockerfile no paramentro -f
$ docker build -f Dockerfile_dev -t php_myqli:7.2-apache .

$ curl http://localhost
```




## Otimizando a imagem*

> Utilizando o history para ver os dados das camadas percorridas para gerar a imagem
```sh 
$ docker history imageName
```

> No alpine utilizamos o parametro **--no-cache para não armazenar dados da instalação**
```sh
FROM alpine:3.16

RUN	apk update && \
	apk --no-cache add nmap && \ 
	apk --no-cache add htop && \
	apk --no-cache add iptraf-ng && 
```

> No ubunto podemos informar para nao instalar pacotes de dependencias e limpar as libs no final

```sh
FROM ubuntu:20.04
RUN apt-get update && \
    apt-get install -y nmap &&\
    apt-get install -y htop &&\
    apt-get install -y iptraf &&\
    --no-install-recommends && \
    rm -rfv /var/lib/apt/lists/*
```

## Utilizando recurso de linter

> Assim como nas linguagens de programação podemos usar um linter para fazer criticas ao nosso dockerfile apontando prossiveis problemas
> Ex:
```sh

$ docker run -i --rm hadolint/hadolint < Dockerfile

```

## Executando um script

```sh
FROM alpine:3.16

RUN	apk update && \
	apk --no-cache add nmap && \ 
	apk --no-cache add htop && \
	apk --no-cache add iptraf-ng && \

COPY --chown=root:root ./script /usr/bin/script.sh 
RUN chmod +x /usr/bin/script.sh

```

## Pasando a var de ambiente para o script.sh

*script.sh*
```sh
#!/bin/bash
echo "Hello world ${VAR_AMBIENTE}!!!"
```

```sh
$ docker run -it --rm -e VAR_AMBIENTE="Valor Var ambiente" minhaImagem script.sh

```

> OBS: Tambem é possivel setar uma variavel no arquivo Dockerfile para garantir um valor caso nao seja setada do comando. Para isso basta adcionar a linha abaixo no Dockerfile
>> ENV VAR_AMBIENTE="Valor padrão da var de ambiente"


## Executando Comandos na imagen

> Para executar comandos quando subir um container basta adcionar a linha abaixo 
>> CMD /usr/bin/script.sh

> Podemos utilizar também o ENTRYPOINT 
>> ENTRYPOINT /usr/bin/script.sh
>> A diferença entre o CMD e ENTRYPOINT é que o ENTRYPOINT nao permit executar outro comando quando setado na cli

Ex: Com o ENTRYPOINT no Dockerfile o comando "ls" no final do comando abaixo será ignorado e executará o ENTRYPOINT

```sh
    $ docker run -it --rm -e VAR_AMBIENTE="Valor Var ambiente" minhaImagem ls
```

# Inserindo LABELs nas imagens

> **Para setar algumas informações no contaniner podemos utilizar o LABEL**
>> **Ex: LABEL maintainer="Fulano de tals"**

