# Kill e sinais de gerenciamento de processos

## Listando processos com pstree

```sh
pstree -np
pstree -s 3973
pgrep -l chr
```
- **n** : ordena a saída pelos números dos **PIDs** dos processos.
- **p** : mostra os **PIDs** dos processos.
- **s** : mostra os processos -pai do processo especificado.

## Sinais

>O sinal faz parte de um mecanismo de comunicação do Linux que é usado para notificar um **processo** da ocorrência de um evento.
>Ou seja, os Processos do Linux ficam monitorando ou escutando sinais que podem ser enviados pelo kernel do sistema ou pelos usuários através do terminal.


```sh
kill -l

1) SIGHUP	 2) SIGINT	 3) SIGQUIT	 4) SIGILL	 5) SIGTRAP
 6) SIGABRT	 7) SIGBUS	 8) SIGFPE	 9) SIGKILL	10) SIGUSR1
11) SIGSEGV	12) SIGUSR2	13) SIGPIPE	14) SIGALRM	15) SIGTERM
16) SIGSTKFLT	17) SIGCHLD	18) SIGCONT	19) SIGSTOP	20) SIGTSTP
21) SIGTTIN	22) SIGTTOU	23) SIGURG	24) SIGXCPU	25) SIGXFSZ
26) SIGVTALRM	27) SIGPROF	28) SIGWINCH	29) SIGIO	30) SIGPWR
31) SIGSYS	34) SIGRTMIN	35) SIGRTMIN+1	36) SIGRTMIN+2	37) SIGRTMIN+3
38) SIGRTMIN+4	39) SIGRTMIN+5	40) SIGRTMIN+6	41) SIGRTMIN+7	42) SIGRTMIN+8
43) SIGRTMIN+9	44) SIGRTMIN+1045) SIGRTMIN+1146) SIGRTMIN+1247) SIGRTMIN+13
48) SIGRTMIN+1449) SIGRTMIN+1550) SIGRTMAX-1451) SIGRTMAX-1352) SIGRTMAX-12
53) SIGRTMAX-1154) SIGRTMAX-1055) SIGRTMAX-9	56) SIGRTMAX-8	57) SIGRTMAX-7
58) SIGRTMAX-6	59) SIGRTMAX-5	60) SIGRTMAX-4	61) SIGRTMAX-3	62) SIGRTMAX-2
63) SIGRTMAX-1	64) SIGRTMAX
```

## Sintaxe básica

```sh
kill [sinal ou opção] pid
```

## Exemplo de uso do kill

```sh 
sleep 180 &   #cria um processo(sleep) em background
ps 1234 ou pstree 1234  # verificando o processo 
kill 1234 #finaliza o processo 
kill -9 1234 #finaliza o processo com SIGKILL
```


## Problemas com o SIGKILL -9

> Finalizar processos com o uso do SIGKILL -9 pode ser um problema porque interrompe o processo de forma radical e não finaliza os processos dependentes. Isso pode deixar Processos filhos zumbis ou órfãos, ocasionar perda de dados e gerar instabilidades.


## Finalizando os processos corretamente

> Para encerrar um processo de forma segura e respeitosa no Linux, você pode executar o seguinte roteiro de comandos de kill:

- SIGTERM Tente enviar um SIGTERM usando kill -15 ou kill padrão **(kill PID)**.
- SIGINT Após alguns segundos, se o processo não estiver finalizado, envie um SIGINT (kill -2 PID).
- SIGHUP Se persistir o processo aberto, envie um SIGHUP (kill -1 PID).



---
https://www.webmundi.com/sistema-operacional/curso-de-linux-basico/como-utilizar-o-kill-e-sinais-no-gerenciamento-de-processos-linux/