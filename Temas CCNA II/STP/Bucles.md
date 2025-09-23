## Problemas de un bucle

- Inestabilidad en la tabla de direcciones MAC.
- Saturación de enlaces
- Alta utilización de CPU (en Switches y dispositivos finales)

Como resultado, la red se vuelve inutilizable.

> [!NOTE] Diferencia entre eliminación de tramas y eliminación de paquetes
> - En la *capa 3* (IPv4/IPv6), los *paquetes* no circulan indefinidamente porque el **TTL o límite de saltos** se va reduciendo hasta llegar a 0 y el router los descarta.  
> - En cambio, en la *capa 2* (Ethernet), los switches no tienen un mecanismo así: una *trama* puede quedarse en bucle sin fin.  
> - Por eso se creó **STP (Spanning Tree Protocol)**, que evita los bucles en redes Ethernet. 


> [!example] Ejemplo con ARP
> Las tramas de difusión, como una solicitud ARP, se reenvían a todos los puertos del conmutador, excepto el puerto de entrada original. Esto asegura que todos los dispositivos en un dominio de difusión reciban la trama. Si hay más de una ruta para reenviar la trama, se puede formar un bucle infinito.

En una red con bucles, la **tabla MAC del switch se vuelve inestable** porque cambia constantemente con las tramas de difusión. Esto genera un alto uso de CPU y puede impedir que el switch reenvíe tramas.

No solo las tramas de difusión son afectadas:

- Las **tramas de unidifusión desconocidas** (cuando el switch no conoce la MAC de destino y reenvía por todos los puertos excepto el de entrada) también provocan problemas, ya que pueden llegar **duplicadas** al dispositivo de destino.

### Tormenta de difusión

Una **broadcast storm** ocurre cuando hay un exceso de tramas de difusión en la red en un corto período de tiempo.  
Esto puede **colapsar la red en segundos**, ya que satura tanto a los switches como a los dispositivos finales.

**Causas principales:**

- **Bucle de Capa 2** (cuando no hay control de redundancia con STP).
    
- **Problemas de hardware**, como una tarjeta de red (NIC) defectuosa que genera tramas de difusión sin control.
