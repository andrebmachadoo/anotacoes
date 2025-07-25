## Tabela de Algoritmos de Hash e Assinaturas
---

Aqui está uma **tabela comparativa** detalhando os principais **algoritmos de hash** (com e sem chave), suas diferenças e aplicações:

---

### **Tabela de Algoritmos de Hash e Assinaturas**  
| **Algoritmo** | **Tipo**               | **Uso de Chave?** | **Segurança**           | **Aplicações Típicas**                          | **Exemplo de Uso**                          |
|---------------|------------------------|-------------------|-------------------------|-----------------------------------------------|---------------------------------------------|
| **SHA-256**   | Hash criptográfico      | ❌ Não            | ✅ Resistente a colisões | Verificação de integridade de arquivos, blockchains (Bitcoin). | `sha256sum arquivo.iso` |
| **SHA-3**     | Hash criptográfico      | ❌ Não            | ✅ Mais robusto que SHA-256 | Substituição futura para SHA-2.               | Criptografia pós-quântica. |
| **MD5**       | Hash criptográfico      | ❌ Não            | ❌ Inseguro (colisões)  | Checksum de arquivos (não para segurança!).   | `md5sum arquivo.zip` (obsoleto para senhas). |
| **HMAC-SHA256**| Hash com chave (MAC)   | ✅ Sim (chave secreta) | ✅ Seguro com chave forte | Autenticação de tokens (JWT), APIs.          | Assinatura em JWTs (`HS256`). |
| **PBKDF2**    | Hash para senhas        | ✅ Sim (salt + iterações) | ✅ Seguro com parâmetros altos | Derivação de chaves a partir de senhas.      | `PBKDF2-HMAC-SHA256(senha, salt, 10000 iterações)`. |
| **bcrypt**    | Hash para senhas        | ✅ Sim (salt + custo) | ✅ Resistente a GPUs/ASICs | Armazenamento seguro de senhas.              | `hash = bcrypt(senha, salt, custo=12)`. |
| **Argon2**    | Hash para senhas        | ✅ Sim (salt + parâmetros) | ✅ Melhor que bcrypt (2015) | Senhas, chaves derivadas.                    | `Argon2id(senha, salt, memória=64MB, iterações=3)`. |
| **RS256**     | Assinatura digital      | ✅ Sim (chave privada/pública) | ✅ Seguro (RSA + SHA-256) | Tokens JWT, certificados SSL.                | `JWT(RS256): assinado com chave privada, verificado com chave pública`. |
| **ES256**     | Assinatura digital      | ✅ Sim (chave EC privada/pública) | ✅ Seguro (ECDSA + SHA-256) | Tokens JWT em sistemas modernos.             | Assinatura com curva elíptica (ex.: P-256). |

---

### **Explicação das Colunas**  
1. **Tipo**:  
   - **Hash puro**: Transformação irreversível (ex.: SHA-256).  
   - **MAC (Message Authentication Code)**: Hash + chave secreta (ex.: HMAC).  
   - **Assinatura digital**: Hash + chave assimétrica (ex.: RS256).  

2. **Uso de Chave**:  
   - **Sem chave**: Aplicações de integridade (ex.: SHA-256).  
   - **Com chave**: Autenticação/confidencialidade (ex.: HMAC, RS256).  

3. **Segurança**:  
   - ✅ **Aceitável hoje**: SHA-256, Argon2, RS256.  
   - ⚠️ **Obsoleto/Inseguro**: MD5, SHA-1.  

4. **Aplicações**:  
   - **Hashes puros**: Verificar downloads, checksums.  
   - **Hashes com chave**: Tokens JWT, autenticação de mensagens.  
   - **Hashes lentos (senhas)**: bcrypt, Argon2.  

---

### **Exemplos Práticos**  
#### **1. SHA-256 (sem chave)**:  
```bash  
echo -n "dado" | sha256sum  
# Saída: 3a6eb0790f39ac87c94f3856b2dd2c5d110e6811602261a9a923d3bb23adc8b7  
```  

#### **2. HMAC-SHA256 (com chave)**:  
```python  
import hmac  
hmac.new(b"chave_secreta", b"mensagem", "sha256").hexdigest()  
# Saída: 'a7d8b9...' (depende da chave)  
```  

#### **3. RS256 (JWT com chave assimétrica)**:  
```json  
// Header:  
{ "alg": "RS256", "typ": "JWT" }  

// Payload:  
{ "sub": "user123", "exp": 1735689600 }  

// Signature:  
RSA-SHA256(base64Url(header) + "." + base64Url(payload), chave_privada)  
```  

---

### **Quando Usar Cada Um?**  
- **Armazenar senhas**: `Argon2` ou `bcrypt`.  
- **Tokens JWT**: `HS256` (simétrico) ou `RS256/ES256` (assimétrico).  
- **Verificar arquivos**: `SHA-256`.  
- **APIs seguras**: `HMAC-SHA256`.  

