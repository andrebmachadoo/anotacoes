# Comando cat
---

Ler o arquivo e atribui resultado filtrado por grep a outro arquivo

```bash
    cat /path/filename.log |grep -n -B 1 -A 2 'conteudo a filtrar' >> /path/destino.log
```

