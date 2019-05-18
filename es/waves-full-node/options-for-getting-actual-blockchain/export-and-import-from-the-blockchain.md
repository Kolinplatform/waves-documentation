#  Exportar e Importar desde el Blockchain

**Nota:** Esta funcionalidad está disponible desde la versión 0.8.

## Exportar bloques existentes a un archivo binario {#user-content-export-existing-blocks-to-a-binary-file}

**Nota:** Debe detener el nodo antes de iniciar la exportación de bloques.

Para exportar el blockchain existente al archivo binario ejecute el siguiente comando. La exportación es una operación bastante rápida, pero el archivo binario resultante también puede llevar hasta 1/3 del tamaño de la carpeta `data` en el disco.

En Windows:

```
java -cp waves-all-<version>.jar com.wavesplatform.Exporter [nombre-archivo-configuracion] [nombre-archivo-salida] [altura(height)]
```

En Linux:

```
Mainnet: sudo -u waves exporter /etc/waves/waves.conf [nombre-archivo-salida] [altura(height)]
Testnet: sudo -u waves-testnet exporter-testnet /etc/waves-testnet/waves.conf [nombre-archivo-salida] [altura(height)]
```


Si el parámetro `altura(height)` no fue dado, todos los bloques serán exportados. De lo contrario, solo se exportarán al archivo de salida los bloques hasta la altura.

El parámetro de nombre de archivo de salida es opcional, el nombre 'blockchain' se usa por defecto. Como resultado, un archivo llamado '&lt;nombre-archivo-salida&gt;-&lt;height&gt;' Se creará en la carpeta actual.

## Eliminar los datos del nodo existente

Para reconstruir completamente el estado del nodo, debe eliminar la carpeta `data` del nodo existente.  
En Windows, la carpeta `data` normalmente se encuentra en `%HOMEPATH%\waves\data`.

En Linux está en la carpeta `/var/lib/waves[-testnet]/` folder:

```
sudo rm -rdf /var/lib/waves[-testnet]/data
```

## Importar bloques del archivo binario {#user-content-import-blocks-from-the-binary-file}

**Nota:** El nodo debe detenerse antes de importar el blockchain.

**Nota:** Si ya tiene algunos datos en la carpeta `data` del nodo, la importación continuará agregando datos nuevos del archivo binario de la cadena de bloques. Por lo tanto, podría estar dispuesto a eliminar los datos existentes. Tenga cuidado al agregar datos, la mezcla de datos de diferentes versiones puede llevar a un estado erróneo.

Para importar la cadena de bloques y reconstruir el estado, ejecute el siguiente comando.

En Windows:

```
java -cp waves-all-<version>.jar com.wavesplatform.Importer [configuration-file-name] [binary-file-name]
```

En Linux:

```
Mainnet: sudo -u waves importer /etc/waves/waves.conf [binary-file-name]
Testnet: sudo -u waves-testnet importer-testnet /etc/waves-testnet/waves.conf [binary-file-name]
```

La importación es una operación pesada y puede tardar unas horas en completarse.

## Descargando Blockchain exportado

Puedes descargar blockchains exportados recientemente usando los siguientes enlaces:

* TestNet: [http://blockchain.testnet.wavesnodes.com/](http://blockchain.testnet.wavesnodes.com/)
* MainNet: [http://blockchain.wavesnodes.com/](http://blockchain.wavesnodes.com/)



