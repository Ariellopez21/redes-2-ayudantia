## Ataques CDP de reconocimiento

- Cisco Discovery protocol, es un protocolo de descubrimiento de enlaces de capa 2.
- Verifica la conectividad de capa 1 y capa 2 y viene activado por defecto (en los dispositivos CISCO).
- Descubre otros dispositivos habilitados para CDP que estén conectados directamente.

Esto lo vuelve una gran herramienta para solucionar problemas de capa 1 y capa 2, pero también lo vuelve una gran herramienta para que los actores de amenaza puedan usarlo y descubrir vulnerabilidades de la infraestructura de la red.

La información de CDP se envía periódicamente y sin cifrar, la información transmitida incluye:
- IP address
- SO del dispositivo cisco ios
- La plataforma basada en las capacidades del modelo del dispositivo.
- Puerto en uso.
- VLAN
- etc.

Mitigación: usar en el switch habilitado con CDP, el comando no cdp run para deshabilitar por completo CDP, pero dentro del config-if usando no cdp enable se deshabilita únicamente desde la interfaz que se específica, esto para permitir usar CDP entre dispositivos switches y deshabilitarlo entre hosts.

> [!info] [[Temas CCNA II/Seguridad LAN/Mitigación Ataques/CDP|Mitigación CDP]]

### LLDP

LLD: Link Layer Discovery Protocol.

Un protocolo similar a CDP es LLDP y este también se puede deshabilitar con no lldp run y si se quiere usar en interfaces puede usarse no lldp transmit y no lldp receive en el modo config-if 