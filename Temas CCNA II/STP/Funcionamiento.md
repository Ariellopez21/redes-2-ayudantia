## Algoritmo ST

El algoritmo de árbol de expansión crea una topología sin bucles al seleccionar un único puente raíz (``root``) donde todos los demás switches determinan una única ruta de menor costo.

### Situación

> [!example] Topología de ejemplo
> ![[Pasted image 20250909075726.png|800|center]]
> - Se cuenta con esta topología de ejemplo.

### Root bridge

> [!example] Topología con root bridge
> ![[Pasted image 20250909080801.png|800|center]]


El **puente raíz** (_root bridge_) es el switch que actúa como **referencia central** dentro de una red con STP. Todos los demás switches calculan la mejor ruta (*la de menor costo*) para llegar a él.  
El costo de la ruta se determina considerando parámetros como el **tipo de enlace y el ancho de banda**.

Como resultado de este proceso, algunos enlaces quedan en estado de **bloqueo** $\varnothing$, evitando la formación de bucles. De esta forma, STP garantiza que exista **una única ruta lógica** entre todos los destinos de la red, bloqueando de manera intencional las rutas redundantes que podrían generar problemas.

### Topología sin bucles

> [!example] Topología sin bucles
> ![[Pasted image 20250909080736.png|800|center]]


Un **puerto bloqueado** convierte el enlace en una conexión que no reenvía tráfico entre dos switches. Esto genera una topología en la que **cada switch tiene una sola ruta hacia el puente raíz**, asemejándose a las ramas de un árbol que convergen hacia su raíz.

### Fallos y recálculos

Las rutas físicas aún existen para proporcionar la redundancia, pero las mismas se deshabilitan para evitar que se generen bucles.

Si una **ruta falla**, STP vuelve a **calcular las rutas** y **desbloquea los puertos** necesarios para permitir que la **ruta redundante** se active. Los recálculos STP también pueden ocurrir cada vez que se agrega un **nuevo switch** o un **nuevo vínculo** entre switches a la red.

## Paso a paso del STP

Proceso de 4 pasos:

1. Elige el puente raíz.
2. Seleccione los root ports.
3. Elegir puertos designados.
4. Seleccione puertos alternativos (bloqueados).

### Datos en consideración

Para los 4 pasos anteriores, se debe considerar la siguiente serie de datos con los que se determinan cada uno de los puertos.

#### BPDU

> [!NOTE] BPDU
> Unidades de datos de protocolo de puente o Bridge Protocol Data Unit

Los conmutadores utilizan BPDU para compartir información sobre sí mismos y sus conexiones, estas son usan para:

- elegir el root bridge
- Los root ports
- Los puertos designados
- Los puertos alternativos

> [!important] Las BPDU contienen el costo de la ruta raíz.

#### BID

> [!NOTE] BID
> Bridge ID, este identifica qué switch envió la BPDU.

El BID **participa** en la toma de muchas de las **decisiones** STA, incluidos los **roles** de puertos y root bridge. 

El BID contiene un **valor de prioridad**, la dirección **MAC** del switch  y un **ID** de sistema extendido. *El valor de BID más bajo lo determina la combinación de estos tres campos*.

#### Bridge priority

> [!NOTE] Bridge Priority
> - El valor de prioridad **predeterminado** para todos los switches Cisco es el valor decimal **32768**. El *rango va de 0 a 61440* y *aumenta de a 4096*. **Es preferible una prioridad de puente más baja**.
> - La **prioridad** de puente **0** **prevalece** sobre el resto de las prioridades de puente.

#### ID de sistema extendido

El **ID del sistema extendido** es un valor decimal agregado a la **prioridad del puente** dentro del **Bridge ID (BID)**, con el fin de identificar la **VLAN** en la BPDU.  

Gracias a este campo, STP puede operar de manera independiente por VLAN, permitiendo que diferentes VLAN tengan distintos **root bridge** y, por tanto, diferentes árboles de expansión. Esto hace posible que enlaces bloqueados para una VLAN puedan ser utilizados por otra.

##### Nota histórica

En las primeras implementaciones de **IEEE 802.1D**, las redes no utilizaban VLAN, por lo que existía un **único árbol de expansión común** para todos los switches. 

> [!warning] En esas versiones iniciales, el **ID del sistema extendido no se incluía** en las BPDU.

