Las VLAN de rango normal en estos switches se numeran del 1 al 1005, y las VLAN de rango extendido se numeran del 1006 al 4094.

### Rango Normal VLANs

Las siguientes son las características de las VLAN de rango normal:

- Se utiliza en redes de pequeños y medianos negocios y empresas.
- Se identifica mediante una ID de VLAN entre 1 y 1005.
- Las ID de 1002 a 1005 se reservan para las VLAN de Token Ring e interfaz de datos distribuidos por fibra óptica (FDDI).
- Las ID 1 y 1002 a 1005 se crean automáticamente y no se pueden eliminar.
- Las configuraciones se almacenan en un archivo de base de datos de VLAN llamado vlan.dat, que se guarda en la memoria flash.
- Cuando se configura, el protocolo de enlace troncal VLAN (VTP) ayuda a sincronizar la base de datos VLAN entre conmutadores.

### Rango Extendido VLANs

Las siguientes son las características de las VLAN de rango extendido:

Los proveedores de servicios los* utilizan para dar servicio a varios clientes y por las empresas globales lo suficientemente grandes como para necesitar identificadores de VLAN de rango extendido.

- Se identifican mediante una ID de VLAN entre 1006 y 4094.
- Las configuraciones se guardan en el archivo de configuración en ejecución.
- Admiten menos características de VLAN que las VLAN de rango normal.
- Requiere la configuración del modo transparente VTP para admitir VLAN de rango extendido.

**Nota:** Nota: la cantidad máxima de VLAN disponibles en los switches Catalyst es 4096, ya que el campo ID de VLAN tiene 12 bits en el encabezado IEEE 802.1Q.