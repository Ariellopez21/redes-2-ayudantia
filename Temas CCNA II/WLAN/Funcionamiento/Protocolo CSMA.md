Las WLAN son configuraciones de medios compartidos semidúplex.

Esto significa que solo un cliente puede transmitir o recibir información a la vez.

Medio compartido significa que todos los clientes transmiten y reciben información a través de un mismo canal de radio.

Problemas que surgen: el cliente no puede escuchar mientras transmite, lo que hace imposible detectar una colisión por su cuenta.

## CSMA/CA

Para esto existe: **Acceso Múltiple con Detección de Operador con Evitación de Coliciones** (CSMA / CA) para determinar cómo y cuándo enviar datos.

1. Un cliente escucha el canal para ver si está inactivo.
2. Envía un mensaje RTS (Ready To Send) al AP para solicitar acceso dedicado.
3. Recibe un CTS (Clear To Send) del AP.
3.1. Sí el cliente no recibe un CTS, este espera un tiempo aleatorio antes de reiniciar el proceso.
4. Sí recibe CTS, transmite información
5. Todas las transmisiones son reconocidas, es decir, si un cliente no está siendo reconocido, asume que ocurrió una colisión y vuelve a reiniciar el proceso.