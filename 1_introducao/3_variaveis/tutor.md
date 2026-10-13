# Kotlin
Declaração de variáveis é baseada principalmente na mutabilidade (se o valor pode ser alterado ou não) e na inferência de tipos.

---

### 1. `val` vs `var`
A palavra-chave utilizada define se a variável pode ter seu valor alterado após a atribuição inicial:

* **`val` (Value / Imutável):**
   Cria uma referência de apenas leitura. Uma vez atribuído o valor, ele não pode ser alterado. Equivale ao `final` do Java. **É a forma recomendada por padrão em Kotlin.**

* **`var` (Variable / Mutável):**
  Permite que o valor seja alterado posteriormente.

```kotlin

fun main() {
    val pais = "Brasil"
    // pais = "Argentina" // ERRO: val não pode ser reatribuído

    var contador = 0
    contador = 1 // Funciona perfeitamente
}

```

---

### 2. Inferência de Tipos e Tipagem Explícita
O compilador do Kotlin consegue deduzir o tipo da variável pelo valor atribuído. 
No entanto, você também pode especificar o tipo explicitamente usando `: Tipo`.

```kotlin

// Inferência automática
val nome = "Carlos"     // Tipo deduzido: String
val idade = 30          // Tipo deduzido: Int
val altura = 1.75       // Tipo deduzido: Double

// Tipagem explícita
val cidade: String = "São Paulo"
val saldo: Double = 250.50

```

---

### 3. Null Safety (Segurança Nula)
Por padrão, as variáveis em Kotlin **não podem** receber o valor `null`, o que previne o famoso erro `NullPointerException`. 
Para permitir que uma variável seja nula, adicione um ponto de interrogação (`?`) ao tipo.

```kotlin

var nome: String = "Ana"
// nome = null // ERRO de compilação

var apelido: String? = "Aninha"
apelido = null // Permitido

```

Ao usar variáveis que podem ser nulas (`Nullable`), o Kotlin exige que você lide com a possibilidade de `null` antes de acessar 
seus métodos ou propriedades:

```kotlin

val tamanho: Int? = apelido?.length // Chamada segura (retorna null se apelido for null)
val tamanhoGarantido: Int = apelido?.length ?: 0 // Operador Elvis (se for null, usa 0)

```

---

### 4. Principais Tipos de Dados
Em Kotlin, tudo é um objeto (não existem tipos primitivos expostos ao desenvolvedor como no Java, embora o compilador otimize isso internamente).

* **Números Inteiros:**
  `Byte`, `Short`, `Int`, `Long`

* **Números Ponto Flutuante:**
  `Float`, `Double`

* **Texto e Caracteres:**
  `String`, `Char`

* **Booleanos:**
  `Boolean` (`true` ou `false`)

---

### 5. Inicialização Tardia (`lateinit` e `lazy`)
Caso você não possa inicializar a variável no momento da declaração:

#### `lateinit var`
Utilizado para variáveis **mutáveis** (`var`) cujo valor será atribuído antes do primeiro uso 
(comum em testes, Android View Binding ou injeção de dependências).

```kotlin

lateinit var usuario: String

fun inicializar() {
    usuario = "João"
}

```

#### `by lazy`
Utilizado para variáveis **imutáveis** (`val`). O valor só é calculado na primeira vez em que a variável for acessada 
na execução do código (inicialização preguiçosa).

```kotlin

val conexaoBanco: String by lazy {
    // Código pesado executado apenas quando 'conexaoBanco' for acessado pela primeira vez
    "Conectado ao Banco de Dados"
}

```
