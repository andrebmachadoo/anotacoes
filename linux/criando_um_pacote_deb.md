## Criando um instalador .deb para distros linux baseadas em Debian
---

*Passo 1* 
- Criando a estrutura do instalador na pasta /tmp ou em outra pasta que preferir

```sh
$ mkdir /tmp/packagename
```

*Passo 2* 
- Diretório obrigatorio que conterá os arquivos de controle do pacote.

```sh
$ mkdir /tmp/packagename/DEBIAN
```

*Passo 3*
- Arquivo "control" que contem dados importantes e e alguns obrigatorios para gerar o pacote.

```txt
Version: (Obrigatório) - versão do pacote o qual você esta criando.
Section: (Recomendado) - Area de aplicação em que o pacote foi classificado.
Architecture: (Obrigatório) - Lista arquitetura(s) para a qual, o pacote é destinado. 

Exemplo de arquiteturas:
i386 ia64 alpha amd64 armeb arm hppa m32r m68k mips mipsel powerpc ppc64 s390 s390x sh3 sh3eb sh4 sh4eb sparc...

Depends: O pacote não será configurado a menos que todos os pacotes listados neste campo sejam configurados corretamente.

Installed-Size: Espaço em disco requerido representado em kilobytes como número decimal simples.

Maintainer: (Obrigatório) - Email do mantenedor do pacote.

Description: (Obrigatório) - Descrição do pacote.

```

*Exemplo:*
```
Package: myappname
Priority: optional
Version: 0.1
Architecture: i386
Maintainer: your name
Depends:
Description: Descricao/Informações importante sobre a aplicação...
```

```sh
$ vi /tmp/packagename/DEBIAN/control

Package: packagename
Priority: optional
Version: 0.1
Architecture: i386
Maintainer: Nome do mantenedor
Depends:
Description: Descrição do pacote
```

*Passo 4* 
- Criar dentro da pasta onde esta gerando o instalador a estrutura de diretorios semelhante ao aplicativo depois de instalado. Para isso entre no diretorio onde esta gerando o instalador e faça como o exemplo abaixo:


```sh
$ mkdir -p usr/bin

# Copiar seu app ou script para o arquivo onde esta sendo gerado o instaldor
cp /home/user/devel/app/fileapp_ou_script ./usr/bin/fileapp_ou_script

# Depois de seguir os passos anteriores esse comando ira gerar o .deb
$ dpkg-deb -b /tmp/packagename /tmp
$ dpkg-deb -b <caminho absoluto do diretório base> <local onde o pacote deve ser gerado>

# instalando
$ dpkg -i /tmp/<nome do pacote>

#Extrair o conteúdo de um pacote deb para dentro de um diretório:
$ dpkg-deb -x <nome_do_Pacote.deb> /tmp/pacote

# Extrair o arquivo de controle de um pacote deb:
$ dpkg-deb -e <nome_do_pacote.deb> /tmp/pacote/DEBIAN


```

