
El alivio de la congestión de la red.

De manera predeterminada, los puertos de switch interconectados tratan de establecer un enlace en **dúplex completo** y por lo tanto se **eliminan los dominios de colisión**.


> [!NOTE] Nota sobre las conexiones duplex completo
> Aumentaron notablemente el rendimiento de las redes LAN y se requieren para velocidades de Ethernet de 1 Gb/s y superiores.

Los switches utilizan **tablas de direcciones MAC** para determinar los puertos de salida y pueden **reducir o eliminar por completo las colisiones**.

Otros métodos de aliviar la congestión:

- **Velocidad de puertos rápidos** (mayores a 1Gbps).
- **Cambio interno rápido**: los switches utilizan un bus interno rápido o memoria compartida para proporcionar un alto rendimiento.
- **Alta densidad de puertos**: Es decir un switch con más puertos, así, se reduce la cantidad de switches necesarios; Por ejemplo, si se necesitaran *96 puertos de acceso*, sería *menos costoso* comprar *dos switches de 48 puertos* en lugar de *cuatro switches de 24 puertos*.
- **Buffers de trama grande**: los switches utilizan búferes de memoria grande para almacenar temporalmente más tramas recibidas antes de tener que empezar a descartarlas. Esto permite que el tráfico de entrada desde un puerto más rápido (por ejemplo, 1 Gbps) se reenvíe a un puerto de salida más lento (por ejemplo, 100 Mbps) sin perder tramas.

Sobre este último punto, se puede determinar con otras palabras... Un **búfer de trama grande** es como un **estacionamiento temporal dentro del switch**.

- Imagina que tienes una **carretera rápida** (1 Gbps) que llega a una **calle más lenta** (100 Mbps).
- Los autos (paquetes de datos) llegan mucho más rápido de lo que pueden salir.
- Si no hubiera un estacionamiento, los autos empezarían a chocar o a perderse porque no hay dónde esperar.

El **búfer** es ese estacionamiento:

- Los autos entran y esperan ordenadamente hasta que haya espacio en la calle lenta para avanzar.
- Así, el switch **no pierde tramas** aunque la entrada sea mucho más rápida que la salida.
