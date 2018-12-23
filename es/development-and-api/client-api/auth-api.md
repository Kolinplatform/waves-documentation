# API de autorizacion de Waves 

Si quieres autorizar a un usuario en tu servicio utilizando su cuenta Waves, aqui esta la solucion. En general, el ususario debe ser redireccionado al cliente oficial de Waves \([https://client.wavesplatform.com/](https://client.wavesplatform.com/)\) junto a ciertos parametros incluyendo la informacion ha ser firmada por el usuario.

Esto puede ser necesario en casos cuando se necesite trabajar con datos personales del usuario y tambien para estar seguro que una cuenta en la  blockchain pertenece a ese usuario.

## Proceso

1. Agregas el widget de Waves Auth en tu website.
2. El usuario entra a tu sitio y desea iniciar sesión con su cuenta Waves.
3. Hace clic en el botón del widget y se redirige al cliente oficial de Waves, junto con algunos datos aleatorios del widget.
4. Allí, el usuario elige si iniciar sesión o cancelar la operacion.
5. Si continúa, los datos se firmarán con la clave privada del usuario..
6. Luego, el usuario es redirigido a tu sitio, junto con su firma y su clave pública.
7. Usted verifica la validez de la firma con los datos proporcionados por el usuario.
8. Si todo es correcto, el usuario ahora está autenticado en tu servicio.

Si el usuario interrumpe el proceso, permanece en la página del Cliente Waves.

## Detalles

Debido a las limitaciones de longitud de la string de consulta, todos los parámetros se expresan con un solo carácter.

[**Aquí**](https://demo.wavesplatform.com) pueses encontrar una demo  mostrando el uso de la Web auth API.

### Solicitud

[Ejemplo](https://client.wavesplatform.com#gateway/auth?r=https://example.com&n=Service%20Name&d=0123456789abc&i=/img/logo.png&success=/wavesAuth): `https://client.wavesplatform.com#gateway/auth?r=https://example.com&n=Service%20Name&d=0123456789abc&i=/img/logo.png&success=/wavesAuth`.

La ruta de acceso básica es `https://client.wavesplatform.com#gateway/auth`. Posteriormente los parámetros de consulta son enviados.

#### Referente

`?r=https://example.com` — la URL de tu website. Debe ser HTTPS. _\(Required\)_

#### Nombre

`?n=Service%20Name` — el nombre de tu servicio. _\(Required\)_

#### Datos

`?d=randomChars` — Los datos que están firmados por la clave privada del usuario. _\(Required\)_

#### Ruta del icono

`?i=/path/to/the/icon.png` — una ruta relativa al parámetro Referido. Alberga el logo de tu aplicación.. _\(Optional\)_

#### Ruta de confirmacion

`?s=/path/to/an/API/method` — una ruta al método que redirige al usuario mientras la firma se realiza correctamente. De forma predeterminada, el usuario se redirige a la raíz de referencia. _\(Optional\)_

#### Modo de depuración

`?debug=true` — una flag para mostrar mensajes de error. _\(Optional\)_

### Respuesta

Ejemplo: `https://example.com/?s=2w7QKSkxKEUwCVhx2VGrt5YiYVtAdoBZ8KQcxuNjGfN6n4fi1bn7PfPTnmdygZ6d87WhSXF1B9hW2pSmP7HucVbh&p=2M25DqL2W4rGFLCFadgATboS8EPqyWAN3DjH12AH5Kdr&a=3PCAB4sHXgvtu5NPoen6EXR5yaNbvsEA8Fj`

#### Firma

`?s=base58EncodedSignature` — a signature of the data which is signed by the user's private key.

#### Llave Publica

`?p=base58EncodedPublicKey` — clave pública del usuario.

#### Dirección

`?a=base58EncodedAddress` — la dirección Waves del usuario.

### Cómo comprobar la validez de la firma

Puedes usar el paquete npm [@waves/signature-generator](https://www.npmjs.com/package/@waves/signature-generator).

Los datos firmados constan de tres objetos. `Prefix string` + `URL host` + `Provided Data`
La firma se toma desde los datos en el siguiente orden: una string `WavesWalletAuthentication`, luego una string con el parámetro de host, luego una string con el valor de parámetro de datos.
Todas las string se convierten a `length bytes + value bytes` como en [Data Transactions](technical-details/data-transaction.md)
La string de prefijo y el host se requieren por motivos de seguridad, si un servicio malintencionado intenta utilizar los datos de transacción y la firma de Auth API, no sería posible transmitirlos a la blockchain.

También sugerimos la validación de la dirección en caso de que la firma y la clave pública sean válidas pero la dirección haya sido cambiada.

#### ejemplo de codigo Js
```javascript
const sg = require('@waves/signature-generator')
const crypto = sg.utils.crypto
const StringWithLength = sg.StringWithLength
const generate = sg.generate
const base58 = sg.libs.base58

const generator = new generate([
  new StringWithLength('prefix'),
  new StringWithLength('host'),
  new StringWithLength('data')
]);

function authValidate(data, sign, publicKey) {
  const prefix = 'WavesWalletAuthentication'

  const byteGen = new generator({
    prefix: prefix,
    host: data.host,
    data : data.data,
  });

   return byteGen.getBytes()
    .then(
      function (bytes) {
        return crypto.isValidSignature(bytes, sign, publicKey)
      })
}

function addressValidate(publicKey, address) {
  var publicKeyBytes = base58.decode(publicKey)
  var addressFromPublicKey = crypto.buildRawAddress(publicKeyBytes)

  return (addressFromPublicKey == address)
}

//Signed data from example link
var signedData = {
  host: 'example.com',
  data: '0123456789abc'
}

var realSignature = '2w7QKSkxKEUwCVhx2VGrt5YiYVtAdoBZ8KQcxuNjGfN6n4fi1bn7PfPTnmdygZ6d87WhSXF1B9hW2pSmP7HucVbh'
var publicKey = '2M25DqL2W4rGFLCFadgATboS8EPqyWAN3DjH12AH5Kdr'
var address = '3PCAB4sHXgvtu5NPoen6EXR5yaNbvsEA8Fj'

//Check returned address and address from public key
var addressValidation = addressValidate(publicKey, address)
console.log('Address validation: ' + addressValidation + '\n')

//Example with real signature
let signatureCheck = authValidate(signedData, realSignature, publicKey)

signatureCheck.then(function(result) {
  console.log('Host: ' + signedData.host)
  console.log('Data: ' + signedData.data)
  console.log('Public key: ' + publicKey)
  console.log('Address: ' + address)
  console.log('Real signature: ' + realSignature)
  console.log('Real signature check: ' + result + '\n')
})

//Example with fake signature
var fakeSignature = '29qWReHU9RXrQdQyXVXVciZarWXu7DXwekyV1zPivkrAzf4VSHb2Aq2FCKgRkKSozHFknKeq99dQaSmkhUDtZWsw'
signatureCheck = authValidate(signedData, fakeSignature, publicKey)

signatureCheck.then(function(result) {
  console.log('Host: ' + signedData.host)
  console.log('Data: ' + signedData.data)
  console.log('Public key: ' + publicKey)
  console.log('Address: ' + address)
  console.log('Fake signature: ' + fakeSignature)
  console.log('Fake signature check: ' + result + '\n')
})
```

#### Ejemplo de codigo Python
```python
import axolotl_curve25519 as curve
import pywaves.crypto as crypto
import base58
from urllib.parse import urlparse, parse_qs


def str_with_length(string_data):
    string_length_bytes = len(string_data).to_bytes(2, byteorder='big')
    string_bytes = string_data.encode('utf-8')
    return string_length_bytes + string_bytes


def signed_data(host, data):
    prefix = 'WavesWalletAuthentication'
    return str_with_length(prefix) + str_with_length(host) + str_with_length(data)


def verify(public_key, signature, message):
    public_key_bytes = base58.b58decode(public_key)
    signature_bytes = base58.b58decode(signature)

    return curve.verifySignature(public_key_bytes, message, signature_bytes) == 0


def verifyAddress(public_key, address):
    public_key_bytes = base58.b58decode(public_key)
    unhashed_address = chr(1) + str('W') + crypto.hashChain(public_key_bytes)[0:20]
    address_hash = crypto.hashChain(crypto.str2bytes(unhashed_address))[0:4]
    address_from_public_key = base58.b58encode(crypto.str2bytes(unhashed_address + address_hash))

    return address_from_public_key.decode() == address



redirected_url = 'https://example.com/?s=2w7QKSkxKEUwCVhx2VGrt5YiYVtAdoBZ8KQcxuNjGfN6n4fi1bn7PfPTnmdygZ6d87WhSXF1B9hW2pSmP7HucVbh&p=2M25DqL2W4rGFLCFadgATboS8EPqyWAN3DjH12AH5Kdr&a=3PCAB4sHXgvtu5NPoen6EXR5yaNbvsEA8Fj'
parsed_url = urlparse(redirected_url)
parsed_query = parse_qs(parsed_url.query)

address = parsed_query['a'][0]
pub_key = parsed_query['p'][0]
signature = parsed_query['s'][0]
data_string = '0123456789abc'
host_string = parsed_url.netloc
message_bytes = signed_data(host_string, data_string)

print('Address:', address)
print('Public key:', pub_key)
print('Signed Data:', message_bytes)
print('Real signature:', signature)
print('Verified:', verify(pub_key, signature, message_bytes))
print('Address verified:', verifyAddress(pub_key, address))

fake_signature = '29qWReHU9RXrQdQyXVXVciZarWXu7DXwekyV1zPivkrAzf4VSHb2Aq2FCKgRkKSozHFknKeq99dQaSmkhUDtZWsw'

print('Fake signature:', fake_signature)
print('Fake signature verification:', verify(pub_key, fake_signature, message_bytes))
```
