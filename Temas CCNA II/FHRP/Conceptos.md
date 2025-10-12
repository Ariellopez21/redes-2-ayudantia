## Limitaciones del Gateway

Cuando se configura un Host con su dirección IPv4, máscara de subred, gateway predeterminado y DNS, todos pueden ser entregados **dinámicamente** por un **servidor DHCPv4** o pueden ser **manualmente configurados**.

Sin embargo, el **gateway predeterminado** siempre es una **única interfaz de salida** y no existe un sitio en el que escribir un respaldo dentro de la configuración.

Este problema implica que sí el gateway predeterminado falla, aunque se tenga conectado otro dispositivo que actúe como gateway de la subred, los hosts no accederán a él porque la configuración es manual.

> [!important] Esto no ocurre con IPv6
> Ya que los **mensajes ICMPv6 con RA** anuncian dinámicamente el gateway predeterminado.
> Sin embargo, **incluso en IPv6**, usar FHRP mejora la velocidad y confiabilidad del cambio de gateway cuando ocurre una falla.

> [!example] Ejemplo Pt. 1: Situación
> ![[Excalidraw/Módulo 9.excalidraw.md#^frame=sZFYUytg6GWtcAGbUq3w1|center]]

> [!example] Ejemplo Pt. 2: Problemática
> ![[Excalidraw/Módulo 9.excalidraw.md#^frame=8vjEx7yKzw22-I1-5IM_H|center]]

## Un router virtual

Para evitar que un único router sea punto de falla, se implementa un **router virtual**.  
Esto consiste en configurar **dos o más routers físicos** para que trabajen juntos y **simulen ser un solo router** ante los hosts de la red local.

- Los routers comparten **una misma dirección IP y MAC virtual**.
    
- Los hosts usan esa IP como **gateway predeterminado**.
    
- Cuando un host envía tráfico, lo hace hacia la **dirección MAC virtual**, pero el **router activo** es el que realmente reenvía los paquetes.
    
- Si el router activo falla, otro router del grupo asume automáticamente su rol.
    

Este proceso es gestionado por un **protocolo de redundancia** (FHRP), que decide:

- cuál router es el **activo** (el que reenvía tráfico),
    
- y cuándo un **router de respaldo** debe tomar el control.
    

Todo este cambio ocurre **sin que los hosts lo noten**, garantizando continuidad en la conexión.  
A esta capacidad de recuperación automática del gateway se le llama **redundancia de primer salto (First Hop Redundancy)**.

> [!example] Ejemplo Pt. 3: Solución
> ![[Excalidraw/Módulo 9.excalidraw.md#^frame=eMBJYKueBOj-KgjA0e-M0|center]]

## Funcionamiento

Cuando falla el **router activo**, el **protocolo de redundancia** hace que el **router de reserva** asuma el nuevo rol de router activo. A continuación, los pasos que se llevan a cabo cuando falla el router activo:

1. El **router de reserva** deja de recibir los **mensajes de saludo** del router de reenvío (el activo).
	
2. El router de reserva asume la función del **router de reenvío** (el nuevo activo).
	
3. Debido a que el nuevo router de reenvío asume tanto la dirección IPv4 como la dirección MAC del **router virtual**, los dispositivos host no perciben ninguna interrupción en el servicio.

