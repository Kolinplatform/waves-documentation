## Funciones Privadass

Todas las funciones privadas aqui explicadas requieren una clave API en cada HTTP requerida utilizando el encabezado `X-Api-Key`. El parametro por defecto es`ridethewaves!`. El valor de encabezado asegurado mediante hash es almacenado en la configuracion del `rest-api.api-key-hash` en el archivo de configuracion waves.conf. Ver [/utils/hash/secure](https://github.com/wavesplatform/Waves/wiki/Waves-Node-REST-API#post-utilshashsecure) Para obtener más información sobre cómo obtener un hash seguro.

### POST /asset/ emision

Emitir un nuevo activo para una dirección que existe en la cartera del nodo.

**Solicitar parametros:**

    Lo mismo que en [Broadcast Issue Assets] ademas de los parametros `senderPublicKey`, `timestamp` y `signature` .
    "sender" - Dirección de la cuenta del remitente existente en el nodo, codificado mediante Base58

**Ejemplo de solicitud JSON:**

```js
{
  "name": "Test Asset 1",
  "quantity": 100000000000,
  "description": "Some description",
  "sender": "3NBVqYXrapgJP9atQccdBPAgJPwHDKkh6A8",
  "decimals": 8,
  "reissuable": true,
  "fee": 100000000
}
```

**Parametros de Respuesta:**

```
Lo mismo que en [Broadcast Issue Assets]
```

**Ejemplo de respuesta JSON:**

```
The same as in [Broadcast Issue Assets]
```

### POST /assets/reissue

Volver a emitir una cantidad adicional del Activo

**Solicitar parametros:**

    Lo mismo que en [Broadcast Reissue Assets] ademas de los parametros `senderPublicKey`, `timestamp` y `signature`.
    "sender" - Dirección de la cuenta del remitente existente en el nodo, codificado mediante Base58

**Ejemplo de solicitud JSON:**

```js
{
  "quantity": 22300000000,
  "assetId": "E9yZC4cVhCDfbjFJCc9CqkAtkoFy5KaCe64iaxHM2adG",
  "sender": "3NBVqYXrapgJP9atQccdBPAgJPwHDKkh6A8",
  "reissuable": true,
  "fee": 100000
}
```

**Parametros de respuesta:**

```
Lo mismo que en [Broadcast Reissue Assets]
```

**Ejemplo de respuesta JSON:**

```
Lo mismo que en [Broadcast Reissue Assets]
```

### POST /assets/burn

Quemar cierta cantidad del activo.

**Parametros de solicitud:**

```
"assetId" - ID de activo previamente emitido, codificado en Base58
"sender" - Dirección del remitente, codificada en base58
"fee" - Tarifa de transacción por emisión de activos, minimo = 100000
"amount" - Cantidad de activos para quemar (número de piezas indivisibles de activos)
```

**Ejemplo de solicitud JSON:**

```js
{
  "sender" : "EHDZiTW9uhZmpfKRyJtusHXCQ3ABwJ3t9dxZdiPp2GZC",
  "fee" : 100000000,
  "assetId" : "AP5dp4LsmdU7dKHDcgm6kcWmeaqzWi2pXyemrn4yTzfo",
  "amount" : 50000
}
```

**Ejemplo de respuesta JSON:**

```js
{
  "type" : 6,
  "id" : "AoqmyXSurAoLqH5zbcKPtksdPwadgudhE7tZ495cQDWs",
  "sender" : "3HRUALDoUaWAmAndWRqhbiQFoqgamhAVggE",
  "senderPublicKey" : "EHDZiTW9uhZmpfKRyJtusHXCQ3ABwJ3t9dxZdiPp2GZC",
  "fee" : 100000000,
  "timestamp" : 1495623946088,
  "signature" : "4sWPrZFpR379XC4Med1y8AK2Avmx8nVUxVAzsE4QMzEeMtQyHgjzfQsi2Y5VY7diCqMAzohy9ZSTP3yfiB3QPQMd",
  "assetId" : "AP5dp4LsmdU7dKHDcgm6kcWmeaqzWi2pXyemrn4yTzfo",
  "amount" : 50000
}
```

### POST /assets/transfer

Crear transacción para transferir activos de una dirección a otra.

** Parámetros de solicitud: **

    Lo mismo que en [Broadcast Transfer Assets] ademas de los parametros `senderPublicKey`, `timestamp` y `signature`.
    "sender" - Dirección de la cuenta del remitente existente en el nodo, codificado mediante Base58

**Ejemplo de solicitud JSON:**

```js
{
  "assetId": "E9yZC4cVhCDfbjFJCc9CqkAtkoFy5KaCe64iaxHM2adG",
  "sender": "3NBVqYXrapgJP9atQccdBPAgJPwHDKkh6A8",
  "recipient": "3Mx2afTZ2KbRrLNbytyzTtXukZvqEB8SkW7",
  "fee": 100000,
  "amount": 5500000000,
  "attachment": "BJa6cfyGUmzBFTj3vvvaew"
}
```

**Parametros de Respuesta:**

```
Lo mismo que en [Broadcast Transfer Assets]
```

**Ejemplo de respuesta JSON:**

```
Lo mismo que en [Broadcast Transfer Assets]
```

### POST /assets/masstransfer

Crear una transacción para transferir un activo a varias direcciones de destinatarios a la vez.

**Solicitar parametros:**

```
"version" - Actualmente 1
"sender" - Dirección del remitente, codificada en base58
"assetId" - ID del activo a enviar. Por defecto, se supone WAVES.
"transfers" - listado en pares (destinatarios, cantidad)  donde:
   "recipient" es una dirección codificada en Base58, y
   "amount" es la cantidad a enviar a esa dirección.
"fee" - Tarifa de transacción, por defecto 100000 + 50000 * (número de transferencias)
"attachment" - Mensaje arbitrario, codificado en Base58, de 140 bytes máx.
```

**Ejemplo de solicitud JSON:**

```js
{
  "version" : 1,
  "sender" : "3HhQxe5kLwuTfE3psYcorrhogY4fCwz2BSh",
  "fee" : 200000,
  "assetId" : null,
  "attachment" : "59QuUcqP6p",
  "transfers" : [ {
    "recipient" : "3HUQa6qtLhNvBJNyPV1pDRahbrcuQkaDQv2",
    "amount" : 100000000
  }, {
    "recipient" : "3HaAdZcCXAqhvFj113Gbe3Kww4rCGMUZaEZ",
    "amount" : 200000000
  } ]
}
```

**Ejemplo de respuesta JSON:**

```js
{
  "type" : 11,
  "id" : "BG7MQF8KffVU6MMbJW5xPowVQsohwJhfEJ4wSF8cWdC2",
  "sender" : "3HhQxe5kLwuTfE3psYcorrhogY4fCwz2BSh",
  "senderPublicKey" : "7eAkEXtFGRPQ9pxjhtcQtbH889n8xSPWuswKfW2v3iK4",
  "fee" : 200000,
  "timestamp" : 1518091313964,
  "signature" : "4Ph6RpcPFfBhU2fx6JgcHLwBuYSpnEzfHvuAHaVVi8mPjn9D69LX7UaCtBEGjtaTJ7uBwhF38nc7wMEZDL4rYLDV",
  "assetId" : null,
  "attachment" : "59QuUcqP6p",
  "transfers" : [ {
    "recipient" : "3HUQa6qtLhNvBJNyPV1pDRahbrcuQkaDQv2",
    "amount" : 100000000
  }, {
    "recipient" : "3HaAdZcCXAqhvFj113Gbe3Kww4rCGMUZaEZ",
    "amount" : 200000000
  } ]
}
```

### POST /assets/make-asset-name-unique

Crear transacción para hacer el nombre de activo único .

**Request params:**

```
"assetId" - ID de activo previamente emitido, codificado en Base58
"sender" - Dirección del remitente, codificada en base58
"fee" - Tarifa de transacción por emisión de Activos, min = 100000
"networkByte" - byte de red ('W' - 87 - mainnet, 'T' - 84 - testnet)
```

**Ejemplo de solicitud JSON:**

```js
{
    "type" : 11,
    "id" : "GRhSHwLLNFz2HmxabiPU521U4NAkLshk2wgqbD9EBqEA",
    "sender" : "3Hb3qXPdr3UikMBefgyu6dZKwG5Hjuphpc4",
    "senderPublicKey" : "8fYJWvPAyUQgVCMuSVNwpZEAgg4E4vn8gz9hRWMsRu31",
    "fee" : 1000000000,
    "timestamp" : 1495637586986,
    "signature" : "2XCbkLbKhKJrcnCUg18LEBykC54cUqtxCMbVpNrzDkXHJG11ZLQB9vSz2Ha8r4hCqgFPRAvvoo4zFecv27v4DCB3",
    "assetId" : "91MxUYbum9hrpJUcRwVe4no36ViqnQGAUaSmM8V8L8Jx",
    "networkByte" : 73
```

**Ejemplo de respuesta JSON:**

```js
{
    "type" : 11,
    "id" : "GRhSHwLLNFz2HmxabiPU521U4NAkLshk2wgqbD9EBqEA",
    "sender" : "3Hb3qXPdr3UikMBefgyu6dZKwG5Hjuphpc4",
    "senderPublicKey" : "8fYJWvPAyUQgVCMuSVNwpZEAgg4E4vn8gz9hRWMsRu31",
    "fee" : 1000000000,
    "timestamp" : 1495637586986,
    "signature" : "2XCbkLbKhKJrcnCUg18LEBykC54cUqtxCMbVpNrzDkXHJG11ZLQB9vSz2Ha8r4hCqgFPRAvvoo4zFecv27v4DCB3",
    "assetId" : "91MxUYbum9hrpJUcRwVe4no36ViqnQGAUaSmM8V8L8Jx",
    "networkByte" : 73
  }
```



