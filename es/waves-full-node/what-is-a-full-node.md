# Waves Full Node

Esta seccion contiene toda la informacio para instalar, configurar y actualizar un Nodo Waves.

1. [Como instalar un Nodo](/waves-full-node/how-to-install-a-node/how-to-install-a-node.md)
2. [Opciones para obtener una Blockchain](/waves-full-node/options-for-getting-actual-blockchain.md)
3. [Estado de descarga y aplicación](/waves-full-node/options-for-getting-actual-blockchain/state-downloading-and-applying.md)
4. [Exportar e Importar desde la Blockchain](/waves-full-node/options-for-getting-actual-blockchain/export-and-import-from-the-blockchain.md)
5. [Actualizar](/waves-full-node/upgrading.md)
6. [Como revertir un Nodo](/waves-full-node/how-to-rollback-a-node.md)
7. [Nodo Waves en el Docker](/waves-full-node/waves-node-in-docker.md)
8. [Como configurar un Nodo](/waves-full-node/how-to-configure-a-node.md)
9. [Configuracion de inicio de sesion](/waves-full-node/logging-configuration.md)
10. [Unirse a la Testnet](/waves-full-node/joining-testnet.md)

# Estructura de la red Waves

La estructura de la red peer-to-peer afecta la seguridad y el rendimiento de las criptomonedas. Una red agrupada geográficamente puede propagar rápidamente un nuevo bloque a muchos otros nodos. Esto hace que sea más difícil para un minero malintencionado propagar bloques/transacciones en conflicto más rápido que los nodos honestos.

Sin embargo, una red menos agrupada puede significar que los nodos completos están siendo gestionados por una variedad más amplia de usuarios, lo que también es bueno para la descentralización.

Waves tiene una red peer-to-peer para difundir la información de bloques y transacciónes.

Cualquier computador corriendo un programa en la blockchain es considerado un nodo.

Waves también contiene nodos completos que permiten a cualquier persona participar en el proceso descentralizado de creación de bloques.

El nodo completo de Waves sirve dos roles críticos:

1. Retransmitir bloques y transacciones a los mineros.
2. Responder a las consultas de los usuarios finales sobre el estado de la cadena de bloques.

# La importancia de un nodo completo

El trabajo de un nodo completo es almacenar los datos de la cadena de bloques, pasarlos a otros nodos y asegurar que los bloques recién agregados sean válidos. La validación implica asegurarse de que el formato del bloque sea correcto, todos los hashes en el nuevo bloque se calcularon correctamente, el nuevo bloque contiene el hash del bloque anterior y cada transacción en el bloque es válida y está firmada por las partes correspondientes. Los nodos completos también pueden actuar como nodos mineros (es decir, generar nuevos bloques). El minero comprueba que cada transacción sea auto válidada, ya que los otros nodos rechazarán el bloque si incluyera transacciones no válidas.

Cualquier nodo puede proponer nuevas transacciones, y estas transacciones propuestas se propagan entre nodos hasta que finalmente se agregan a un bloque.

**Nota.** Puede encontrar una lista completa de nodos en [dev.pywaves.org](http://dev.pywaves.org/generators/) y [Here](https://wavesplatform.com/leasing#nodes) Puedes encontrar una lista de los principales nodos enlistados por su saldo de WAVES.

