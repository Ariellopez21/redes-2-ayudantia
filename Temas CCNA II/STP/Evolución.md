Algunos de los STP nuevos que surgieron a partir del original (**802.1d**) son:

- **PVST (Per-VLAN STP):** Ejecuta una instancia de STP por cada VLAN, permitiendo que cada VLAN tenga su propio root bridge y topología.
- **RSTP (Rapid STP):** Evolución de STP clásico que mantiene compatibilidad, pero logra una **convergencia mucho más rápida** al detectar y reaccionar a cambios en la red casi al instante.
- **MSTP (Multiple STP):** Permite **agrupar varias VLAN en una misma instancia STP**, reduciendo el consumo de recursos y simplificando la gestión en redes grandes.

Los estándares siguientes son los más importantes:

> [!NOTE] Estándar IEEE-802-1D-2004
> Los swithes y bridges que cumplen con el estándar utilizarán Rapid Spanning Tree Protocol (RSTP) en lugar del protocolo STP anterior especificado en el estándar **802.1d**.

> [!NOTE] 802.1d
> Hablamos de este estándar como el que se explicó a lo largo de todo el módulo.

> [!NOTE] 802.1w
> Este estándar es el incorporado en **IEEE-802-1D-2004** para trabajar con RSTP.

### Tabla de STPs

| Variedad STP      | Explicación simplificada                                                                                                                                      |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **STP** (802.1D)  | Versión original del estándar. Crea un solo árbol de expansión para toda la red, sin importar cuántas VLAN existan.                                           |
| **PVST+**         | Mejora de Cisco. Crea un árbol de expansión separado para cada VLAN, lo que permite usar mejor los enlaces redundantes.                                       |
| **802.1D-2004**   | Versión actualizada del estándar STP, que incorpora mejoras del IEEE 802.1w.                                                                                  |
| **RSTP** (802.1w) | “Rapid STP”. Es una evolución de STP que logra convergencia más rápida cuando cambia la topología.                                                            |
| **PVST+ rápido**  | Versión de Cisco que combina RSTP con PVST+. Crea un árbol por VLAN pero con convergencia más rápida que PVST+ normal.                                        |
| **MSTP** (802.1s) | “Multiple Spanning Tree”. Estándar IEEE que permite agrupar varias VLAN en una misma instancia de árbol de expansión, reduciendo la cantidad de procesos STP. |
| **Instancia MST** | Implementación de Cisco de MSTP. Permite hasta 16 instancias de RSTP y combina muchas VLAN en topologías comunes para ahorrar recursos.                       |

## RSTP

- Es la **evolución de STP (802.1D)**, pero mantiene la misma lógica y compatibilidad.
- Usa el mismo algoritmo y parámetros básicos, por lo que es fácil de configurar si ya conoces STP.
- **Principal ventaja:** la **convergencia es mucho más rápida**, pasando de decenas de segundos en STP a solo **milisegundos** en una red bien configurada.    
- Los puertos alternativos o de respaldo pueden activarse de inmediato sin esperar todo el proceso de STP.

👉 **Cisco Rapid PVST+**: implementación de Cisco que aplica RSTP por VLAN, creando una instancia independiente para cada una.

### Comparación

Entre todo lo que aprendimos de STP vimos:

- [[#Algoritmo ST]]
- [[#Datos en consideración|Datos relevantes para el algoritmo]]
- [[#Temporizador y estados]]

> [!NOTE] Comparación STP vs RSTP: Estados de puertos
> ![[Pasted image 20250909103333.png|800|center]]
> - En este último, vimos los [[#Estados]] para la convergencia, este es mucho más simple, pues reduce tres estados a uno solo.


> [!NOTE] Comparación STP vs RSTP: Tipo de puerto
> ![[Pasted image 20250909103714.png|800|center]]
> - Otro cambio importante, es que cuando vimos STP, asumimos que el puerto alternativo era llamado de esa forma o como sinónimo: puerto bloqueado. Dicho puerto funcionaba como una copia de seguridad y no permitía que fluyan tramas por su enlace.
> - RSTP pasa del concepto a la implementación y directamente crea un tipo de puerto **Backup Port** y otro tipo de puerto **Alternative Port** que realizan las acciones antes mencionadas por separado.


> [!NOTE] RSTP: Uso del Backup Port
> ![[Pasted image 20250909104042.png|800|center]]
> - El **Backup port** es una copia de seguridad en un medio compartido, como un hub.
