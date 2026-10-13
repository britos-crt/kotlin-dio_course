O controle de fluxo em Kotlin é composto por:

* estruturas condicionais (`if`, `when`)
*  laços de repetição (`for`, `while`, `do-while`)
*  expressões de salto (`break`, `continue`, `return`)

---

### 1. `if` e `else`
Em Kotlin, o `if` pode ser utilizado tanto como uma instrução comum quanto como uma **expressão** que retorna um valor. 
Por conta disso, a linguagem não possui um operador ternário (`condicao ? a : b`).

```kotlin

val a = 10
val b = 20

// Uso tradicional como instrução
if (a > b) {
    println("a é maior")
} else {
    println("b é maior")
}

// Uso como expressão (retorna valor)
val maior = if (a > b) a else b

// Com blocos de código (o último valor do bloco é retornado)
val resultado = if (a > b) {
    println("Avaliando 'a'...")
    a
} else {
    println("Avaliando 'b'...")
    b
}

```

---

### 2. `when`
O `when` substitui o tradicional `switch` de outras linguagens, porém é mais poderoso e flexível. 
Ele avalia seus argumentos sequencialmente até que uma condição seja satisfeita.

#### Uso como substituto do `switch`:

```kotlin

val x = 2

when (x) {
    1 -> println("x é 1")
    2, 3 -> println("x é 2 ou 3")
    in 4..10 -> println("x está no intervalo de 4 a 10")
    !in 11..20 -> println("x não está entre 11 e 20")
    else -> println("Nenhuma condição atendida")
}

```

#### Verificação de tipos (`is`) e atribuição como expressão:

```kotlin

val objeto: Any = "Olá, Kotlin"

val descricao: String = when (objeto) {
    is String -> "É uma String com tamanho ${objeto.length}"
    is Int -> "É um número inteiro"
    is Boolean -> "É um valor booleano"
    else -> "Tipo desconhecido"
}

```

#### Uso sem argumento (substitui cadeias complexas de `if/else`):

```kotlin

val nota = 85

when {
    nota >= 90 -> println("A")
    nota >= 80 -> println("B")
    nota >= 70 -> println("C")
    else -> println("Reprovado")
}

```

---

### 3. Laços de Repetição

#### `for`
Itera sobre qualquer estrutura que forneça um iterador (como intervalos/ranges, arrays e coleções).

```kotlin

// Intervalos numéricos (Ranges)
for (i in 1..5) { print(i) }        // 12345 (inclusivo)
for (i in 1 until 5) { print(i) }  // 1234 (exclui o último elemento)
for (i in 5 downTo 1) { print(i) } // 54321 (ordem decrescente)
for (i in 1..10 step 2) { print(i) } // 13579 (incremento customizado)

// Coleções
val frutas = listOf("Maçã", "Banana", "Uva")

for (fruta in frutas) {
    println(fruta)
}

// Iterando com índice
for ((index, fruta) in frutas.withIndex()) {
    println("Posição $index: $fruta")
}

```

#### `while` e `do-while`
Funcionam da mesma forma que em outras linguagens da família C:

```kotlin

var contador = 0

// Avalia a condição antes de executar
while (contador < 3) {
    println("Contador: $contador")
    contador++
}

// Executa pelo menos uma vez antes de avaliar a condição
do {
    println("Executou do-while")
} while (contador < 0)

```

---

### 4. Expressões de Salto e Rótulos (Labels)
Além de `return`, `break` e `continue`, o Kotlin permite usar **rótulos (labels)** identificados com o símbolo `@` 
para controlar o fluxo em laços aninhados ou lambdas.

#### Rótulos com laços de repetição:

```kotlin

loopExterno@ for (i in 1..3) {
    for (j in 1..3) {
        if (i == 2 && j == 2) {
            break@loopExterno // Interrompe o laço externo diretamente
        }
        println("i = $i, j = $j")
    }
}

```

#### Rótulos com expressões lambda:

```kotlin

val numeros = listOf(1, 2, 3, 4, 5)

numeros.forEach {
    if (it == 3) return@forEach // Funciona como um 'continue', pulando o item 3
    println(it)
}

```
