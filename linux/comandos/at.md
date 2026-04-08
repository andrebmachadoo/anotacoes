# Comando at
---

>O comando `at` lê arquivos da entrada padrao ou de um arquivo especifico para serem executados posteriormente:


### Modo 1:  

1. Na linha de comando digite o comando at seguido da hora ou data/hora;
2. Pressione enter para abrir o prompt que deverá inserir as linhas de comandos desejados;
3. Pressione **Control+D** para colocar o comando em background;

Exemplo:
```bash
   $ at 9:45
   $ at> mkdir teste
   $ at> echo "Teste do comando at" > teste/teste.txt
   $ at> cp ./teste/teste.txt ~/
   $ at> <Control+D>
   warning: commands will be executed using /bin/sh
   job 1 at Wed Oct 16 09:45:00 2019   
```

### Modo 2:

1. ****:  
   ```bash
   $ at -f file_comands.txt 9:45
   ```  

### Alternativas de data e hora 

> O exemplo a seguir considera que o comando at foi executado no dia 18 de outubro de 2019 às 18:00 horas.

|Expressão|	Equivale a|
|-|-|
|`$ at noon 				`|18 de outubro de 2019|
|`$ at midnight 			`|00 19 de outubro de 2019|
|`$ at teatime 			    `|00 18 de outubro de 2019|
|`$ at tomorrow 			`|00 19 de outubro de 2019|
|`$ at noon tomorrow 		`|00 19 de outubro de 2019|
|`$ at next week 			`|00 25 de outubro de 2019|
|`$ at next monday 		    `|00 24 de outubro de 2019|
|`$ at fri 				    `|21 de outubro de 2019|
|`$ at NOV 				    `|18 de novembro de 2019|
|`$ at 9:00 AM 			    `|00 19 de outubro de 2019|
|`$ at 2:30 PM 			    `|30 18 de outubro de 2019|
|`$ at 1430 				`|18 de outubro de 2019|
|`$ at 2:30 PM tomorrow 	`|30 19 de outubro de 2019|
|`$ at 2:30 PM next month 	`|30 18 de novembro de 2019|
|`$ at 2:30 PM Mon 		    `|30 21 de outubro de 2019|
|`$ at 2:30 PM 10/21 		`|30 21 de outubro de 2019|
|`$ at 2:30 PM Oct 21 		`|30 21 de outubro de 2019|
|`$ at 2:30 PM 10/21/2014 	`|30 21 de outubro de 2019|
|`$ at 2:30 PM 21.10.14 	`|30 21 de outubro de 2019|
|`$ at now + 30 minutes 	`|30 18 de outubro de 2019|
|`$ at now + 1 hour 		`|00 18 de outubro de 2019|
|`$ at now + 2 days 		`|00 20 de outubro de 2019|
|`$ at 4 PM + 2 days 		`|00 20 de outubro de 2019|
|`$ at now + 3 weeks 		`|00 8 de novembro de 2019|
|`$ at now + 4 months 		`|00 18 de fevereiro de 2020|
|`$ at now + 5 years 		`|00 18 outubro 2024|


>**Obs**: 
> - O comando at não é recomendado para tarefas recorrentes ou que necessitam de privilégios de superusuário, acesso a variáveis de ambiente, acesso a arquivos temporários, ou acesso a arquivos de log. Para tarefas simples e pontuais, o comando `cron` pode ser mais adequado.  
> - Os comandos adicionados serão executados no /bin/sh  
### Listar tarefas agendadas

```bash
$ atq
```
### Remover tarefas agendadas

```bash
$ atrm <job_number>
```
### Referências
- [Comando at](https://www.computerhope.com/unix/uat.htm)
- [Alternativas de data e hora](https://www.gnu.org/software/bash/manual/bash.html#Shell-Builtin-Commands)
- [linuxforce](https://linuxforce.com.br/comandos-linux/comandos-linux-comando-at/?gad_source=1&gad_campaignid=23710759196&gbraid=0AAAAADmPUt59VUm6K0xeKQlISgONkQfIv&gclid=CjwKCAjw-dfOBhAjEiwAq0RwI904l_fcwhAMoR3KliMbUpyjM5EnjMUeKhpzbfApbuFb7V7nFBaTBhoCKncQAvD_BwE)










