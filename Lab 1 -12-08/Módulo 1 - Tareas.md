# Acceso remoto

- Configurar acceso remoto con ssh y clave rsa, usando login local (1).

> [!TODO] Pendientes hasta próximos módulos
> - Configurar acceso remoto con ssh y clave rsa, usando login (1).
> - Configurar acceso remoto con ssh y telnet, clave rsa, y usando login local (1), luego desactivar las claves rsa (2), y permitir solo el acceso remoto a ssh (3).
> 

# Configuración básica de un Switch

- designar un ip default-gateway
- implementar un banner
- determinar la contraseña de acceso para el modo `#`.
- crear 3 usuarios locales
- Encriptar los datos
- Configurar acceso remoto por ssh v2 y eliminar el acceso por telnet
- crear la VLAN administrativa (de preferencia ``vlan 99``)
- Ingresar con un computador por cable ``console``.

> [!question] ¿Qué ocurriría si aplicamos todas las mismas configuraciones a un Router e intentamos entrar por cable `console`?

# Tarea loopback

- Crear un loopback en una red simple y simular que esa subred es internet, es decir, ponerla como S* para redirigir paquetes.

> [!question] ¿Qué ocurre aquí?
> Escribe en tu router `Router# debug ip packet` para ver el tráfico a través del router e intenta hacer ping desde un PC hacia otro que sí tenga IP. Verás que pasa a través de las interfaces que configuraste para llegar al destino y entregar el mensaje.
> En caso contrario, si se realiza un ping a una IP que no pertenece a ninguna subred que tu router conozca, la enviará por defecto a loopback y lo verás en el `debud mode`.
> **Ten en cuenta que**, sí se realiza un ping a una IP que sí pertenezca a una subred que tu router conozca pero **NO** está asignada a ningún equipo, no será enviada a loopback. 
> Otra forma de ver el tráfico enviado a loopback es con `# show interfaces loopback [id]`.

# VLAN

- Crear tres interfaces vlan diferentes a la vlan 1 y hacerles ping desde un equipo.

