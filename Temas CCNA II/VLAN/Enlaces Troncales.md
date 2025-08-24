Gracias a las **VLAN**, el tráfico en la red se optimiza porque cada puerto solo permite el paso del tráfico correspondiente a su VLAN asignada. Pero surge la pregunta: ¿cómo se comunican los switches entre sí si hay múltiples VLAN?

Aquí entran en juego los **enlaces troncales**. Un enlace troncal permite que varias VLAN viajen por un único puerto, lo que facilita la comunicación entre switches, así como entre switches y dispositivos de capa 3 (por ejemplo, routers o switches de capa 3).

Para configurar un puerto como troncal, se utiliza el protocolo **IEEE 802.1Q** (conocido también como _dot1q_). Este protocolo etiqueta los tramas Ethernet con el identificador de VLAN correspondiente, de manera que el dispositivo receptor sepa a qué VLAN pertenece cada trama.

Un enlace troncal no está asociado a una VLAN específica: actúa como un **conducto** que transporta múltiples VLAN de un dispositivo a otro.

Además de usarse entre switches y routers, los enlaces troncales también pueden establecerse entre un switch y un servidor u otro dispositivo que cuente con una tarjeta de red compatible con **802.1Q**.

#### Ejemplo de uso de enlaces troncales

> [!info] Importante
> Se utilizará la red de ejemplo en la sección [[Ventajas VLAN#Ejemplo de beneficios de una VLAN]] 


> [!info] Red con VLAN
> ![[Pasted image 20250822092058.png|800|center]]
> 🔹 Esta red posee dos **enlaces troncales**: uno conecta el switch S1 con S2 y otro conecta S1 con S3.  
> 🔹 Los enlaces troncales están configurados para transportar las VLAN 10, 20, 30 y 99. (La VLAN 99 suele usarse como **VLAN de administración**).  
> 🔹 Los **puertos de acceso**, como F0/11 y F0/18, están configurados para permitir **únicamente** el tráfico de **una VLAN específica** (VLAN 10 para PC1 y PC4, VLAN 20 para PC2 y PC5, y VLAN 30 para PC3 y PC6).  
> 🔹 Los enlaces troncales emplean **IEEE 802.1Q** (_dot1q_) para identificar a qué VLAN pertenece cada trama.
> 🔹 Es decir, un **puerto de acceso** se asigna a una sola VLAN, mientras que un **puerto troncal** puede transportar múltiples VLAN entre switches o hacia otros dispositivos compatibles.

#### Etiquetado 802.1Q

Cuando usamos un **enlace troncal** con **802.1Q**, normalmente **todas las tramas llevan una etiqueta** que indica a qué VLAN pertenecen.  

Pero existe una excepción: la **VLAN nativa**.

Recordemos lo que es la [[Tipos de VLAN#VLAN Nativa|VLAN Nativa]]:

- Es la VLAN a la que se asignan las **tramas que llegan sin etiqueta** a un puerto troncal.
- Por defecto, en Cisco la **VLAN nativa es la VLAN 1**, aunque por seguridad se suele cambiar.
- Se usa para ciertos tipos de tráfico que tradicionalmente no se etiquetan (como mensajes de control o administración entre switches).

##### Marcos etiquetados en la VLAN Nativa

- En Cisco, **el tráfico de la VLAN nativa nunca debería venir etiquetado**.

- Si un switch Cisco recibe una trama **etiquetada con el mismo ID de la VLAN nativa**, la descarta.    

> [!warning] Algunos dispositivos de otros fabricantes (teléfonos IP, routers, switches que no pertenezcan a Cisco) **sí pueden enviar etiquetas incluso para la VLAN nativa** → por eso hay que configurarlos correctamente para evitar problemas.

##### Marcos sin etiqueta en la VLAN Nativa

- Si un troncal recibe una trama **sin etiqueta**, automáticamente la asigna a la **VLAN nativa**.
- Si no hay puertos ni dispositivos en esa VLAN, el switch simplemente descarta la trama.
- Internamente, el switch asigna un valor llamado **PVID (Port VLAN ID)** que corresponde a la VLAN nativa.

Ejemplo: Sí configuras VLAN 50 como nativa → la PVID es 50. Lo que implica que todo tráfico sin etiqueta se envía a la VLAN 50; Si no configuras nada → PVID = VLAN 1.

A continuación, una tabla de cómo procede el tráfico con y sin etiqueta en un enlace troncal:

| VLAN   | Tráfico etiquetado                                                               | Tráfico no etiquetado                                                        |
| ------ | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| Nativa | Sí VLAN está etiquetada con `id` de la Nativa, **descarta**.                     | Sí el tráfico no está etiquetado, se envía con **normalidad** a VLAN Nativa. |
| Otra   | Sí VLAN está etiquetada con `id` diferente a Nativa, procede con **normalidad**. | No aplica: todo tráfico **sin etiqueta** siempre se manda a la VLAN nativa.  |

Con esto:

- La **única VLAN que puede recibir tráfico no etiquetado es la VLAN nativa**.
- Todo el tráfico etiquetado (excepto si coincide con la VLAN nativa) viaja sin problemas.
- Si una trama llega **etiquetada como nativa**, Cisco la descarta.

#### Etiquetado de VLAN de Voz

Se necesita una red VLAN de voz separada para admitir VoIP. Esto permite aplicar políticas de calidad de servicio (QoS) y seguridad al tráfico de voz.

Un host IP puede conectarse al teléfono IP para obtener conectividad de red también. Un puerto de acceso que conecta un teléfono IP de Cisco puede configurarse para utilizar dos VLAN separadas: Una VLAN es para el tráfico de voz y la otra es una VLAN de datos para admitir el tráfico de host.