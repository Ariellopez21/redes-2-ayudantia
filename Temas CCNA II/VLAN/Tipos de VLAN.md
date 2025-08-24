### VLAN Predeterminada

Corresponde a la VLAN 1.

Todos los puertos del switch están configurados acá, a menos que se configure explícitamente para estar en otra VLAN. Esto significa que las VLAN [[#VLAN Nativa|Nativa]] y [[#VLAN de Administración|de Administración]] también están de forma predeterminada en la VLAN 1.

> [!info] Recomendación de seguridad
> Cambiar la VLAN de administración y la nativa, y no usarlas para tráfico de usuarios.

### VLAN de Datos

Son las VLAN configuradas para separar el tráfico que realizan los usuarios.

Las VLAN de datos son las que dividen la red en grupos de usuarios o dispositivos (Ej, VLAN 20 - Estudiantes, VLAN 30 - Profesores, etc...)

> [!NOTE] Tenga en cuenta que... 
> **No** se debe permitir el tráfico de **administración de voz y red** en las VLAN de datos.
### VLAN Nativa

- Se usa **únicamente en enlaces troncales (trunks)**, no en puertos de acceso.

¡[[Enlaces Troncales|Clic aquí para ver Enlaces Troncales]]!

- La VLAN nativa sirve para transportar tráfico **sin etiquetar (untagged)** en un enlace troncal.
- Por defecto, en los switches Cisco, la VLAN nativa es la **VLAN 1**.
- Ejemplo: si un switch recibe un frame en un puerto trunk **sin etiqueta 802.1Q**, lo asigna automáticamente a la VLAN nativa.

> [!warning] Problema de seguridad
> Si dejas la VLAN nativa como la 1, un atacante puede inyectar tráfico sin etiquetar y hacerlo pasar por la VLAN equivocada (**ataque de VLAN hopping**).
> Por eso se recomienda **cambiar la VLAN nativa a una VLAN no usada** y **no asignar hosts a ella**.

### VLAN de Administración

VLAN configurada para dedicarse al tráfico de administración, o sea, SSH, Telnet, HTTPS, HTTP, SNMP, etc.

> [!warning] Vulnerabilidad
> De forma predeterminada la VLAN de Administración es la VLAN 1 (VLAN Predeterminada).
### VLAN de Voz

VLAN exclusiva para el tráfico VoIP.

Necesidades:

- **Ancho de banda** garantizado para asegurar la calidad de la voz.
- **Prioridad** de la transmisión sobre los tipos de tráfico de la red.
- Capacidad para ser **enrutado en áreas congestionadas** de la red.
- Una **demora inferior** a 150 ms a través de la red.

> [!important] Un dato MUY importante sobre VLAN de Voz
> Un **puerto de acceso** puede pertenecer a **sólo una VLAN** a la vez. Sin embargo, un puerto también se puede asociar a una **VLAN de voz**. Por ejemplo, un puerto conectado a un teléfono IP y un dispositivo final se asociaría con dos VLAN: una para voz y otra para datos.