Cuando las VLAN comenzaron a utilizarse para segmentar la red, el estándar se actualizó para incluir el campo de **sistema extendido ID**. Esto también permitió que evoluciones posteriores, como **Rapid STP (RSTP)**, aprovecharan esta capacidad para administrar múltiples instancias de STP según las VLAN.

#### Dirección MAC

Cuando dos switches están configurados con la **misma prioridad** y tienen la **misma ID** de sistema extendido, el switch que posee la **dirección MAC** con el **menor valor**, expresado en hexadecimal, tendrá el **menor BID**.

### Paso 1: Root Bridge

- Se designa un único root bridge entre toda la red de switches del dominio de difusión.
- El root bridge se usa como referencia para todos los cálculos de rutas.
- Los switches intercambian BPDU para crear la topología sin bucles comenzando con el root bridge.

#### Proceso de elección

- Todos los switches del dominio de difusión participan para ser el root bridge.
- Cuando un switch es encendido, comienza a enviar BPDU por defecto cada 2 segundos.
- Las BPDU se envían en el dominio de difusión (broadcast) y contiene el [[#BID]] con sus respectivos campos.
- Las tramas enviadas con BPDU contienen el BID del switch de envío y el BID del root bridge; Sí el switch no ha enviado una trama con anterioridad, ambas BID son la misma, debido a que no ha podido compararla con ningún otro switch.
- **El switch que tiene el BID más bajo se convierte en el root bridge**.

> [!info] El BID del root bridge es comocido como Root ID

> [!important] Recomendación
> Cuando se tiene puesto el ojo en un switch para que ese sea el **root bridge**, se recomienda cambiarle el [[#Bridge priority]] para que sea el menor y sea **elegido**.

#### Costo de la ruta

Una vez elegido el root bridge, todos los switches están de acuerdo con la elección y comienza a determinar el menor de ruta hacía el root bridge.

> [!info] Recuerda
> Los switches no pueden estar de acuerdo con la elección del root bridge sí un puerto se cae, se agrega un nuevo puerto, se agrega un nuevo switcc, se quita un switch, o bien ocurra cualquier tipo de acontecimiento que altere las rutas determinadas por el STP.

 El **costo interno de la ruta raíz**, está determinada por la suma de todos los costos de los puertos individuales a lo largo de la ruta desde el conmutador hasta el puente raíz.

El costo de la ruta está incluido en el [[#BPDU]].

El costo de un puerto está determinado por la siguiente tabla:

| Velocidad de enlace | STP Cost: IEEE 802.1D-1998 | Costo de RSTP: IEEE 802.1w-2004 |
| ------------------- | -------------------------- | ------------------------------- |
| 10 Gbps             | 2                          | 2000                            |
| 1 Gbps              | 4                          | 20000                           |
| 100 Mbps            | 19                         | 200000                          |
| 10 Mbps             | 100                        | 2000000                         |

- IEEE 802.1D: Costo de ruta corta.
- IEEE-802.1w: Costo de ruta larga.

Se sugiere que para enlaces > 10Gbps se utilice el costo de ruta larga, pero de forma predeterminada se usa el costo de ruta corta.

El hecho de que los costos de ruta estén determinados por la velocidad del enlace, da lugar a que el administrador manipule la red como quiera para determinar qué camino es el que quiere que sigan los switches hasta llegar al root bridge.

### Paso 2: Root ports

Cada switch que no sea root bridge elegirá un root port, el puerto más cercano al root bridge en términos de costo ([[#Costo de la ruta]]).

### Paso 3: designed ports

- En **cada enlace entre dos switches**, uno de los puertos será marcado como **designado**.
- El **puerto designado** es el que tiene el **menor costo acumulado hacia el root bridge**.
- En otras palabras: si en un enlace Switch A ↔ Switch B, A tiene mejor camino al root bridge, entonces el puerto de A será el designado para ese segmento.

### Paso 4: alternative port

- Los puertos que **no resultan elegidos** ni como raíz ni como designados pasan a estar en estado de **bloqueo**.
- Los puertos alternativos también se llaman puertos bloqueados o de copia de seguridad.

### Resultado final

- Cada switch (excepto el root bridge) tendrá **un puerto raíz activo**.
- Cada segmento tendrá **un puerto designado activo**.
- Los demás puertos quedan bloqueados.

## STP para etherchannel

Para adelantar contenidos, tenemos el siguiente ejemplo:

> [!example] Ejemplo de enlace con caminos iguales
> ![[Pasted image 20250909095643.png|800|center]]

En este ejemplo, tenemos la conexión entre dos switches conectados a través de 2 enlaces.

S1 siendo el root bridge tiene los puertos F0/1 y F0/2, que están directamente conectados al si mismo, por lo tanto, su prioridad es 0, entonces, ambos son puertos designados.

S4 debe tener 1 root port y el otro puerto debe ser un puerto bloqueado.

En este caso, tenemos que el BID del root bridge es el mismo para ambos enlaces. (F0/1 - F0/6 y F0/2 - F0/5), la prioridad de puerto es la misma (128) y la dirección MAC del dispositivo es la misma en ambos puertos. Por lo tanto quedamos en un empate.

¿Qué ocurre aquí?

Se utiliza como último recurso el ID del puerto en uso, en este caso, los F0/1 y F0/2; Cómo F0/1 es menor, este dejará al enlace como port designed - root port, dejando al enlace del F0/2 como port designed - port alternative.

> [!example] ¡Solución!
> ![[Pasted image 20250909100448.png|800|center]]

## Temporizador y estados

### Temporizadores de STP

> [!info] Estados STP
> ![[Pasted image 20250909100839.png|800|center]]
> - Los temporizador se basan en todos estos estados para realizar la convergencia STP.

1. **Hello Timer (Temporizador de saludo)**
    
    - Intervalo con el que el _root bridge_ envía BPDUs.
    - **Valor por defecto:** 2 segundos.        
    - **Rango configurable:** 1 – 10 segundos.

2. **Forward Delay (Temporizador de retardo de reenvío)**
    
    - Tiempo que un puerto pasa en los estados de **Listening** y **Learning** antes de llegar a **Forwarding**.
    - **Valor por defecto:** 15 segundos.
    - **Rango configurable:** 4 – 30 segundos.

3. **Max Age (Temporizador de antigüedad máxima)**
    
    - Tiempo máximo que un switch espera sin recibir BPDUs antes de considerar que hubo un cambio de topología.        
    - **Valor por defecto:** 20 segundos.
    - **Rango configurable:** 6 – 40 segundos.

### Estados

| Estado del puerto | Descripción |
|-------------------|-------------|
| Bloqueo           | El puerto es alternativo y no reenvía tramas. Solo recibe BPDUs para determinar la ubicación del root bridge y los roles de puerto. Si no recibe BPDUs en 20 s (Max Age), entra en bloqueo. |
| Escucha           | Tras bloqueo, el puerto pasa a escucha. Procesa y envía BPDUs, pero aún no reenvía tráfico de usuario. Se prepara para participar en la topología. |
| Aprendizaje       | Después de escucha. Procesa BPDUs, empieza a llenar la tabla MAC, pero todavía no reenvía tráfico de usuario. |
| Reenvío           | El puerto ya reenvía tráfico de usuario y sigue enviando/recibiendo BPDUs. Es parte activa de la topología. |
| Deshabilitado     | No participa en STP ni reenvía tráfico. Se configura manualmente por administración. |
En resumen:

- **Bloqueo** → Solo escucha BPDUs, no reenvía tráfico.
- **Escucha** → Recibe y envía BPDUs, pero no reenvía tráfico de usuario.
- **Aprendizaje** → Llena la tabla MAC, pero aún no reenvía tráfico de usuario.
- **Reenvío** → Reenvía tráfico de usuario y participa activamente en STP.
- **Deshabilitado** → Estado administrativo, sin participación en STP ni reenvío.

| Estado del puerto | BPDU                  | Tabla de direcciones MAC   | Reenvío de frames de datos |
|-------------------|-----------------------|----------------------------|----------------------------|
| Bloqueo           | Recibir solo          | No hay actualización       | No                         |
| Escucha           | Recibir y enviar      | No hay actualización       | No                         |
| Aprendizaje       | Recibir y enviar      | Actualización de la tabla  | No                         |
| Reenvío           | Recibir y enviar      | Actualización de la tabla  | Sí                         |
| Deshabilitado     | No se ha enviado ni recibido | No hay actualización | No                         |
