# Descripcion del Lenguaje

El lenguaje de contratos inteligentes de Waves es:

* Flojo
* Tipeado fuerte
* Tipeado estadistico
* Basada en la expresion.

## Operaciones y construcciones.

* Operaciones Binarias:`>=`, `>`, `<`, `<=`, `+`, `-`, `&&`, `||`, `*`, `%`, `/`, `==`, `!=`
* Operaciones unarias `-`, `!`
* Declaraciones de constantes via `let`
* Clausula `if-then-else` 
* Acceder a campos de cualquier instancia dentro de estructuras predefinidas por `.`
* Acceder a elementos de lista mediante índice `[]`
* Llamadas de funciones predefinidas mediante `()`

## Tipos de datos disponibles

* `Long`
* `String`
* `Boolean`
* `ByteVector`
* `List[T]`
* Estructura de datos predefinidos no recursivos tales como `Transaction` y `Block`.
* `Unit` - un tipo que tiene una sola instancia, `unit`.
* `Nothing`- "tipo inferior", no puede existir ninguna instancia de este tipo, pero puede aplicarse a cualquier otro tipo.
* Tipos de unión, como `Int | String | Transaction` y `ByteVector | Unit`

### Estructuras

* `Point(x: Int, y: Int)`
* `Alias(name: String)`

La definición de estructuras de usuario está restringida en RIDE.  
Puede crear una instancia de cualquier estructura predefinida llamando al constructor.

```js
let addr = Address(base58'3My3KZgFQ3CrVHgz6vGRt8687sH4oAA1qp8')
let alias = Alias("alicia")
let name  = alias.name
```

### Lista\[T\]

El usuario no puede crear `List[T]` pero él puede introducir datos que contiene algunos campos de`List[T]` . Todas las transacciones contienen campo `proofs: List[ByteVector]` pero las transacciones de transferencia masiva contienen campo `transfers: List[Transfer]`.

Para acceder al elemento de listas puedes usar la sintaxis `list[index]` con el primer elemento en index 0.

Para determinar el recuento de elementos de la lista, puede utilizar la función `size`:

* `size`: `List[T] => Long`
  Esto también es cierto para `DataType.ByteArray`:
* `size`: `DataType.ByteArray => Long`

### ByteVector

Standard ByteVector type

* `size`: `ByteVector => Long`
* `take`: `ByteVector`, `Long` =&gt; `ByteVector`
* `drop`: `ByteVector`, `Long` =&gt; `ByteVector`
* `dropRight`: `ByteVector`, `Long` =&gt; `ByteVector`
* `takeRight`: `ByteVector`, `Long` =&gt; `ByteVector`

### Long

* `fraction(value: LONG, numerator: LONG, denominator: LONG) => LONG`

### String

Standard string type

* `size`: `String => Long`
* `take`: `String`, `Long` =&gt; `String`
* `drop`: `String`, `Long` =&gt; `String`
* `takeRight`: `String`, `Long` =&gt; `String`
* `dropRight`: `String`, `Long` =&gt; `String`

## Pattern Matching

There is a mechanism for checking a value against a pattern. The user can handle different expected types in a match expression.  
A match expression has:

* A value
* The match keyword.
* At least one case clause:
  ```js
  match (tx) {
    case a:TransferTransaction => a.recipient
    case b:MassTransferTransaction => b.transfers
    case _ => false
  }
  ```

# Examples

Here's a complete example for 2 of 3 multi-sig :

```js
let alicePubKey  = base58'B1Yz7fH1bJ2gVDjyJnuyKNTdMFARkKEpV'
let bobPubKey    = base58'7hghYeWtiekfebgAcuCg9ai2NXbRreNzc'
let cooperPubKey = base58'BVqYXrapgJP9atQccdBPAgJPwHDKkh6A8'

let aliceSigned  = if(sigVerify(tx.bodyBytes, tx.proofs[0], alicePubKey  )) then 1 else 0
let bobSigned    = if(sigVerify(tx.bodyBytes, tx.proofs[1], bobPubKey    )) then 1 else 0
let cooperSigned = if(sigVerify(tx.bodyBytes, tx.proofs[2], cooperPubKey )) then 1 else 0

aliceSigned + bobSigned + cooperSigned >= 2
```

**Note** Keep in mind that all `let`'s could actually be inlined, they exist only for the sake of readability.

