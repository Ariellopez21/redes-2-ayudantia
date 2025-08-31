## Router-on-a-stick

### Paso 1

Crear las VLANs

- `(config)# vlan [id]`: Para crear la vlan y posteriormente asignar nombre.

### Paso 2

Configurar la VLAN administrativa.

Este paso es el más importante porque usaremos la VLAN administrativa como medio para que los datos fluyan.

Puesto que esta será la que permitirá el flujo entre los switches y que tendrá los enlaces troncales que permiten el paso a todas las VLAN que yo haya configurado.

Por lo tanto, el `default-gateway` debe corresponder al de la subred de la VLAN administrativa.

```bash
S1(config)# vlan 99
S1(config-vlan)# name Management
```

```bash
S1(config)# ip default-gateway [ipv4]
```

A través de la VLAN administrativa, **los troncales pasarán la información hasta llegar al router**.

Supongamos que la subred de la VLAN administrativa es la 172.16.99.0/24, lo que significa que al llegar al router, se llegará a través de esta subred y aterrizarán todos los paquetes en el gateway 172.16.99.1/24.

A partir de allí, se pasarán a las demás subredes, por ejemplo, 172.16.10.0/24, 172.16.20.0/24, etc.

```bash
S1(config)# int vlan 99
S1(config-if)# ip add [ipv4] [mask]
S1(config-if)# no shut
```

### Paso 3

Configurar los puertos de acceso

```bash
S1(config)# int [int][id]
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan [id]
S1(config-if)# no shut
```

### Paso 4

Configurar los puertos troncales

```bash
S1(config)# int [int][id]
S1(config-if)# switchport mode trunk
S1(config-if)# no shut
```

### Paso 5

Pasamos al router, donde elegiremos una interfaz física y nos meteremos por cada subinterfaz que necesitemos para dirigir los paquetes que lleguen al router.

```bash
R1(config)# int [int] [id].[sub-id]
```

Ej: `# int g0/0/0.99`

Debemos decirle a cada subinterfaz que solamente le permitiremos el paso de la VLAN que le dictemos

```bash
R1(config-subif)# encapsulation dot1Q [vlan-id]
```

ej: `# encapsulation dot1Q 99`

Finalmente, asignamos la ip

```bash
R1(config-subif)# ip add [ipv4] [mask]
```

ej: `# ip add 192.168.99.1 255.255.255.0`

### Paso 6

Luego de configurar todas las subinterfaces correspondientes a cada VLAN, volvemos a la interfaz física y la activamos.

```bash
R1(config)# int [int] [id]
R1(config-if)# no shut
```

ej: `# int g0/0`

## Switch de capa 3 con SVIs

### Paso 1

Crear las VLANs

- `(config)# vlan [id]`: Para crear la vlan y posteriormente asignar nombre.

### Paso 2

Crear las interfaces virtuales SVI, asignarles ip y activarlas

```bash
D1(config)# int vlan [id]
D1(config-if)# ip add [ipv4] [mask]
D1(config-if)# no shut
```

### Paso 3

Configurar los puntos de acceso con sus respectivas VLANs

```bash
D1(config)# int [int] [id]
D1(config-if)# switchport mode access
D1(config-if)# switchport access vlan [id]
```

Ej de interfaz de acceso: `# int g0/1/1`

### Paso 4

Habilitar `ip routing` para que el tráfico entre VLANs esté permitido.

```bash
D1(config)# ip routing
```

## Rutear entre Switch de capa 3 y otros dispositivos de capa 3

### Paso 1

Ir al puerto que queremos enrutar y desactivar el switchport, para posteriormente poder asignarle ip.

```bash
D1(config)# int [int] [id]
D1(config-if)# no switchport
D1(config-if)# ip add [ipv4] [mask]
D1(config-if)# no shut
```

### Paso 2

Es importante saber que la configuración `ip routing` es necesaria tanto para la comunicación entre VLANs como para la comunicación de enrutamiento.

```bash
D1(config)# ip routing
```

### Paso 3

Enrutar puertos.

```bash
R1(config)# ip route [subnet-ip-destination] [mask] [interface out | ip-next-jump]
```

