
Crear la siguiente red:

> [!NOTE] Topología EtherChannel
> ![[Excalidraw/Módulo 6.md#^frame=k11oAPpuhaKRnGDFFGda1|center|800]]

## Condiciones

- Cada enlace etherchannel debe estar compuesto de 4 puertos físicos.

> [!example] Ejemplo
> Fa0/1 - Fa0/4 = Po1

- Tal como se observa en la figura, dos de los port-channel deben estar configurados con PAgP y los otros dos con LACP.

## Verificación

- Al usar `show etherchannel summary` debería verse todos los puertos en uso por cada Po (Cada switch debería tener solo 2 Po).
- Dentro del mismo comando anterior se puede ver el modo de negociación de cada puerto.
- Hacer ping entre todos los equipos conectados.

