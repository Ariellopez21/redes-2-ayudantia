## 14.1.1 Dos funciones del router

Primero, dejar claro:
- **Un switch** une dispositivos dentro de **la misma red** Ethernet.
- **Un router** conecta **redes diferentes**: tiene **varias interfaces**, cada una en una red IP distinta.

Entonces, las funciones de un router constan del **proceso al recibir un paquete IP:**
1. El router **consulta su tabla de enrutamiento** para decidir **la mejor ruta** hacia la red destino (esto es **enrutamiento**).
2. Con esa decisión, **elige la interfaz de salida** adecuada y **reen­vía el paquete** (esto es **reenvío/forwarding**).

> [!example] Tabla de enrutamiento de un router.
> ![[Pasted image 20251108204653.png]]


Notas clave:

- La **interfaz de salida** puede llevar directamente al **host final** o a **otro router** camino al destino.
- **Cada red** que conecta el router **requiere su propia interfaz**.

## Mejor ruta = coincidencia más larga

Cuando un router recibe un paquete, busca en su **tabla de enrutamiento** la ruta que **más se parezca** a la dirección IP de destino.  
Esa “parecida” se mide en **cuántos bits iniciales (de izquierda a derecha)** coinciden entre la IP destino y las redes guardadas en la tabla.

👉 Cuantos **más bits coincidan**, más específica es la ruta → **mejor coincidencia**.  
👉 Esa es la ruta que el router elige para enviar el paquete.

**Ejemplo:**

- IP destino: `192.168.1.45`
- Rutas en la tabla:
    - `192.168.0.0/16` → coincide en 16 bits
    - `192.168.1.0/24` → coincide en 24 bits ✅ (más larga → se elige esta)

> [!example] Otro ejemplo, modo CISCO
> ![[Pasted image 20251108204933.png]]

> [!example] Otro ejemplo, modo CISCO IPv6
> ![[Pasted image 20251108205006.png]]

## Creación de tabla de enrutamiento

> [!example] Red de ejemplo para R1
> ![[Pasted image 20251108205235.png]]

Su tabla de enrutamiento consta de:

- Directamente conectados (Agregadas por interfaz): $10.0.1.0/24,\;10.0.2.0/24,\;10.0.3.0/24$.
- Remotas (Agregadas por enrutamiento dinámico o estático): Todas las demás.
- Predeterminada (salida de último recurso): A través de $S^{*}=0.0.0.0$. Puede ser dirigida al router **ISP**.