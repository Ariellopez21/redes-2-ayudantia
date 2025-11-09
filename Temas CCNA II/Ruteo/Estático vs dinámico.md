## Cuánto usar cada uno

Estático:

- Ruta predeterminadas de reenvío de paquetes a un ISP.
- Rutas fuera de dominio de enrutamiento y no aprendidas por el protocolo dinámico en uso.
- Cuando el administrador de red desea definir cualquier ruta explícitamente.
- Para enrutamiento entre redes de código auxiliar.
- Redes pequeñas.
- Redes de prueba.

Dinámico:

- Redes grandes.
- Redes que poseen más de **unos pocos routers**.
- Cuando la red está constantemente cambiando de topología.
- Para mayor escalabilidad.

Tabla comparativa:

| **Característica**              | **Routing dinámico**                                                      | **Routing estático**                         |
| ------------------------------- | ------------------------------------------------------------------------- | -------------------------------------------- |
| Complejidad de la configuración | Independiente del tamaño de la red                                        | Aumentos en el tamaño de la red              |
| Cambios de topología            | Se adapta automáticamente a los cambios de topología                      | Se requiere intervención del administrador   |
| Escalabilidad                   | Adecuado para topologías complejas                                        | Adecuado para topologías simples             |
| Seguridad                       | La seguridad debe estar configurada                                       | La seguridad es inherente                    |
| Uso de recursos                 | Usa CPU, memoria, ancho de banda de enlaces                               | No se necesitan recursos adicionales         |
| Predictibilidad de Ruta         | La ruta depende de la topología y el protocolo de enrutamiento utilizados | Definido explícitamente por el administrador |

> [!example] Línea de tiempo de protocolos de ruteo dinámicos
> ![[Pasted image 20251108214023.png]]

Se utilizan los términos:

- Vector distancia
- Estado de enlace
- Vector ruta

Para referirse al tipo de algoritmo de **mejor ruta** que utiliza cada protocolo:

> [!example] Tabla de tipo algoritmo utilizado 
> ![[Pasted image 20251108214214.png]]