# Protocolo de verificación de assets Waves

## Motivacion

La plataforma Waves permite crear y transferir cualquier asset. El único limitante para el creador es pagar una tarifa (actualmente 1 Waves). Esto reduce el umbral para ingresar a la plataforma, pero abre muchas oportunidades para enviar spam a un precio relativamente bajo. También los activos creados a modo de estafa se podrían usar para fines fraudulentos, por ejemplo, duplicando, total o parcialmente, el nombre de una criptomoneda existente o una empresa conocida con el objetivo de engañar a los usuarios.

Queremos proteger a los usuarios de activos sospechosos y garantizar que los activos verificados sean los utilizados. Esto podría ser posible con algún tipo de listado generado por los poseedores de tokens con sistema de votación o por una organización confiable que cumpla con las reglas establecidas, cuyo acceso sea público.

Aquí presentamos un estándar que permite el intercambio de información de tokens entre los proveedores de datos y las aplicaciones que utilizan la blockchain de Waves.

Cualquier compañía o proveedor individual puede proporcionar información sobre tokens, verificar / certificar proyectos que hayan emitido un token en la cadena de bloques Waves. Cualquier aplicación que use la cadena de bloques Waves puede usar la información provista por los proveedores.

Un ejemplo de tal proveedor es [bettertokens] (http://bettertokens.org/) - Tokenization Standards Association, una organización sin fines de lucro, cuya función principal es el desarrollo de estándares de diligencia debida para las compañías que participan en la tokenización de activos y Ofertas iniciales de moneda (ICO) / eventos de generación de token (TGE por sus siglas en Ingles).

## Especificaciones

Nuestro protocolo sirve como una interacción entre los proveedores y la cadena de bloques. Un proveedor puede ser tanto una organización centralizada con una metodología desarrollada, como un servicio descentralizado para clasificar tokens mediante votación o múltifirma.

Cada proveedor tiene su propia dirección de Waves. Se puede crear especialmente para fines de verificación de activos o también para otros objetivos.

![](/_assets/waves_ticker_1.png)

Antes de comenzar a proporcionar información sobre tokens, los proveedores deben completar información sobre sí mismos los datos de DataTransaction. Luego, para cada token, el proveedor debe completar otra entrada de datos en el mismo DataTransaction, con información detallada y del estado del token . DataTransaction es enviado a la dirección de la cuenta inteligente y puede leerse como estado de la cuenta (account state). Ejemplo de dicha transacción en formato JSON:

```
{
  "sender": "3FjTpAg1VbmxSH39YWnfFukAUhxMqmKqTEZ", 
  "data": [
   {
      "key": "data_provider_name", // provider initialization key
      "type": "string", 
      "value": "Example Asset Verification Provider", // company name 
   }, {
      "key": "data_provider_link", 
      "type": "string", 
      "value": "http://example.com", // provider’s site 
   }, {
      "key": "data_provider_email", 
      "type": "string", 
      "value": "example@gmail.com", // contact email 
   }, {
      "key": "data_provider_logo_meta", 
      "type": "string", 
      "value": "data:image/png;base64", // information about a logo type (svg, png, jpg … ) 
   }, {
      "key": "data_provider_logo", 
      "type": "binary", 
      "value": "base64:__base64_image_code__", // provider's logo 
   },  {
      "key": "data_provider_lang_list", 
      "type": "string",
      "value": "en" // a list of available languages for provider's description
    }, {
      "key": "data_provider_description_<en>", // provider initialization key
      "type": "string", 
      "value": "Verification provider", // provider info 
    }
  ]
}
```

La descripción de cada activo consta de varias entradas de datos, la primera es status_id que describe la medida de confianza / amenaza:

Tabla 1. Estado de Tokens 

| Estado | Descripción | Comentar |
| : --- | : --- | : --- |
| 2 | Verificado| Activos verificados y de confianza, los emisores pasaron KYC, tokens de puertas de enlaces oficiales, etc. |
| 1 | Descrito | Fichas con descripción clara que no son phishing o estafa |
| 0 | Desconocido | Estado por defecto. No es necesario agregarlo a la lista de proveedores a menos que el proveedor quiera eliminar un activo de la lista |
| -1 | Sospechoso | El activo parece sospechoso o usado para spam |
| -2 | Peligroso | Fraudes peligrosos y activos de phishing |

```
{
  "sender": "3FjTpAg1VbmxSH39YWnfFukAUhxMqmKqTEZ", 
  "data": [ {
      "key": "status_id_<2L3hRkSJpmaytgSfKLSNgC1vcoUvGGAv2353c6V9hPKC>, // token ID
      "type": "integer", 
      "value": "1", // status
   }, {
      "key": "link_<2L3hRkSJpmaytgSfKLSNgC1vcoUvGGAv2353c6V9hPKC>", 
      "type": "string", 
      "value": "http://example.com", // project site 
   }, {
      "key": "email_<2L3hRkSJpmaytgSfKLSNgC1vcoUvGGAv2353c6V9hPKC>", 
      "type": "string", 
      "value": "example@gmail.com", // project contact email
   }, {
      "key": "description_<en>_<2L3hRkSJpmaytgSfKLSNgC1vcoUvGGAv2353c6V9hPKC>", 
      "type": "string", 
      "value": "Fundada en junio de 2012, Company es una billetera y plataforma de moneda digital donde los comerciantes y consumidores pueden realizar transacciones con nuevas monedas digitales como Bitcoin, Ethereum y Litecoin. Establecido en San Francisco, California. ", // breve descripción del proyecto
   }, {
      "key": "ticker_<2L3hRkSJpmaytgSfKLSNgC1vcoUvGGAv2353c6V9hPKC>", 
      "type": "string", 
      "value": "TKR", // marcador de proyecto asignado
   }, {
      "key": "logo_meta_<2L3hRkSJpmaytgSfKLSNgC1vcoUvGGAv2353c6V9hPKC>", 
      "type": "string", 
      "value": "data:image/png;base64", // logo del proyecto 
   }, {
      "key": "logo_<2L3hRkSJpmaytgSfKLSNgC1vcoUvGGAv2353c6V9hPKC>", 
      "type": "string", 
      "value": "base64:__base64_image_code__", // logo del proyecto
   }
  ]
}
```


Tabla 2. Parámetros para la descripción del proveedor


| Llave | Requerido | Valor |
| :--- | :--- | :--- |
| data_provider_name | true | Nombre del proveedor |
| data_provider_link | true | Un enlace al sitio web del proveedor |
| data_provider_email | false | Correo electrónico de contacto |
| data_provider_description_<language> | true |  Información del lenguaje de servicio del proveedor "data_provider_lang_list"|
| data_provider_lang_list | true | Una lista de los idiomas disponibles en los cuales que se puede agregar al proveedor y sus tokens en formato separado por coma|
| data_provider_logo | false | El logotipo del proveedor en cualquier formato en base64, debe ir acompañado de un campo  "data_provider_logo_meta" |
| data_provider_logo_meta | true | Una descripción del formato de logotipo | 

Tabla 3. Parámetros para describir el token.

| Llave | Requerido | Valor |
| :--- | :--- | :--- |
| status_id_<ASSET_ID> | true | Estado |
| link_<ASSET_ID> | false | Un enlace al sitio web del proveedor |
| email_<ASSET_ID> | false | Correo electrónico de contacto |
| description_<LANG>_<ASSET_ID> | false | Información del lenguaje del servicio del proveedor  "data_provider_lang_list"|
| ticker_<ASSET_ID> | false | Ticker asociado al proyecto |
| logo_<ASSET_ID> | false |   El logotipo del proveedor en cualquier formato en base64, debe ir acompañado de un campo   "logo_meta_<ASSET_ID>" |
| logo_meta_<ASSET_ID> | false | Una descripción del formato de logotipo |



