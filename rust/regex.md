## Regex em strings 
---

>**Observação:** Rust não tem expressões regulares nativamente, deve ser adicionada 

✅ 1. Adicione ao Cargo.toml:


```toml
[dependencies]
regex = "1"
```
ou 
```sh 
$ cargo add regex
```

✅ 2. Exemplo: Buscar e substituir com regex
```rust
use regex::Regex;

fn main() {
    let texto = "Email: exemplo@gmail.com e outro: teste@empresa.com";
    
    // Regex para buscar e-mails
    let re = Regex::new(r"\b[\w.-]+@[\w.-]+\.\w+\b").unwrap();

    // Substituir todos os e-mails por "[oculto]"
    let resultado = re.replace_all(&texto, "[oculto]");

    println!("{}", resultado);
}

```

✅ 3. Exemplo: Verificar se a string bate com o padrão
```rust
let re = Regex::new(r"^\d{3}-\d{2}-\d{4}$").unwrap(); // ex: 123-45-6789
let valido = re.is_match("123-45-6789");             // true

```

✅ 4. Capturar grupos
```rust
let re = Regex::new(r"(\w+)@(\w+)\.com").unwrap();
let caps = re.captures("contato@exemplo.com").unwrap();

println!("Usuário: {}", &caps[1]);
println!("Domínio: {}", &caps[2]);