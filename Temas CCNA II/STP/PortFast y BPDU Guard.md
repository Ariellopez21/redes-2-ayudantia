Cuando un switch se enciende o un dispositivo se conecta, el puerto pasa por los estados de **Escucha** y **Aprendizaje**, tardando unos **30 segundos** antes de reenviar tráfico. Esto puede causar problemas con clientes **DHCP**, que no logran obtener dirección IP a tiempo.

**PortFast** soluciona esto: hace que los puertos de acceso pasen **directo a reenvío**, sin esperar los 30 segundos, permitiendo que los dispositivos (PC, impresoras, etc.) se conecten de inmediato.

> [!warning] PortFast solo se debe usar en **puertos de acceso** (dispositivos finales). Si se activa en un puerto conectado a otro switch, podría provocar un bucle.

Para evitar riesgos, se usa **BPDU Guard**, que **desactiva el puerto automáticamente** si detecta una BPDU, protegiendo la red de bucles.

> [!example] Ejemplo de uso BPDU Guard
> ![[Pasted image 20250909104532.png|800|center]]
> - **PortFast acelera la conexión** de equipos finales.  
> - **BPDU Guard protege** contra configuraciones peligrosas.
> - Significa que **PortFast** debe usarse entre dispositivos finales y un switch porque **elimina** el paso de las BPDU. Y para asegurarse de eso, se usa **BPDU Guard**, pues, si llegara a pasar una BPDU, el Guard lo detectaría, deshabilitando automáticamente el enlace, evitando bucles..
