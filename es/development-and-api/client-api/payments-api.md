# API de pagos Waves

Si desea que alguien pague con WAVES o con cualquier otro token de Waves, puede utilizar nuestra API de pagos.

## Proceso

1. Debe configurar un botón en su sitio que active la creación de una URL y redirigir hacia ella.
2. Un usuario decide comprar algo y el usuario presiona ese botón.
3. Después de eso, el usuario se redirige al Cliente Waves con una ventana con parámetros de pago.
4. El usuario modifica esos parámetros si es posible y envía el formulario.
5. Si todo está bien, el usuario es redirigido de nuevo al remitente.
6. Se proporciona al remitente un ID de la transacción que puede verificarse si está en el blockchain.

Si el usuario interrumpe el proceso, el usuario permanece en la página del Cliente Waves.

## Detalles

[** Aquí **](https://demo.wavesplatform.com/payment-api) puede encontrar el proyecto de demostración que muestra cómo usar la API de pago para las donaciones. La API de pago permite crear un enlace especial para evitar la entrada de semillas en sitios de terceros.


### Solicitud

[Ejemplo](https://client.wavesplatform.com/#send/WAVES?recipient=your-alias&amount=0.01&attachment=SomeString&referrer=https://example.com&strict): `https://client.wavesplatform.com/#send/WAVES?recipient=your-alias&amount=0.01&attachment=SomeString&referrer=https://example.com&strict`.

La ruta basica es `https://client.wavesplatform.com/#send/{assetId}`. Luego están los parámetros.

#### ID del activo

`/#send/8LQW8f7P5d5PZM7GtZEBgaqRPGSzS3DfPuiXrURJ4AJS` — el ID del activo necesario para el pago. El único parámetro de ruta aquí. _\(Requerido\)_

#### Recipiente

`?recipient=3PCAB4sHXgvtu5NPoen6EXR5yaNbvsEA8Fj` — la dirección \(o un alias \) para enviar los tokens. 

#### Cantidad

`?amount=10.5` —  el número de fichas a pagar. _\(Requerido\)_

#### Datos adjuntos

`?attachment=SomeString` — String adjunto de pago. _\(Opcional\)_

#### Referente

`?referrer=https://example.com/waves-payment` — URL de su servicio. Debe ser solo para HTTPS. _\(Opcional\)_

#### Modo estricto

`?strict` — si se establece esta bandera, un usuario no podrá cambiar los datos en el formulario. _\(Opcional\)_

### Respuesta

Example: `https://example.com/waves-payment?txId=D1USZfZPzVd2XNH9xj52Z81XhxChpwUKDJpQHz2haXRT`.

El ID de la transacción de pago del usuario estará en la consulta.

#### ID de la transacción

`?txId=D1USZfZPzVd2XNH9xj52Z81XhxChpwUKDJpQHz2haXRT` — el ID de la transacción exitosa del usuario.
