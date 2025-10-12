## Opciones

Esta es la tabla completa de CISCO (aproximadamente).

|**Opciones de FHRP**|**Descripción**|
|---|---|
|**Protocolo de Router de Reserva Directa (HSRP, Hot Standby Router Protocol)**|Es un FHRP propietario de Cisco que permite conmutación por error (failover) transparente de un router IPv4 de primer salto. HSRP proporciona redundancia al permitir que varios routers compartan una IP predeterminada. Un router actúa como activo (reenvía paquetes) y otro como de espera (asume el rol si el activo falla).|
|**HSRP para IPv6**|Versión IPv6 del HSRP. Usa direcciones MAC e IPv6 virtuales derivadas del grupo HSRP. Envía anuncios RA periódicos; si el router activo falla, estos anuncios se detienen y otro asume el rol.|
|**Virtual Router Redundancy Protocol v2 (VRRPv2)**|Protocolo **no propietario** que permite a varios routers compartir una IP virtual IPv4. Un router es elegido como maestro y los otros como respaldo. Similar a HSRP, pero estándar abierto.|
|**VRRPv3**|Extensión de VRRPv2 compatible con IPv4 e IPv6. Más escalable y apto para entornos de múltiples proveedores.|
|**Protocolo de Equilibrio de Carga del Gateway (GLBP, Gateway Load Balancing Protocol)**|FHRP propietario de Cisco que no solo proporciona respaldo, sino también **balanceo de carga**: reparte el tráfico entre varios routers del grupo.|
|**GLBP para IPv6**|Versión IPv6 de GLBP. Permite que varios routers compartan un gateway IPv6 virtual y repartan el tráfico mientras ofrecen redundancia.|
|**Protocolo de detección del router ICMP (IRDP, ICMP Router Discovery Protocol)**|FHRP heredado definido en RFC 1256. Permite a los hosts descubrir routers IPv4 cercanos para obtener conectividad fuera de su red local.|

## Tabla resumen

| **Protocolo** | **Tipo**               | **IPv4/IPv6** | **Fabricante**      | **Función principal**                              |
| ------------- | ---------------------- | ------------- | ------------------- | -------------------------------------------------- |
| **HSRP**      | Redundancia            | IPv4          | Cisco               | Failover automático (router activo y de respaldo). |
| **HSRPv6**    | Redundancia            | IPv6          | Cisco               | Versión IPv6 de HSRP con anuncios RA.              |
| **VRRPv2**    | Redundancia            | IPv4          | Estándar abierto    | Igual que HSRP, pero no propietario.               |
| **VRRPv3**    | Redundancia            | IPv4 e IPv6   | Estándar abierto    | Más escalable y multi-proveedor.                   |
| **GLBP**      | Redundancia + Balanceo | IPv4          | Cisco               | Reparte la carga entre routers activos.            |
| **GLBPv6**    | Redundancia + Balanceo | IPv6          | Cisco               | Igual que GLBP, pero en IPv6.                      |
| **IRDP**      | Descubrimiento         | IPv4          | Estándar (RFC 1256) | Permite a los hosts encontrar routers disponibles. |
