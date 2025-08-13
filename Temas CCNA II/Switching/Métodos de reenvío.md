# Métodos de reenvío

### Almacenamiento y reenvío de switching

- Este método toma una **decisión** de **reenvío** en una trama después de haber recibido la **trama completa**.
- Revisada para la detección de errores mediante un mecanismo matemático de verificación de errores conocido como Verificación por Redundancia Cíclica (Cyclic Redundancy Check, CRC).
- El intercambio por almacenamiento y envío es el método principal de switching LAN de Cisco.

#### Verificación de errores

- Después de recibir la **trama completa** en el **puerto de entrada**, el switch compara el valor de Secuencia de Verificación de Trama (Frame Check Sequence, FCS) en el último campo del datagrama con sus propios cálculos de FCS. 
- FCS es un proceso de **verificación de errores** que contribuye a **asegurar** que la trama **no contenga errores** *físicos* ni de *enlace de datos*. Si la trama no posee errores, el switch la reenvía. De lo contrario, se descartan las tramas.

#### Almacenamiento en búfer automático

- Proporciona la flexibilidad para admitir cualquier combinación de velocidades de Ethernet.
- Por ejemplo, manejar una **trama entrante** que viaja a un **puerto Ethernet** de *100 Mbps* que debe **enviarse** a una interfaz de *1 Gbps*, **requeriría** utilizar el método de almacenamiento y reenvío. 
- Ante cualquier **incompatibilidad** de las **velocidades** de los puertos de **entrada** y **salida**, el switch **almacena** la trama completa en un búfer, calcula la verificación de FCS, la reenvía al buffer del puerto de salida y después la envía.

> [!important] El método de switching de almacenamiento y reenvío elimina las tramas que no pasan la comprobación FCS. Por lo tanto, no reenvía tramas no válidas.

### Método de corte

- Este método **inicia el proceso** de **reenvío** una vez que se determinó la **dirección MAC** de **destino** de una **trama entrante** y se estableció el **puerto de salida**.

Como observaste en la nota *important* presente en la sección anterior [[#Almacenamiento en búfer automático]], el método de switching de almacenamiento y reenvío es muy seguro, gracias a la comprobación FCS.

Este método es más **rápido** pero menos **seguro** que el de almacenamiento y reenvío.  
En lugar de esperar a recibir la **trama completa**, el switch comienza a reenviarla tan pronto como lee los **primeros bytes**, suficientes para identificar la **dirección MAC de destino**.  
De esta manera, puede consultar la **tabla de direcciones MAC** y tomar una **decisión de reenvío** casi de inmediato, reduciendo la latencia.

La gran ventaja es su **baja latencia**, ideal para entornos donde la velocidad es prioritaria.  
La desventaja es que, al no verificar toda la trama antes de enviarla, puede reenviar datos **corruptos o con errores** sin detectarlos previamente.