---

### **Cuidados**  
- **Nunca use MD5/SHA-1** para segurança.  
- **Prefira algoritmos lentos** (bcrypt, Argon2) para senhas.  
- **JWTs**: Use `RS256` ou `ES256` se precisar distribuir chaves públicas.  



---


### Esclarecendo esses termos de forma **prática e direta**! Todos estão relacionados a **técnicas para fortalecer hashes** (especialmente usadas em **senhas**).  

---

### **1. Salt + Iterações**  
#### **O que é?**  
- **Salt**: Valor aleatório único (como já explicado).  
- **Iterações**: Número de vezes que o algoritmo de hash é **reprocessado** sobre o dado.  

#### **Como funciona?**  
```python  
hash = senha + salt  
for _ in range(iterações):  
    hash = algoritmo_hash(hash)  # Reprocessa o hash múltiplas vezes  
```  

#### **Exemplo Prático (PBKDF2)**:  
```rust  
use pbkdf2::pbkdf2_hmac;  
use sha2::Sha256;  

let senha = "senha123";  
let salt = "salto_aleatorio";  
let mut hash = [0u8; 32]; // Tamanho do hash (ex.: 32 bytes para SHA-256)  

// 10.000 iterações:  
pbkdf2_hmac::<Sha256>(senha.as_bytes(), salt.as_bytes(), 10_000, &mut hash);  
```  

#### **Por que usar?**  
- **Aumenta o custo computacional** para ataques de força bruta.  
- **Padrão em algoritmos como PBKDF2**.  

---

### **2. Salt + Custo**  
#### **O que é?**  
- **Custo (cost)**: Parâmetro que define **quão lento** o hash deve ser (ex.: em `bcrypt`). Quanto maior, mais recursos computacionais são necessários.  

#### **Como funciona?**  
- Em `bcrypt`, o custo controla:  
  - Número de rodadas do algoritmo (ex.: `2^cust`).  
  - Memória usada.  

#### **Exemplo Prático (bcrypt)**:  
```rust  
use bcrypt::hash;  

let senha = "senha123";  
let custo = 12; // 2^12 iterações (balanceia segurança vs. desempenho)  
let hash = hash(senha, custo)?;  
```  

#### **Por que usar?**  
- **Adaptável ao hardware**: Você pode aumentar o `custo` conforme a evolução da tecnologia.  
- **Inviabiliza ataques com GPUs/ASICs**.  

---

### **3. Salt + Parâmetros**  
#### **O que é?**  
- **Parâmetros ajustáveis**: Em algoritmos como `Argon2`, você define múltiplos fatores:  
  - **Iterações** (time cost).  
  - **Memória** (em MB/KB).  
  - **Grau de paralelismo** (threads).  

#### **Exemplo Prático (Argon2)**:  
```rust  
use argon2::{Argon2, Algorithm, Version, Params};  

let senha = "senha123";  
let salt = "salto_aleatorio";  

let params = Params::new(  
    65536,  // Memória (64MB)  
    3,      // Iterações  
    4,      // Paralelismo (threads)  
    None    // Tamanho do hash (opcional)  
)?;  

let argon2 = Argon2::new(Algorithm::Argon2id, Version::V0x13, params);  
let hash = argon2.hash_password(senha.as_bytes(), salt.as_bytes())?;  
```  

#### **Por que usar?**  
- **Personalização fina**: Adapta-se a diferentes cenários (ex.: servidores com muita RAM).  
- **Resistência a ataques especializados** (como GPUs).  

---

### **Resumo das Diferenças**  
| **Termo**       | **Definição**                                  | **Exemplo de Algoritmo** |  
|------------------|-----------------------------------------------|--------------------------|  
| **Iterações**    | Número de reprocessamentos do hash.           | PBKDF2                   |  
| **Custo**        | Fator exponencial que controla complexidade.  | bcrypt                   |  
| **Parâmetros**   | Ajustes de memória, iterações e paralelismo.  | Argon2                   |  

---

"Iterações = É o número de vezes que o algoritmo **recalcula o hash internamente** para tornar o processo mais lento (e resistente a ataques).  

---

### **Exemplo Visual**  
Imagine que um atacante tente quebrar uma senha:  
- **Sem iterações/custo**: Pode testar 1 bilhão de senhas/segundo.  
- **Com iterações/custo alto**: Só consegue testar 1.000 senhas/segundo.  

---

### **Quando Usar Cada Um?**  
- **PBKDF2**: Sistemas legados ou onde simplicidade é importante.  
- **bcrypt**: Bom equilíbrio entre segurança e facilidade de uso.  
- **Argon2**: Máxima segurança (recomendado hoje).  

