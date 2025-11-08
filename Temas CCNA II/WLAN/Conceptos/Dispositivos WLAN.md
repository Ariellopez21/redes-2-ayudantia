## NIC inalámbrica

> [!NOTE] NIC Inalámbrica
> ![[Pasted image 20251101002117.png|900|center]]

Implementar tecnología inalámbrica requiere:

- Un transmisor de radio (en este caso la NIC).
- Un receptor de radio en la misma sintonía (un dispositivo final o uno de red como un router o un AP).

La NIC actúa tanto de transmisor como receptor.

Viene integrada o se puede conectar por USB.

## Router de Hogar Wireless


> [!NOTE] Router Potente con tres antenas
> ![[Pasted image 20251101002418.png]]

Un router se anuncia mediante su SSID (Service Set Identifier: Conjunto de servicios compartidos).

La mayoría de los routers Wireless actualmente entregan:

- QoS
- Alta velocidad
- Transmisión de video
- IPv6
- Puertos USB para conectar impresoras o notebooks.
- Utilidades de configuración

Además, se pueden comprar extensores de alcance Wifi para ampliar la conexión en los puntos muertos donde no puede llegar la señal Wi-Fi del módem.

## Access Point Wireless

La mejor solución para extender el internet inalámbrico es un AP.


> [!NOTE] Access Point Ubiquiti
> ![[Pasted image 20251101002942.png]]

### AP autónomo

Dispositivos independientes configurados mediante GUI o CLI.

Útil cuando se requiere únicamente de uno o dos. Situaciones de redes pequeñas o domésticas.

Cada AP es independiente de otro, sus configuraciones también y sí aumenta la demanda inalámbrica se requieren más AP porque no se sincronizan para optimizar la señal.

> [!NOTE] AP autónomo en acción
> ![[Pasted image 20251101003208.png]]

### AP basado en controladores

Se les denomina puntos de acceso lightweight (LAPs).

Usan el protocolo LWAPP (Lightweight Wireless Access Point Protocol) para comunicarse con el WLC (Wireless LAN Controller).

A medida que se agregan AP, son gestionados, configurados y administrados de manera automática por el WLC.

> [!NOTE] Funcionamiento y comunicación de AP basado en controladores
> ![[Pasted image 20251101003624.png]]
> - El WLC está conectado a varios puertos con el switch usando lo que se le llama **Grupo de Agregación de Enlaces** (LAG).
> - LAG proporciona redundancia y equilibrio de carga como etherchannel.
> - ¡No confundir con Etherchannel! Ya que LAG no es compatible con LACP ni PaGP.

## Antenas inalámbricas

### Onmidireccionales

> [!NOTE] Antenas inalámbricas onmidireccionales
> ![[Pasted image 20251101003909.png]]
> - Entrega cobertura 360°
> - Ideal para casas, oficinas abiertas, salas de conferencia y áreas exteriores.

### Direccionales

> [!NOTE] Antena inalámbrica direccional
> ![[Pasted image 20251101004002.png]]
> - Enfocan la señal de radio en una dirección.
> - Es una señal increíblemente superior en una dirección y débil en todas las demás.
> - Ejemplos como antenas Yagi o parabólicas.

### MIMO

> [!NOTE] Antenas inalámbricas MIMO
> ![[Pasted image 20251101004126.png]]
> - Entrada múltiple - Salida múltiple (MIMO).
> - Usa muchas antenas para aumentar el ancho de banda.
> - Se puede usar hasta 8 antenas para aumentar el rendimiento.
> - Disponible para IEEE 802.11n/ac/ax.

