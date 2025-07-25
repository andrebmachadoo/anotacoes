### **Exemplo Prático de um Ataque com GPU/ASIC**  
Vamos supor que um hacker tenha vazado um **banco de dados com senhas hasheadas** (em SHA-1, que é fraco). Ele quer descobrir as senhas originais.  

---

#### **Passo a Passo do Ataque**  
1. **Dados Vazados**:  
   ```  
   Usuário: username@email.com | Hash: 5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8 (hash de "password123")  
   ```  

2. **Ferramenta Usada**:  
   - **GPU**: Usa um programa como **Hashcat** ou **John the Ripper**.  
   - **ASIC**: Máquina especializada (ex.: Antminer modificado).  

3. **Ataque de Força Bruta**:  
   - O hacker roda um **dicionário de senhas comuns** (ex.: "123456", "senha", "password123").  
   - A GPU/ASIC calcula **1 bilhão de hashes SHA-1 por segundo** e compara com o hash vazado.  

4. **Resultado**:  
   - Em **menos de 1 segundo**, a senha `"password123"` é descoberta.  

---

#### **Código Simplificado (Simulação em Python)**  
```python  
import hashlib  

# Senhas comuns para teste  
senhas_testadas = ["123456", "senha", "password123", "admin"]  

# Hash vazado do banco de dados  
hash_vazado = "5baa61e4c9b93f3f0682250b6cf8331b7ee68fd8"  

# Ataque com GPU (simulado)  
for senha in senhas_testadas:  
    hash_calculado = hashlib.sha1(senha.encode()).hexdigest()  
    if hash_calculado == hash_vazado:  
        print(f"Senha quebrada: {senha}")  
        break  
```  
**Saída**:  
```  
Senha quebrada: password123  
```  

---

### **Como Saber se um Hash é Vulnerável?**  
| Algoritmo  | Resistência a GPU/ASIC | Tempo para Quebrar (exemplo) |  
|------------|------------------------|-----------------------------|  
| **MD5**    | ❌ Péssima             | Milissegundos               |  
| **SHA-1**  | ❌ Ruim                | Segundos                    |  
| **bcrypt** | ✅ Boa (se custo ≥ 12) | Anos                        |  
| **Argon2** | ✅ Excelente           | Séculos                     |  

---

### **O que Acontece se Usar Bcrypt/Argon2?**  
- **Bcrypt (custo=12)**:  
  - Uma GPU consegue testar **apenas ~500 senhas/segundo** (vs. 1 bilhão em SHA-1).  
  - Levaria **anos** para quebrar uma senha média.  

- **Argon2 (parâmetros fortes)**:  
  - Consome **muita memória**, o que paralisa GPUs/ASICs.  
  - Praticamente **invulnerável** a ataques em massa.  

---

### **Como se Proteger na Prática?**  
1. **Para senhas**:  
   ```rust  
   // Rust: Usando Argon2  
   use argon2::{Argon2, PasswordHasher};  
   use argon2::password_hash::SaltString;  

   let senha = "senha_segura";  
   let salt = SaltString::generate(&mut rand::thread_rng());  
   let argon2 = Argon2::default();  
   let hash = argon2.hash_password(senha.as_bytes(), &salt).unwrap();  
   ```  

2. **Para sistemas críticos**:  
   - Adicione **pepper** (segredo global) além do salt.  
   - Use **autenticação de 2 fatores (2FA)**.  

---

### **Resumo Final**  
- **GPUs/ASICs são super-rápidos** para quebrar hashes fracos (MD5, SHA-1).  
- **Solução**: Use **Argon2 ou bcrypt** com parâmetros altos.  
- **Regra de ouro**: Se seu sistema ainda usa SHA-1 para senhas, **mude agora!**  

Quer ver um ataque real em ação (com tempos reais)? Posso mostrar um demo passo a passo! 🔥