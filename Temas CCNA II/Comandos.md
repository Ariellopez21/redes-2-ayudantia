# Show

###### shows generales

- `show startup-config`
- `show running-config`
- `show flash`: Muestra los archivos de la memoria flash.
- `show version`
- `show history`
- `show ip interface [id]`: Muestra la información IP de una interfaz.
- `show interfaces [id]`: Muestra la configuración de una interfaz.
- `show mac-address-table`: Muestra la tabla de direcciones MAC
- `show ip ssh`: Para ver si el equipo admite ssh.

###### Verificación de interfaz

- `show ip interface brief`: resumen de todas las intefaces.
- `show running-config interface [interface-id; ej. g0/0]`: Muestra la info. de la interfaz 
- `show ip route`: Muestra la tabla de ruteo.

###### duplex 

A continuación, un ejemplo:

```bash
S1# show controllers ethernet-controller fa0/1 phy | include MDIX
```

###### interfaz

```bash
S1# show interfaces [id]
```


# Configuraciones rápidas y secundarias

### Duplex y Semiduplex

###### Configurar modo de duplex

```bash
S1(config)# interface [interface] [id]
S1(config-if)# duplex [option]
S1(config-if)# speed [number]
```

### Negociación

###### Configurar negociación automática (activa)

```bash
S1(config-if)# mdix auto
```

# VLAN

###### Configurar VLAN: Crear

Crea un SVI

```bash
S1(config)# interface vlan [id]
S1(config-if)# ip address [ipv4-address] [subnet-mask]
```

# Gateway predeterminado

###### Configuración del gateway predeterminado

No olvidar que esto debe hacerse en un **switch**.

```cli
S1(config)# ip default-gateway [ip-gateway-without-mask]
```

# Configuración básica

## Guardar

###### Guardar configuración en ejecución (running-conf)

```bash
S1# copy running-config startup-config
```

###### Guardado rápido y reinicio

```bash
S1# wr
S1# reload
```

## Acceso al CLI

###### Clave de acceso al CLI

```cli
R1(config)# enable secret [password]
```

###### Encriptar contraseña

Encripta la contraseña de la base de datos del dispositivo

```cli
R1(config)# service password-encryption
```

## VLAN

![[#VLAN#Configurar VLAN Crear]]

## Hostname

###### Configurar nombre de dispositivo

```cli
R1(config)# hostname [hostname]
```

## Banner

###### Banner de notificaciones

```cli
R1(config)# banner motd #MESSAGE_HERE#
```

## VTY Line

###### Configuración vty line

```cli
R1(config)# line console 0
R1(config-line)# password [password]
R1(config-line)# login
R1(config-line)# exit
R1(config)# line vty [range]
R1(config-line)# password [password]
R1(config-line)# login
R1(config-line)# exit
```

> [!important] La línea 5 generalmente se anota como `line vty 0 4` para Routers y `line vty 0 15` para Switches.

## Interfaces

###### Configuración de interfaces

```cli
R1(config)# interface [interface] [id]
R1(config-if)# ip address [ipv4-address] [subnet-mask]
R1(config-if)# ipv6 address [ipv6-address]/[prefix-mask]
R1(config-if)# description [description]
R1(config-if)# no shutdown
```

# Rutear

### Estático

###### ip route

```cli
R1(config)# ip route [subnet-ip-destination] [mask] [interface out | ip-next-jump]
```
