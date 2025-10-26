## Ataques STP

Los actores de amenaza usan **lógica no basada en conexiones físicas** pero que harían que su host apareciera como un root bridge.

Los actores de amenaza usan su host como switch y envían BPDU con una prioridad increíblemente baja (por ejemplo 0).

Esto provoca que el Spanning Tree ponga como root bridge al actor de amenaza, consiguiendo que todos los mensajes pasen por el root bridge, consiguiendo un ataque de man-in-the-middle.

> [!info] [[Temas CCNA II/Seguridad LAN/Mitigación Ataques/STP|Mitigación STP]]