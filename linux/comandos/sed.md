## Comando sed (Stream Editor)
O **`sed`** (Stream Editor) é um comando para edição rápida de texto diretamente no terminal, útil para substituir, deletar, inserir ou extrair conteúdo em arquivos ou streams.  

### Principais usos:  
- **Substituir texto** (o mais comum).  
- **Deletar linhas**.  
- **Filtrar ou transformar texto**.  

---

### **Exemplos práticos:**  

1. **Substituir texto em um arquivo** (troca "foo" por "bar"):  
   ```bash
   sed 's/foo/bar/g' arquivo.txt
   ```  
   - `s` = substituir  
   - `g` = substituir **todas** as ocorrências (sem o `g`, só a primeira de cada linha).  

2. **Salvar as alterações no arquivo** (usa `-i`):  
   ```bash
   sed -i 's/foo/bar/g' arquivo.txt
   ```  

3. **Deletar linhas que contêm "error"**:  
   ```bash
   sed '/error/d' arquivo.txt
   ```  

4. **Extrair linhas específicas (ex.: linhas 10 a 20)**:  
   ```bash
   sed -n '10,20p' arquivo.txt
   ```  

5. **Substituir em apenas uma linha específica (ex.: linha 5)**:  
   ```bash
   sed '5s/foo/bar/' arquivo.txt
   ```  

---

### **Dica útil:**  
- Use `sed` com outros comandos (ex.: `grep`, `cat`). Exemplo:  
  ```bash
  cat log.txt | sed 's/ERROR/CRITICAL/g' | grep "CRITICAL"
  ```  

---

## Exemplo de **regex avançada** usando `sed`, com padrões complexos e grupos de captura:  

### **Exemplo 1: Substituir datas no formato `DD/MM/AAAA` para `AAAA-MM-DD`**  
```bash
echo "Data: 25/12/2023" | sed -E 's#([0-9]{2})/([0-9]{2})/([0-9]{4})#\3-\2-\1#g'
```
**Saída:**  
```
Data: 2023-12-25
```
- `-E` → Habilita **regex estendida** (suporta `+`, `|`, `()` sem escape).  
- `([0-9]{2})` → Captura **2 dígitos** (dia ou mês).  
- `([0-9]{4})` → Captura **4 dígitos** (ano).  
- `#\3-\2-\1#` → Reordena os grupos (`\3` = ano, `\2` = mês, `\1` = dia).  

---

### **Exemplo 2: Extrair emails de um texto**  
```bash
echo "Contato: user@exemplo.com, admin@site.com" | sed -E 's/.*([a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}).*/\1/g'
```
**Saída:**  
```
user@exemplo.com
```
- `[a-zA-Z0-9._%+-]+` → Nome do usuário (ex.: `user.123`).  
- `@[a-zA-Z0-9.-]+` → Domínio (ex.: `@exemplo`).  
- `\.[a-zA-Z]{2,}` → TLD (ex.: `.com`, `.org`).  

---

### **Exemplo 3: Remover comentários HTML**  
```bash
echo "Texto <!-- comentário --> mais texto" | sed -E 's/<!--.*-->//g'
```
**Saída:**  
```
Texto  mais texto
```
- `<!--.*-->` → Casa qualquer texto entre `<!--` e `-->`.  

---

### **Dica para regex avançada no `sed`**  
- Use `-E` (ou `-r` em algumas versões) para evitar escapes excessivos.  
- Para **multilinha**, adicione `:a;N;$!ba;s/...//g` (mais complexo, considere `awk` ou `perl`).  

