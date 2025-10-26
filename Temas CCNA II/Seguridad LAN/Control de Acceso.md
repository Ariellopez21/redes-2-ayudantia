## Control de acceso

### Autenticación con una contraseña local

- NAC provee servicios AAA
- Autenticación: configurar un inicio de sesión, combinando nombre de usuario y contraseña, a nivel de consola, lineas vty, y puertos auxiliares; el más simple de implementar, pero también el mas débil y menos seguro.
- SSH: Requiere un nombre de usuario y una contraseña, que se encriptan durante la transmisión; nombre de usuario y la contraseña pueden ser autenticados por el método de base de datos local; más responsabilidad porque el nombre de usuario queda registrado cuando un usuario inicia sesión.
- Limitaciones SSH: Las cuenta de usuario deben ser configuradas localmente en cada dispositivo. En una gran empresa con múltiples routers y switches que controlar, puede tomar mucho tiempo implementar y cambiar bases de datos locales en cada dispositivo. Además, la configuración de la base de datos local no proporciona ningún método de autenticación de respaldo.

### Componentes AAA

- Autenticación, Autorización y Registro.
- similar al uso de una tarjeta de crédito
- La tarjeta de crédito identifica quién la usa y cuánto puede gastar puede el usuario de esta, y mantiene un registro de cuántos elementos o servicios adquirió el usuario.
- marco principal para ajustar el control de acceso en un dispositivo de red.
- tiene permitido acceder a una red (autenticar), controlar lo que las personas pueden hacer mientras se encuentran allí (autorizar) y qué acciones realizan mientras acceden a la red (registrar).

### Autenticación

- Dos métodos de implementación de autenticación AAA son Local y basado en servidor.
- Los AAA locales guardan los nombres de usuario y contraseñas localmente en un dispositivo de red como el router de Cisco.
- Con el método basado en servidor, el router accede a un servidor central de AAA. El servidor AAA contiene los nombres de usuario y contraseñas de todos los usuarios.
- TACACS+ y RADIUS

### Autorización

- automática y no requiere que los usuarios tomen medidas adicionales después de la autenticación. La autorización controla lo que el usuario puede hacer o no en la red después de una autenticación satisfactoria.

### Registro

- recopila y reporta datos de uso.
- La organización puede utilizar estos datos para fines como auditorías o facturación.
- pueden incluir la hora de inicio y finalización de la conexión, los comandos ejecutados, la cantidad de paquetes y el número de bytes.
- Los servidores AAA mantienen un registro detallado de lo que el usuario autenticado hace exactamente en el dispositivo (incluye comandos EXEC y de configuración que emite el usuario)
- El registro contiene varios campos de datos, incluidos el nombre de usuario, la fecha y hora, y el comando real que introdujo el usuario.

### 802.1x

- define un control de acceso y un protocolo de autenticación basados en puertos.
- evita que las estaciones de trabajo no autorizadas se conecten a una LAN a través de puertos de switch de acceso público.
- El servidor de autenticación autentica cada estación de trabajo, que está conectada a un puerto del switch, antes de habilitar cualquier servicio ofrecido por el switch o la LAN.
- Existe un cliente (suplicante) que ejecuta el software cliente 802.1X para conectarse (por cable o inalámbrico), un servidor (autenticación) que valida la identidad del cliente y notifica al switch o AP si el cliente está autorizado o no para acceder a la LAN y a los servicios del switch, finalmente, el switch (autenticador) que funciona como intermediario (proxy) entre cliente y servidor, solicita la identificación, verifica dicha información al servidor y transmite una respuesta. En todo este proceso de autenticación, el suplicante no interactúa directamente con el servidor.
