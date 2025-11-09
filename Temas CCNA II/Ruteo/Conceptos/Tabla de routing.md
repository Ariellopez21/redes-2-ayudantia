## Principios de la tabla de enrutamiento

| **Principios de la tabla de enrutamiento**                                                                                             | **Ejemplo**                                                                                                                                                                                                                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Cada router toma su decisión por sí solo, basándose en la información que tiene en su propia tabla de enrutamiento.                    | - R1 sólo puede reenviar paquetes utilizando su propia tabla de enrutamiento.- R1 no sabe qué rutas están en las tablas de enrutamiento de otros (por ejemplo, R2).                                                                                                           |
| La información de una tabla de enrutamiento de un enrutador no necesariamente coincide con la tabla de enrutamiento de otro enrutador. | Solo porque R1 tiene ruta en su tabla de enrutamiento a una red en el internet a través de R2, eso no significa que R2 sepa sobre eso mismo red.                                                                                                                              |
| La información de enrutamiento sobre una ruta no proporciona enrutamiento de retorno al secundario.                                    | R1 recibe un paquete con la dirección IP de destino de PC1 y la la dirección IP de origen de PC3. Solo porque R1 sabe reenviar el paquete fuera de su interfaz G0/0/0, no significa necesariamente que sepa cómo reenviar paquetes procedentes de PC1 a la red remota de PC3. |
## Enrutamiento dinámico en la tabla de enrutamiento

> [!example] Salida de un router usando dynamic routing
> ![[Pasted image 20251108211835.png]]

## Nota de la ruta predeterminada

Una ruta predeterminada tiene el mismo funcionamiento que la del **gateway predeteminado** de un Host.

Sí el dispositivo actual no sabe qué hacer con la dirección que tiene en sus manos, se la deja encargada al dispositivo predeterminado que tiene asignado como **último recurso**, en el mejor de los casos, él sabrá que hacer.

## Distancia administrativa

- Cuando **varias fuentes** (estática, OSPF, EIGRP, etc.) anuncian **el mismo prefijo**, el router elige **una sola** para instalar en la tabla.
- La elección se hace por **Distancia Administrativa (AD)** = “confianza” del origen. 
- **Menor AD = más confiable**.
- Si la AD es igual (misma fuente), se usa la **métrica** del protocolo; puede haber **ECMP** si empatan.

**AD típicas (menor → mayor confianza):**

- **Conectada** 0
- **Estática** 1
- **eBGP** 20
- **EIGRP interno** 90
- **OSPF** 110
- **RIP** 120

> [!example] Si OSPF (110) y EIGRP (90) conocen el mismo /24, **gana EIGRP** por tener **AD más baja**.
