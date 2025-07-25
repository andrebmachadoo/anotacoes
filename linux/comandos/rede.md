## Comandos para manutenção de rede
---

### ifconfig

***ifconfig*** - Exibe configurações das interfacese de rede 


### ip
***ip a*** - Exibe interfaces de rede 
***ip -4 a*** - Exibe interfaces ipv4
***ip -6 a*** - Exibe interfaces ipv6
***ip -c -h a*** - Exibe interfaces com detalhes coloridos 

***ip a show wlp1s0*** - Exibe detalhes da interface informada
***ip -c link ls up*** - Apenas interfaces ativas

### Monitorar/Listar portas abertas 

```
$	sudo netstat -putona
$	sudo ss		-tulpn
```
-t – ativa a listagem de portas TCP.
-u – permite a listagem de portas UDP.
-l – imprime apenas soquetes de escuta.
-n – mostra o número da porta.
-p – mostra o nome do processo/programa.

***Para monitorar em tempo real pode usar os comandos acima precedido do comando watch***

```
$	sudo netstat	-putona
$	sudo ss		-tulpn
```


