## Asociación

Una parte importante del proceso 802.11 es descubrir una WLAN y conectarse.

Los dispositivos inalámbricos:

- Descubren APs
- Se autentican con el AP
- Se asocian con el AP

Para asociarse exitosamente, deben acordar parámetros específicos:

- SSID: Este es el nombre de la red; En empresas grandes se usan VLAN para segmentar el tráfico, cada SSID está asignada a una VLAN.
- Contraseña.
- Modo de red: Estándares 802.11a/b/g/n/ac/ad; Los AP y routers funcionan con varios estándares al mismo tiempo.
- Modo de seguridad: WEP, WPA, WPA2; Idealmente habilitar siempre el de más alto nivel de seguridad.
- Configuración de canales: Bandas de frecuencia para transmitir datos inalámbricos; los routers y AP lo ajustan automáticamente o se puede definir manualmente si existe interferencia.

## Modo de entrega

### Pasivo

Un router o AP se anuncia abiertamente con su SSID.

Los clientes eligen ingresar.

> [!NOTE] Moto de entrega Pasivo
> ![[Pasted image 20251104075056.png]]

### Activo

El cliente debe conocer datos de la red, como el SSID, contraseña y estándares.

Al enviar esta información, se envía una trama de solicitud de sondeo por varios canales.

