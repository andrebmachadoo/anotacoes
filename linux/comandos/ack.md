# Comando ack
---

>O comando `ack` é uma ferramenta de busca em código-fonte, similar ao `grep`, mas otimizado para programadores.

### Principais vantagens:  
- Ignora arquivos não relevantes (como `.git/`, `node_modules/`, etc.) por padrão.  
- Destaca os resultados com cores.  
- Sintaxe mais simples para buscas em códigos.  

### Exemplos básicos:  
1. **Buscar uma palavra em arquivos do diretório atual**:  
   ```bash
   ack "function"
   ```  
2. **Buscar case-insensitive**:  
   ```bash
   ack -i "error"
   ```  
3. **Mostrar apenas os nomes dos arquivos que contêm a busca**:  
   ```bash
   ack -l "TODO"
   ```  
4. **Buscar em um tipo específico de arquivo (ex.: `.js`)**:  
   ```bash
   ack --js "console.log"
   ```  

Se não tiver instalado, pode instalar via:  
- **Linux (Debian/Ubuntu)**: `sudo apt install ack`  
- **macOS (Homebrew)**: `brew install ack`  

É mais rápido e prático que `grep` para trabalhar com código.