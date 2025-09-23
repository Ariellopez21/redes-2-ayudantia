## Protocolos de negociación automática

Los EtherChannels se pueden formar por medio de una negociación con uno de dos protocolos: [[PAgP|Port Aggregation Protocol (PAgP)]] o [[LACP|Link Aggregation Control Protocol (LACP)]]. Estos protocolos permiten que los puertos con características similares formen un canal mediante una negociación dinámica con los switches adyacentes.

> [!tip] Se puede usar cualquiera.

En EtherChannel, es **obligatorio** que todos los puertos tengan la misma velocidad, la misma configuración de dúplex y la misma información de VLAN. Cualquier modificación de los puertos después de la creación del canal también modifica a los demás puertos del canal.

> [!NOTE] También es posible configurar un EtherChannel estático o incondicional sin PAgP o LACP.

![[PAgP]]

![[LACP]]



## Tabla resumen

Básicamente, esta tabla define lo que necesitas saber para configurar adecuadamente cualquiera de ambos protocolos para establecer EtherChannel.

| PAgP                  | LACP            |
| --------------------- | --------------- |
| desirable - desirable | active - active |
| desirable - auto      | active - pasive |