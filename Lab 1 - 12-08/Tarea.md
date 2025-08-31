# Parte 1

De acuerdo a lo aprendido en los contenidos CCNA I y a la clase de diagnóstico, se pidió realizar la siguiente red:

> [!info] Red Clase Diagnóstico
> ![[tarea1.jpeg | 800 | center]]

# Parte 2

## Acceso remoto

- Configurar acceso remoto con ssh y clave rsa, usando login local (1) en el switch de la subred $192.168.68.64/27$

> [!TODO] Pendientes hasta próximos módulos
> - Configurar acceso remoto con ssh y clave rsa, usando login (1).
> - Configurar acceso remoto con ssh y telnet, clave rsa, y usando login local (1), luego desactivar las claves rsa (2), y permitir solo el acceso remoto a ssh (3).
> 

## Configuración básica de un Switch

Al mismo switch que en la sección anterior, configurar lo siguiente:

- designar un ip default-gateway
- implementar un banner
- determinar la contraseña de acceso para el modo `#`.
- crear 3 usuarios locales
- Encriptar los datos
- Configurar acceso remoto por ssh v2 y eliminar el acceso por telnet
- crear la VLAN administrativa (de preferencia ``vlan 99``)
- Ingresar con un computador por cable ``console``.

> [!important] ¡Configurar también para el Router de la misma subred!

## Tarea loopback

- Crear una interfaz loopback en el router que debe conectarse a la subred $10.10.10.0/24$  y simular que esa subred es internet, es decir, ponerla como S* para redirigir paquetes.

> [!question] ¿Qué ocurre aquí?
> Escribe en tu router `Router# debug ip packet` para ver el tráfico a través del router e intenta hacer ping desde un PC hacia otro que sí tenga IP. Verás que pasa a través de las interfaces que configuraste para llegar al destino y entregar el mensaje.
> En caso contrario, si se realiza un ping a una IP que no pertenece a ninguna subred que tu router conozca, la enviará por defecto a loopback y lo verás en el `debud mode`.
> **Ten en cuenta que**, sí se realiza un ping a una IP que sí pertenezca a una subred que tu router conozca pero **NO** está asignada a ningún equipo, no será enviada a loopback. 
> Otra forma de ver el tráfico enviado a loopback es con `# show interfaces loopback [id]`.

# VLAN

> [!TODO] Pendientes hasta próximos módulos
> - Crear tres interfaces vlan diferentes a la vlan 1 y hacerles ping desde un equipo.

