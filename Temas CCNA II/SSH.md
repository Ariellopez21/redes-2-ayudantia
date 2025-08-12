### SSH vs Telnet

**Telnet** utiliza el puerto TCP 23. Es un protocolo que utiliza la **transmisión de texto sin formato** **seguro** tanto de la *autenticación de inicio de sesión* (nombre de usuario y contraseña) como de los *datos transmitidos* entre los dispositivos de comunicación.

**Secure Shell (SSH)** es un protocolo seguro que utiliza el puerto TCP 22. Proporciona una **conexión** de administración segura (**encriptada**) a un dispositivo remoto.

El *SSH debe reemplazar a Telnet para las conexiones de administración*. SSH proporciona **seguridad** para las **conexiones remotas** mediante el **cifrado seguro** *cuando se autentica* un dispositivo (nombre de usuario y contraseña) y también *para los datos transmitidos* entre los dispositivos que se comunican.

> [!example] Puertos TCP
> Los **puertos** SSH y Telnet corresponden respectivamente a los puertos 22 y 23 del protocolo **TCP**

###### Show versión para admitir SSH

A continuación, al ejecutar ``show version``, si el Cisco IOS posee un **``k9``**, entonces **admite ssh**.

```cli
S1# show version
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE7, RELEASE SOFTWARE (fc1)
```

### Configuración SSH

#### Paso 1

Con la misma finalidad que en [[#Show versión para admitir SSH]].

```cli
S1# show ip ssh
```

#### Paso 2

Configurar dominio con un **nombre de dominio IP** (DNS).

```cli
S1(config)# ip domain-name [name; ej. cisco.com]
```

#### Paso 3

Generar clave RSA.

```cli
S1(config)# ip ssh version 2
S1(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024
```

###### Eliminar clave RSA

Después de eliminar la clave, el servidor ssh quedará deshabilitado automáticamente.

```cli
S1(config)# crypto key zeroize rsa
```

#### Paso 4

Autenticar de forma local un usuario.

```cli
S1(config)# username [username] secret [password]
```

Esto **añadirá** a la base de datos del dispositivo, en este caso, un Switch de nombre `S1`, el **usuario** y su contraseña para poder **conectarse** a través de ssh de forma **remota**.

#### Paso 5

Configurar las lineas de terminal virtual (vty line)

```cli
S1(config)# line vty 0 15
S1(config-line)# transport input ssh
S1(config-line)# login local
```

Vamos a analizar, línea por línea, **número 1**: 

- **`line`**: se refiere a una **línea de acceso**, es decir, un canal de comunicación o consola virtual.
- **`vty`**: significa **Virtual Teletype**, que básicamente representa una **línea de terminal virtual**, usada para acceder al dispositivo de forma **remota**,mediante **Telnet o SSH**.

Entonces, `line vty 0 15` configura las **líneas virtuales del 0 al 15**, permitiendo hasta 16 sesiones simultáneas de Telnet o SSH.

Línea **número 2**:

``transport input ssh`` significa:

- **Solo** se permiten **conexiones remotas** mediante **SSH**.  
- **Telnet** queda **deshabilitado**.

``transport input`` puede configurarse de varias formas:

- `transport input none`: Desactiva todas las conexiones remotas.
- `transport input ssh telnet`
- `transport input telnet`
- `transport input all`

Finalmente, línea **número 3**:

- **`login`**: habilita el requerimiento de autenticación para las sesiones entrantes (por Telnet o SSH, según cómo esté configurado `transport input`, pero en **este caso** solo **ssh**).
- **`local`**: especifica que la **autenticación se hará con la base de datos local** del dispositivo, es decir, usando **usuarios y contraseñas creados con el comando `username`**.


> [!important] Usar solo ``local``
> Si en ves de usar `login local` solo se usara `login`, entonces, las contraseñas de los usuarios depende exclusivamente de las `vty line`, o sea, que se debe entrar al modo de configuración `(config-line)` y allí utilizar `password [password]`.

#### Paso 6

Sí no habilitó `ip ssh version 2`, este es el momento de hacerlo en el modo de `(config)`.
