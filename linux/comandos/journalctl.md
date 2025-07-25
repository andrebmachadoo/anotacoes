# journalctl
---

> **journalctl** é a ferramenta util para monitoramento de logs do systemd. O comando sem parâmetros lista todos os logs gerados e na primeira linha exibe a data de inicio dos logs, mas existem vários parâmetros uteis para relatorios:

```sh
journalctl --since "2017-07-27 01:00:00" --until "2017-07-28 15:00:00"

# --since --> inicio dos logs(somente hora considera data atual)
# --until --> limite final dos logs

#informando um ou mais serviços para monitorar
journalctl -u nginx.service -u sshd.service

#Em tempo real, semelhante ao comando tail
journalctl -f
journalctl -u nginx.service -f

#usar com parâmetros de PID, UID, GID
journalctl _PID=5000  
journalctl _UID=33

#logs do Kernel
journaulctl -k
```

## Formatos de saída
```sh
#formato json
journalctl -u nginx -o json
journalctl -u nginx -o json-pretty

# mais detalhados
journalctl -u nginx -o verbose
#formato mais curto:
journalctl -u nginx -o cat
# Formato padrão de LOGs
journalctl -u nginx -o short

#logs do boot corrente  
journalctl -b
```
