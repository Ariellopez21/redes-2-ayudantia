## Ataque de tablas de direcciones MAC

### Saturación de tablas de direcciones MAC

- Todas las tablas MAC tienen un tamaño fijo, por lo tanto, un switch puede quedarse sin espacio para guardar las direcciones MAC.
- Este tipo de ataque se basa en bombardear la tabla de direcciones MAC hasta que se llena.
- Cuando esto ocurre, el switch trata la trama como un unicast desconocido y comienza a inundar todo el tráfico entrante por todos los puertos en la misma VLAN sin hacer referencia a la tabla MAC.
- Esto, permite que un atacante capture todas las tramas enviadas desde un host a otro en la LAN local o VLAN local.

> [!info] [[Temas CCNA II/Seguridad LAN/Mitigación Ataques/Tabla de direcciones MAC|Mitigación Tabla de direcciones MAC]]

