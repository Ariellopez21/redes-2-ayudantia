
> [!example] Ambas funcionalidades de un router, con énfasis en **proceso de reenvío**
> ![[Pasted image 20251108205936.png]]
> - **Si el destino está en una red conectada directamente**:
>     - El router **envía el paquete directo al dispositivo** final.
>     - Para ello necesita saber la **dirección MAC** asociada a la IP destino:
>         - **IPv4:** usa el **protocolo ARP**, que pregunta _“¿quién tiene esta IP?”_ y el dispositivo responde con su MAC.
>         - **IPv6:** usa **ICMPv6 Neighbor Solicitation (NS)**, que cumple el mismo rol que ARP: descubre la MAC asociada a una IP.
>     - Una vez conocida, el router **encapsula el paquete en una trama Ethernet** y lo reenvía.
> - **Si el destino está en una red remota**
>     - El router **envía el paquete a otro router (siguiente salto)**, según la ruta indicada en su tabla.
>     - El proceso para encontrar la MAC es igual (ARP o ICMPv6 NS), pero en este caso busca la dirección del **router siguiente**, no del destino final.
> - **Si no hay coincidencia en la tabla de enrutamiento**
>     - Si no existe una ruta hacia la red destino ni una ruta predeterminada (`0.0.0.0/0`), **el router descarta el paquete**.

## Mecanismos de reenvío

- Switching de procesos
- Switching rápido
- Cisco Express Forwarding (CEF)

Resumen:

| Mecanismo                          | Cómo funciona                                                                                                                                                                                        | Dónde ocurre                                    | Rendimiento                | Estado actual                             |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- | -------------------------- | ----------------------------------------- |
| **Process Switching**              | **Cada paquete** sube a la CPU: busca ruta en la RIB (Router Information Base) y decide interfaz; repite para todos.                                                                                 | Plano de **control** (CPU)                      | **Lento**                  | Legado (evitarlo).                        |
| **Fast Switching**                 | **Primer paquete** va a CPU; se guarda una **entrada en caché** de siguiente salto. Los siguientes paquetes del **mismo flujo** usan esa caché.                                                      | Mixto: 1.º en control, resto en datos con caché | **Más rápido** que process | Legado (propenso a caché desactualizada). |
| **CEF (Cisco Express Forwarding)** | La CPU **precalcula** y mantiene una **FIB** (Forwarding Information Base) y **tabla de adyacencias** (MAC/encapsulado). **Todos** los paquetes se reenvían mirando esas tablas, sin subir a la CPU. | Plano de **datos** (construido por el control)  | **Más rápido y escalable** | **Por defecto** en routers Cisco y MLS.   |

### Switching de procesos

> [!example] Proceso visual
> ![[Pasted image 20251108210757.png]]

- Cada paquete sube a la CPU: consulta la RIB, decide interfaz y encapsulado.
- Se repite **paquete por paquete**, aunque sean del mismo flujo.
- Ocurre en el plano de **control**; muy **lento** y no escala.
- Hoy es legado; sólo útil para entender el funcionamiento base o para pruebas.

### Switching rápido

> [!example] Proceso visual
> ![[Pasted image 20251108210829.png]]

- El **primer paquete** va a CPU; se calcula el siguiente salto y se guarda en **caché**.
- Los siguientes paquetes **del mismo flujo** usan esa entrada sin pasar por la CPU.
- Más **rápido** que process, pero la caché puede quedar desactualizada.
- También legado; reemplazado por CEF en redes modernas.

### CEF

> [!example] Proceso visual
> ![[Pasted image 20251108210849.png]]

- La CPU **precalcula** y mantiene la **FIB** (rutas para reenvío) y **adyacencias** (encapsulado/MAC).
- **Todos** los paquetes se reenvían en el **plano de datos** consultando esas tablas.
- **Más rápido y escalable**, se actualiza con los cambios de topología.
- Es la opción **predeterminada** en routers Cisco y switches multicapa.