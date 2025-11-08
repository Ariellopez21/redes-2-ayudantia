
> [!NOTE] Conexión WLAN
> ![[Pasted image 20251104083426.png]]
> - Conexión de equipo por cable hacia un router inalámbrico.
> - Conexión de router inalámbrico hacia modem de bancha ancha (DSL)

Estos routers proveen:

- Seguridad WLAN
- Servicios DHCP
- NAT (Traducción de Direcciones de Red)
- QoS
- Otras funciones

## Conexión hacia router inalámbrico

Los router vienen pre configurados.

Los routers usan DHCP automáticamente.

Para configurar un router usando la GUI:

1. Abra un navegador
2. Ingrese la IP privada predeterminada del router. (se encuentra en la documentación del router)
3. De forma predeterminada (**suele ser**) 192.168.0.1 y el usuario es admin con clave admin.

### Configuración básica

1. Iniciar sesión
2. Cambiar contraseña de admin predet.
3. Cambiar las IPv4 predet. del DHCP
4. Renovar dirección IP de host (CMD -> /renew).
5. Iniciar sesión en el router con la nueva IP.

### Configuración inalámbrica

1. Ver valores predet. WLAN (SSID, clave, otros)
2. Modo de red: Se puede elegir qué estándar 802.11 usar (Auto, N-Only, Legacy, Disabled). Por ejemplo Legacy significa que todos los dispositivos que se conectan al router deben tener una variedad de NIC inalámbrica instaladas. (NIC 802.11a/n/ac).
3. Configurar canales: recuerde para 2.4GHz (canales 1,6,11).
4. Configurar modo de seguridad: AES, TKIP, WPA2, etc.

## Configuración de red de malla (WMN)

Un router basta para proporcionar internet en un radio de 45 mts.

Sí se quiere extender, se usan APs conectados al router que extienden la conectividad.

## NAT - IPv4

En la GUI del router, en la sección **estado** se tiene la IPv4 asignada del router que se transmite a internet (una ip pública como 209.165.201.11).

NAT en pocas palabras es la transformación de IPv4 privadas como:

- 10.0.0.0/8
- 172.16.0.0/16
- 192.168.1.0/24

A IPv4 públicas que tienen permitido comunicarse por el internet (enrutables en internet).

## QoS

Configurar QoS permite decidir sí se prefiere mejorar el tráfico para preferir voz y vídeo.

En algunos routers esto se puede configurar en [[#Reenvío de puertos|puertos específicos]] (así como la VLAN VoIP)

Puede salir en el router como **Control de Ancho de Banda**.

## Reenvío de puertos

Es un método basado en reglas que permite dirigir el tráfico entre dispositivos de redes separadas.

Esto es básicamente una [[ACL]].

Es decir:
- Puedo decirle al router a través de direcciones IPv4 quién tiene permitido el acceso o salida a mi red.
- Puedo decirle al router a través de puertos como HTTP (puerto:80), HTTPS (puerto:443), FTP (puerto:72?) u otro sí el tráfico tiene permitido pasar por una dirección IPv4
- Puedo decirle al router a través de puertos como los anteriormente mencionados sí un host puede enviar o recibir mensajes con dichos puertos.
- O todas las anteriores combinadas.



