## SSH vs Telnet

**Telnet** utiliza el puerto TCP 23. Es un protocolo que utiliza la **transmisión de texto sin formato** **seguro** tanto de la *autenticación de inicio de sesión* (nombre de usuario y contraseña) como de los *datos transmitidos* entre los dispositivos de comunicación.

**Secure Shell (SSH)** es un protocolo seguro que utiliza el puerto TCP 22. Proporciona una **conexión** de administración segura (**encriptada**) a un dispositivo remoto.

El *SSH debe reemplazar a Telnet para las conexiones de administración*. SSH proporciona **seguridad** para las **conexiones remotas** mediante el **cifrado seguro** *cuando se autentica* un dispositivo (nombre de usuario y contraseña) y también *para los datos transmitidos* entre los dispositivos que se comunican.

> [!example] Puertos TCP
> Los **puertos** SSH y Telnet corresponden respectivamente a los puertos 22 y 23 del protocolo **TCP**
