# Tabla de direcciones MAC

Es la forma que tiene un Switch LAN para reenvíar tráfico.

Un Switch LAN reenvía tráfico basado en el **puerto de entrada** de la *trama* y la **dirección MAC** de destino de la misma *trama*.

Una *trama ethernet* con un **dirección MAC de destino** siempre llegará al mismo destino, independientemente del **puerto de entrada** que utilice.

> [!warning] Una trama Ethernet nunca se reenviará fuera del mismo puerto en el que se recibió.

> [!INFO] La tabla MAC se almacena en la Memoria de Contenido Direccionable (CAM), motivo por el que a veces se le llama tabla CAM a la anterior.

Es importante que noten que, cuando un switch **no posee una dirección MAC en la tabla**, realizará la *búsqueda* en cada **puerto de salida** para determinar en *cuál* está la **MAC del destino**.

Una vez que la *dirección MAC* se encuentra, se **guarda** en la tabla como un **destino** asegurado para que no tenga que volver a realizar la *búsqueda* interfaz por interfaz.

Esto se detalla a continuación en [[#Método de aprender y reenviar]].

## Método de aprender y reenviar

Tenemos un switch con **4 puertos** (Fa0/1, Fa0/2, Fa0/3 y Fa0/4).  
Actualmente la tabla de direcciones MAC del switch está **vacía**.

> [!NOTE] Switch de 4 puertos
> ![[Excalidraw/Módulo 2.md#^frame=wcDjLQMrRqDaem0hr4Z6u | 800 | center]]


### Paso 1

Supongamos que tenemos PC1 y PC2, donde PC1 se quiere comunicar con PC2.

> [!NOTE] Comunicación PC1 - PC2
> ![[Excalidraw/Módulo 2.md#^frame=2yOYL82qhGlMMQHfAeclP | center | 800]]

**PC1 (MAC: ``AB:CD:E1``)** envía una *trama Ethernet* hacia **PC2 (MAC: ``AB:CD:E2``)** por el **puerto Fa0/1**.
    
- El switch ve la **MAC de origen** `AB:CD:E1` y nota que viene de **Fa0/1**.
    
- Como esa MAC no está en la tabla, **la agrega**.

| MAC origen | Puerto Origen |
| ---------- | ------------- |
| AB:CD:E1   | fa0/1         |


> [!NOTE]  Comunicación PC1 - PC2, extendida
> ![[Excalidraw/Módulo 2.md#^frame=IDwanSL6Oag6naBBSevu5 | center | 800]]

### Paso 2

- El switch ahora revisa la **MAC de destino**: `AB:CD:E2`.
    
- Esa dirección no está en la tabla, así que el switch **no sabe por dónde enviarla**.
    
- Aplica **unidifusión desconocida**.

> [!NOTE] Unidifusión desconocida
> Envía la trama por **todos los puertos excepto por el origen (Fa0/1)** (es decir, la reenvía por Fa0/2, Fa0/3 y Fa0/4).

- La trama llega a **PC2** (Fa0/3), que responde con otra trama de vuelta a **PC1**.

> [!NOTE] Comunicación PC1 - PC2, respuesta
> ![[Excalidraw/Módulo 2.md#^frame=fqzgOIoTVFySCNsHD9DI3 | center | 800]]

- El switch recibe la respuesta proveniente de **Fa0/3**, ve la **MAC de origen** `AB:CD:E2` y **la agrega** a la tabla:

| MAC origen | Puerto Origen |
| ---------- | ------------- |
| AB:CD:E1   | fa0/1         |
| AB:CD:E2   | fa0/2         |
### Resultado

La próxima vez que **PC1** envíe algo a **PC2**, el switch revisa la tabla, ve que la MAC de destino `AB:CD:E2` está en **Fa0/3**, y envía la trama **directamente** por ese puerto (en lugar de inundar usando unidifusión desconocida).

Adicionalmente, las direcciones agregadas tienen un temporizador, digamos que la tabla se vería como algo así:

| MAC origen | Puerto Origen | Temporizador |
| ---------- | ------------- | ------------ |
| AB:CD:E1   | fa0/1         | 5s           |
| AB:CD:E2   | fa0/2         | 1s           |

La cual refresca la tabla con la última adición; [[#Temporizador|Clic aquí]] para ver directamente sobre el Temporizador.

> [!question] ¿Qué ocurriría si quisiera enviar una trama desde PC1 (fa0/1) a PC4 (fa0/4)?

 Paso 1

- El switch recibe la trama de **PC1** con origen `AB:CD:E1` por **Fa0/1**.
- Ya tiene esa MAC registrada, así que **solo actualiza el temporizador** de esa entrada (no agrega nada nuevo).

 Paso 2

- La MAC de destino `AB:CD:E4` **no está en la tabla**, así que el switch hace **unidifusión desconocida**: reenvía la trama por **todos los puertos excepto Fa0/1** (o sea, Fa0/2, Fa0/3 y Fa0/4).

 Respuesta de PC4

- Cuando PC4 responde, su trama llega al switch por **Fa0/4** con MAC de origen `AB:CD:E4`.
    
- El switch **aprende** esta nueva dirección y actualiza la tabla:

| MAC origen | Puerto Origen |
| ---------- | ------------- |
| AB:CD:E1   | fa0/1         |
| AB:CD:E2   | fa0/2         |
| AB:CD:E4   | fa0/4         |

#### Temporizador

El temporizador tiene un valor predeterminado pero se puede ajustar... Supongamos que son 60s.

Cuando un valor de la tabla llega a los 60s, o sea el **límite**, este valor se **borra** y deja el **espacio libre**, esto se hace para **evitar información obsoleta**.

Un ejemplo de la utilidad del temporizador: 

Imagina que un dispositivo (por ejemplo, un notebook) está conectado al **Fa0/9** y el switch lo aprende ahí.  
Pero después alguien desconecta ese notebook y la conecta en **Fa0/5**.

- Si el switch **no tuviera un temporizador**, seguiría pensando que esa MAC está en Fa0/9 y enviaría las tramas allí… pero allí ya no hay nada.
    
- El tráfico se perdería y habría retrasos hasta que el switch descubriera la ubicación correcta.
