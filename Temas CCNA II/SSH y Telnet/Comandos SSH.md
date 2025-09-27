## Configuración general

1. Activar ssh versión 2

```bash
S1(config)# ip ssh version 2
```

2. Generar llave RSA

```bash
S1(config)# crypto key generate rsa
How many bits in the modulus [512]: 1024
```

> [!NOTE] Se recomienda 1024 o más

3. Activar su uso en la interfaz necesaria (line vty)

```bash
S1(config)# line vty [range-id-port]
S1(config-line)# transport input ssh
S1(config-line)# login local
```

## Otras configuraciones

- Show: Para saber sí está activa

```bash
S1# show ip ssh
```

- Agregar DNS

```bash
S1(config)# ip domain-name [name; ej. cisco.com]
```

- Eliminar clave RSA

```bash
S1(config)# crypto key zeroize rsa
```

- [[#Show versión para admitir SSH|Show version]].

### Show versión para admitir SSH

A continuación, al ejecutar ``show version``, si el Cisco IOS posee un **``k9``**, entonces **admite ssh**.

```cli
S1# show version
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE7, RELEASE SOFTWARE (fc1)
```