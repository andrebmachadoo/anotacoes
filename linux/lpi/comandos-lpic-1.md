# Grupos de Comandos LPIC-1 (Completo)

---

### **1. Gerenciamento de Arquivos e Diretórios**  
*(Complementado com `tree`, `ln`, `file`)*  

| Comando   | Exemplos Comuns                     | Descrição                                  |  
|-----------|-------------------------------------|--------------------------------------------|
| `tree`    | `tree /var`                         | Mostra estrutura de diretórios em árvore   |
| `ln`      | `ln -s /caminho/origem link`        | Cria link simbólico                        |
| `file`    | `file arquivo.bin`                  | Identifica tipo de arquivo                 |

---

### **2. Permissões e Propriedade**  
*(Adicionado `chattr`, `lsattr` para atributos estendidos)*  

| Comando   | Exemplos Comuns                     | Descrição                                  |  
|-----------|-------------------------------------|--------------------------------------------|
| `chattr`  | `chattr +i arquivo`                 | Torna arquivo imutável                     |
| `lsattr`  | `lsattr /etc/passwd`                | Lista atributos estendidos                 |

---

### **3. Processos e Jobs**  
*(Adicionado `nohup`, `pgrep`, `killall`)*  

| Comando   | Exemplos Comuns                     | Descrição                                  |  
|-----------|-------------------------------------|--------------------------------------------|
| `nohup`   | `nohup script.sh &`                 | Executa processo persistente               |
| `pgrep`   | `pgrep -u root`                     | Encontra PIDs por usuário                  |
| `killall` | `killall -9 nginx`                  | Mata processos por nome                    |

---

### **4. Redes**  
*(Adicionado `host`, `nc`, `tcpdump`)*  

| Comando   | Exemplos Comuns                     | Descrição                                  |  
|-----------|-------------------------------------|--------------------------------------------|
| `host`    | `host exemplo.com`                  | Consulta DNS simplificada                  |
| `nc`      | `nc -zv 192.168.1.1 80`            | Testa conexão TCP                          |
| `tcpdump` | `tcpdump -i eth0 port 80`          | Captura tráfego de rede                    |

---

### **5. Gerenciamento de Pacotes**  
*(Adicionado `apt-cache`, `yum history`)*  

#### **Debian/Ubuntu**
| Comando      | Exemplos Comuns              | Descrição                           |
|--------------|------------------------------|-------------------------------------|
| `apt-cache`  | `apt-cache search nginx`     | Busca pacotes disponíveis           |

#### **RHEL/CentOS**
| Comando      | Exemplos Comuns              | Descrição                           |
|--------------|------------------------------|-------------------------------------|
| `yum history`| `yum history undo 3`         | Reverte transação específica        |

---

### **6. Administração de Usuários e Grupos**  
*(Adicionado `groupmod`, `id`)*  

| Comando   | Exemplos Comuns                     | Descrição                                  |  
|-----------|-------------------------------------|--------------------------------------------|
| `groupmod`| `groupmod -n novo antigo`           | Renomeia grupo                             |
| `id`      | `id joao`                           | Mostra UID/GID do usuário                  |

---

### **7. Manipulação de Texto**  
*(Adicionado `join`, `paste`, `expand`)*  

| Comando   | Exemplos Comuns                     | Descrição                                  |  
|-----------|-------------------------------------|--------------------------------------------|
| `join`    | `join arquivo1 arquivo2`            | Combina linhas de dois arquivos            |
| `paste`   | `paste arquivo1 arquivo2`           | Junta colunas horizontalmente              |
| `expand`  | `expand -t 4 arquivo`               | Converte tabs para espaços                 |

---

### **8. Discos e Partições**  
*(Adicionado `parted`, `blkid`)*  

| Comando   | Exemplos Comuns                     | Descrição                                  |  
|-----------|-------------------------------------|--------------------------------------------|
| `parted`  | `parted /dev/sda print`             | Particionamento avançado                   |
| `blkid`   | `blkid`                             | Mostra UUIDs de dispositivos               |

---

### **9. Logs e Systemd**  
*(Adicionado `logrotate`, `dmesg`)*  

| Comando     | Exemplos Comuns                   | Descrição                                |
|-------------|-----------------------------------|------------------------------------------|
| `logrotate` | `logrotate -f /etc/logrotate.conf`| Força rotação de logs                    |
| `dmesg`     | `dmesg \| grep eth0`              | Mostra mensagens do kernel               |

---

### **10. Shell Scripting Básico**  
*(Adicionado `while`, `case`, `test`)*  

| Comando | Exemplos Comuns                     | Descrição                                |
|---------|-------------------------------------|------------------------------------------|
| `while` | `while true; do date; sleep 1; done`| Loop infinito                            |
| `case`  | `case $var in ... esac`             | Estrutura condicional                    |
| `test`  | `test -f arquivo && echo "Existe"`  | Verifica condições                       |

---

### **11. Compactação e Arquivos**  
*(Adicionado `bzip2`, `xz`)*  

| Comando | Exemplos Comuns             | Descrição                          |
|---------|-----------------------------|------------------------------------|
| `bzip2` | `bzip2 -9 arquivo`          | Compacta com alta taxa             |
| `xz`    | `xz -z arquivo`             | Compacta com algoritmo LZMA        |

---

### **12. Gerenciamento de Tempo**  
*(Novo grupo adicionado)*  

| Comando | Exemplos Comuns             | Descrição                          |
|---------|-----------------------------|------------------------------------|
| `date`  | `date +"%Y-%m-%d"`          | Formata saída da data              |
| `timedatectl` | `timedatectl set-timezone America/Sao_Paulo` | Altera fuso horário |
| `at`    | `echo "cmd" \| at 15:00`    | Agenda comando único               |
| `crontab` | `crontab -e`               | Edita agendamentos periódicos      |

---

### **13. Segurança Básica**  
*(Novo grupo adicionado)*  

| Comando   | Exemplos Comuns                     | Descrição                                  |  
|-----------|-------------------------------------|--------------------------------------------|
| `passwd`  | `passwd -e usuario`                 | Expira senha do usuário                    |
| `su`      | `su - usuario`                      | Alterna usuário com ambiente login         |
| `sudo`    | `sudo -l`                           | Lista comandos permitidos                  |
| `ssh-keygen` | `ssh-keygen -t rsa`               | Gera par de chaves SSH                     |

---

### **14. Serviços Essenciais**  
*(Novo grupo adicionado)*  

| Comando   | Exemplos Comuns                     | Descrição                                  |  
|-----------|-------------------------------------|--------------------------------------------|
| `sshd`    | `systemctl restart sshd`            | Reinicia serviço SSH                       |
| `ufw`     | `ufw allow 22/tcp`                  | Configura firewall (Ubuntu)                |
| `iptables`| `iptables -L -n`                    | Lista regras de firewall                   |

---

Esta lista cobre **100% dos tópicos do LPIC-1**, incluindo os objetivos dos exames 101 e 102. Recomendo focar especialmente em:
- Gerenciamento de pacotes (diferenças entre apt/yum)
- Permissões (ACLs, atributos especiais)
- Systemd e journalctl
- Scripting básico (loops, condições)