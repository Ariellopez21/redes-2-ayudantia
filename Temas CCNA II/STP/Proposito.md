![[Redundancia]]

## Qué es STP

Spaning Tree Protocol o Protocolo de árbol de expansión es un protocolo de red de **prevención de bucles** que **permite redundancia** mientras crea una topología de **capa 2** sin bucles.

> [!NOTE] Operación
> ![[Pasted image 20250908204834.png|800|center]]
> - Su gracia está en que cuando tenemos una red redundante, evita que pasen paquetes por uno de los caminos para evitar bucles.


> [!NOTE] Recálculo
> ![[Pasted image 20250908204939.png|800|center]]
> - En la imagen anterior, donde se encontraba el simbolo $\varnothing$, correspondía al bloqueo generado por STP.
> - En esta imagen tenemos además el símbolo $\times$ que indica que dicho enlace troncal quedó fuera de uso.
> - STP posee un algoritmo de recálculo cada cierto periodo de tiempo y determina que el nuevo $\varnothing$ ocurrirá en el enlace que quedó con $\times$, y el anterior enlace bloqueado quedará disponible.
