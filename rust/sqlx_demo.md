## SQLX Demo
---

### Instalando dependencias 

**1.Via comando:**
```sh 
$ cargo add sqlx --features mysql,runtime-tokio-native-tls
$ cargo add sqlx --features postgres,runtime-tokio-native-tls # para postgress

$ cargo add tokio --features full
```
**2. Manualmente no Cargo.toml**
```toml
[dependencies]
sqlx = { version = "0.7", features = ["mysql", "runtime-tokio-native-tls"] }
sqlx = { version = "0.7", features = ["postgres", "runtime-tokio-native-tls"] } # para postgres
tokio = { version = "1.0", features = ["full"] }
```

### Exemplo de Query Simples (Fetch de Dados)

**Postgres**
```rust
use sqlx::postgres::PgPoolOptions;

#[derive(Debug, sqlx::FromRow)]
struct User {
    id: i32,
    name: String,
    email: String,
}

#[tokio::main]
async fn main() -> Result<(), sqlx::Error> {
    // Configura a conexão com o banco
    let pool = PgPoolOptions::new()
        .max_connections(5)
        .connect("postgres://user:password@localhost/database")
        .await?;

    // Executa uma query e mapeia para a struct `User`
    let users = sqlx::query_as::<_, User>("SELECT id, name, email FROM users WHERE id = $1")
        .bind(1) // Substitui $1 por 1
        .fetch_all(&pool)
        .await?;

    println!("Users: {:?}", users);
    Ok(())
}
```
**Mysql**
```rust
use sqlx::mysql::MySqlPoolOptions;

#[derive(Debug, sqlx::FromRow)]
struct User {
    id: i32,
    name: String,
    email: String,
}

#[tokio::main]
async fn main() -> Result<(), sqlx::Error> {
    // Configura a conexão com o MySQL
    let pool = MySqlPoolOptions::new()
        .max_connections(5)
        .connect("mysql://user:password@localhost/database")
        .await?;

    // Executa uma query e mapeia para a struct `User`
    let users = sqlx::query_as::<_, User>("SELECT id, name, email FROM users WHERE id = ?")
        .bind(1) // Substitui o `?` por 1
        .fetch_all(&pool)
        .await?;

    println!("Users: {:?}", users);
    Ok(())
}
```

**Principais Diferenças (MySQL vs PostgreSQL)**
- **Placeholder:** MySQL usa `?` em vez de `$1`, `$2`.
- **Pool:** `MySqlPoolOptions` em vez de `PgPoolOptions`.
- **String de conexão:** Inicia com `mysql://`.


### Principais Funções do SQLx

- query_as → Mapeia o resultado para uma struct (usando FromRow).
- bind → Previne SQL Injection (substitui $1, $2, etc.).
- fetch_one → Retorna 1 registro.
- fetch_all → Retorna todos os registros.
- execute → Para INSERT/UPDATE/DELETE (retorna u64 de linhas afetadas).


