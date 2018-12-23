# API del Waves Keeper 

[Descargar](https://drive.google.com/drive/folders/1m4dD4C8pEJ4y6-hpauF9TGSIsevY-3me?usp=sharing)

[Pagina del Demo](https://chrome-ext.wvservices.com/)

Tenga en cuenta que el Waves Keeper también puede soportar [API del Waves Client](https://docs.wavesplatform.com/en/development-and-api/client-api/overview.html): [API de autorizacion Waves](https://docs.wavesplatform.com/en/development-and-api/client-api/auth-api.html), [API de Pago](https://docs.wavesplatform.com/en/development-and-api/client-api/payments-api.html). Si un usuario tiene tanto el Cliente Waves como el Waves Keeper, el Keeper tendra mayor prioridad.
 
En primer lugar, para trabajar con la API, debe agregar un objeto público denominado Waves en su sitio. En este objeto están disponibles las siguientes funciones.


## Autenticación
Para trabajar con una cuenta concreta, necesita implementar la autenticación a través de la función Waves:

`auth(AUTH_DATA)`

donde`AUTH_DATA` es un json en la siguiente forma:

```
AUTH_DATA {
	name: string, //app’s name
	data: string, // data for sign (seed)
	icon: string, // optional parameter: app’s icon (full URL)
  successPath: string // optional parameter: full redirect URL for authentication result, must be https://
}
```

Una solicitud de ejemplo podría verse como:

```
Waves.auth({
    name: 'My App',
    data: 'test secret string',
    successPath: 'https://my-site.com/auth/waves' 
  }).then(
	  res,  // res - the user data + signature of auth data
	  err   // err - the error message
)
```



## Firmar Transaccion

Esta función solo genera una firma para la transacción, pero no la envía al nodo. Puede obtener un objeto "Promise" para autoenviar al nodo.

`signTransaction(TRANSACTION)`

La solicitud completa es:

`Waves.signTransaction(TRANSACTION): Promise<tx>;`


Un ejemplo de `TRANSACTION` puede ser encontrado a continuacion.

 
Un ejemplo de una solicitud para firmar una transacción de transferencia:

```
Waves.signTransaction({
type: 4,
data: {
	amount: {
		assetId: ‘WAVES’,
		tokens: ‘0.123456’
	},
	fee: {
		assetId: ‘WAVES’,
		tokens: ‘0.01’
	},
	recipient: ‘3N5net4nzSeeqxPfGZrvVvnGavsinipQHbE’
}
}).then(
	res,  // res - result for self-sending to the node
	err   // err - the error message 
)

```

## Firmar y publicar una transacción

Esta función firma la transacción, la envía al nodo y devuelve un objeto Promise con la respuesta del servidor. La solicitud completa es:

`Waves.signAndPublishTransaction(TRANSACTION): Promise<tx>;`

Un ejemplo do `TRANSACTION` se encuentra a continuacion. 
También puede haber un parámetro opcional `successPath` : `Waves.signAndPublishTransaction(TRANSACTION, successPath): Promise<tx>;`,
este parámetro puede redirigir al usuario a alguna URL si la transacción se envía con éxito `?txId={id};` 

Un ejemplo de una solicitud para firmar una transacción de transferencia:
```
Waves.signAndPublishTransaction({
  type: 4,
  {
    amount: {
      assetId: 'WAVES',
      tokens: '0.123456'
    },
    fee: {
      assetId: 'WAVES',
      tokens: '0.01'
    },
    recipient: '3N5net4nzSeeqxPfGZrvVvnGavsinipQHbE'
  }
}).then(
  	res,  // res - result of a sending transaction to the server
	err   // err - the error message 
)
```

## Solicitud de firma

Esta función devuelve la firma de los datos. La solicitud completa es:

`Waves.signRequest(SIGN_REQUEST_DATA)`.

```
SIGN_REQUEST_DATA {
	type: REQUEST_TYPE,
	data {}
}
```
```
REQUEST_TYPE {
	MATCHER_ORDERS = 1001,
	COINOMAT_CONFIRMATION: = 1004
}
```

## Orden de firma

Esta función devuelve la firma de los datos solicitados. Firma los datos y devuelve un objeto Promise para autoenviar al matcher.
La solicitud completa es:

`Waves.signOrder(SIGN_ORDER_DATA)`.

## Firmar y publicar orden

Esta función firma el pedido, lo envía al comparador y devuelve un objeto Promise con la respuesta del servidor. La solicitud completa es:
`Waves.signAndPublishOrder(SIGN_ORDER_DATA)`
```
SIGN_ORDER_DATA  {
	type: 1002,
	data: {
		amount: {
			assetId: ASSET_ID,
			tokens: Number|String
		},
		price: {
			assetId: ASSET_ID,
			tokens: Number|String
		},
		orderType: 'string' //  only 'sell' or 'buy'
		matcherFee: {
			assetId: ASSET_ID,
			tokens: Number|String
		},
		expiration: number // timepstamp
		timestamp: number // timepstamp
	}
}
```

## Firmar cancelar orden

Esta función devuelve la firma de los datos de cancelación del pedido. Firma los datos y devuelve un objeto Promise para autoenviar al matcher.

La solicitud completa es:

`Waves.signCancelOrder(SIGN_CANCEL_ORDER_DATA)`.

## Firmar y publicar una orden de cancelacion

Esta función firma el pedido de cancelación, lo envía al emparejador y devuelve un objeto Promesa con la respuesta del servidor. La solicitud completa es:

`Waves.signAndPublishCancelOrder(SIGN_CANCEL_ORDER_DATA)`.
```
SIGN_CANCEL_ORDER_DATA  {
	type: 1003,
	data: {
		id: 'string' // order id
	}
}
```


### Estructura general de "TRANSACTION"

Una `TRANSACTION` en generak es una strin json de la siguiente forma:

```
TRANSACTION  {
type: TRANSACTION_TYPE_NUMBER,
successPath: string,
	data: {
		… TRANSACTION_DATA
}
}
```
### Tipos de transacciones
Las transacciones en Waves pueden ser de 14 tipos (1 - es la transaccion genesis):
```
TRANSACTION_TYPE_NUMBER {
   SEND_OLD = 2,
   ISSUE = 3,
   TRANSFER = 4,
   REISSUE = 5,
   BURN = 6,
   EXCHANGE = 7,
   LEASE = 8,
   CANCEL_LEASING = 9,
   CREATE_ALIAS = 10,
   MASS_TRANSFER = 11,
   DATA = 12,
   SET_SCRIPT = 13,
   SPONSORSHIP = 14
}
```

### Datos de la transacción

Una `TRANSACTION_DATA` contiene información sobre la transacción en un json con el formato estandar de para diferentes tipos de transacciones en Waves:

**Transferencia:**
```
{
  amount: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  recipient: string //base58Address
}
```


**Emitir:**
```
{
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  name: string,
  description: string,
  quantity: string|number,
  precision: number,
  reissuable: boolean
}
```

**Re-emitir:**
```
{
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  reissuable: boolean,
  quantity: string|number,
  assetId: string
}
```

**Quemar:**
```
{
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  reistruesuable: boolean,
  amount: string|number,
  assetId: string,	
}
```

**Arrendar:**
```
{
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  amount: string|number,
  recipient: string,	
}
```

**Cancelar arriendo:**
```
{
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  leaseId: string,
}
```

**Transferencia Masiva:**
```
{
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  totalAmount: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  transfers: [
    {
	    recipient: String,
	    amount: Number|String
    },
    ...
  ]

}
```

**Transacción de datos:**
```
{
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  data: [
	  { type: 'string', key: String, value: String },
    { type: 'number', key: String, value: number  },
    { type: boolean, key: String, value: Boolean  },
    ....
  ],
}
```

**Patrocinio:**
```
{
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  minSponsoredAssetFee: {
    assetId: ASSET_ID,
    tokens: Number|String
  }
}
```

**Establecer Script:**
```
{
  fee: {
    assetId: ASSET_ID,
    tokens: Number|String
  },
  script: string, //a script in Waves script format: 'base64:{script in base64 from RIDE compiler}'
}
```


