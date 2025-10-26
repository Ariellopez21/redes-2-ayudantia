## Ataques ARP

ARP: Address Resolution Protocol (Protocolo de resolución de direcciones)

Con ARP tenemos una dirección IP que está mapeada a una dirección MAC desconocida. **Esto se usa todo el tiempo**.

Un cliente podría enviar una respuesta ARP no solicitada que se conoce como **ARP gratuito**. Esto, es un broadcast donde tenemos una dirección IP específica que se asigna a una dirección MAC específica.

El problema está cuando alguien envía un ARP gratuito como transmisión, y otros dispositivos como hosts u otros switches van a almacenar esa dirección MAC y la combinación de direcciones IP en sus tablas ARP y tablas de direcciones MAC.

¿Por qué es un problema? Un actor de amenaza puede enviar un mensaje ARP gratuito con información falsificada dentro de ella. **Esto efectivamente permite que cualquier host afirme ser el propietario de cualquier combinación de direcciones IP y dirección MAC que deseen.**

A través de un ejemplo sencillo:

- Sí tengo un PC1 y un R1 pertenecientes a una subred, está claro que PC1 enviará datos a R1 cuando intente ir al gateway predeterminado.
- Pero recordemos que según el modelo OSI, antes de pasar por la capa 3, transmitimos datos en capa 2.
- Por lo tanto, un actor de amenaza puede posicionarse con un PC2: una dirección MAC falsificada y la misma dirección que el gateway predeterminado.
- Logrando que el mensaje enviado desde PC1 a R1 pase primero por PC2, luego, PC2 envía la información a R1 y R1 entenderá que debe devolver la información a la MAC falsificada de PC2 porque cree que la información proviene de allí (sin importar que posee el mismo ip address).
- El flujo consta de: PC1 -> PC2 -> R1 y luego R1 -> PC2 -> PC1. Provocando un ataque de man-in-the-middle

> [!info] [[ARP y suplantación|Mitigación ARP y suplantación]]
