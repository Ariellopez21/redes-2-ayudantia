## Servidor CISCO IOS DHCPv4

Suponga la siguiente red de ejemplo:

> [!example] Red de ejemplo
> ![[Pasted image 20250929090248.png|800|center]]

### Paso 1

**Excluir direcciones IPv4**: Cuando un router actúa como servidor DHCPv4, puede **reservar ciertas direcciones IPv4 para que no sean asignadas automáticamente a los clientes**. Esto se hace porque algunos dispositivos, como routers, servidores o impresoras, suelen configurarse con direcciones estáticas y no deben entrar en el rango dinámico. La exclusión puede hacerse tanto para una dirección específica como para un rango completo, indicando el valor inicial y final. Además, es posible ejecutar el comando varias veces para excluir distintos bloques de direcciones.

```
Router(config)# ip dhcp excluded-address [unique-addr | range-addr]
```

### Paso 2

**Defina un nombre de grupo DHCPv4**: La configuración de un servidor de DHCPv4 implica definir un conjunto de direcciones que se deben asignar.

```
  Router(config)# ip dhcp pool pool-name    
  Router(dhcp-config)#
```

### Paso 3

**Configure el grupo DHCPv4**:
- El conjunto de direcciones y el router de gateway predeterminado deben estar configurados.
- Use la **network** instrucción para definir el rango de direcciones disponibles. 
- Use el **default-router** comando para definir el router de gateway predeterminado. 
- Normalmente, el gateway es la interfaz LAN del router más cercano a los dispositivos clientes. 
- Se requiere un gateway, pero se pueden indicar hasta ocho direcciones si hay varios gateways.

Otros comandos del pool de DHCPv4 son optativos, Por ejemplo:
- La dirección IPv4 del servidor DNS que está disponible para un cliente DHCPv4 se configura mediante el comando **dns-server**. 
- El comando **domain-name** se utiliza para definir el nombre de dominio. 
- La duración del arrendamiento de DHCPv4 puede modificarse mediante el comando **lease**. 
- El valor de arrendamiento predeterminado es un día. El comando **netbios-name-server** se utiliza para definir el servidor WINS con NetBIOS.

Para más información sobre la configuración de DHCP: [[Temas CCNA II/DHCP/DHCPv4/Comandos#comandos del pool de DHCPv4|Comandos del pool]]

### Configuración de la red de ejemplo

```bash
R1(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.9
R1(config)# ip dhcp excluded-address 192.168.10.254
R1(config)# ip dhcp pool LAN-POOL-1
R1(dhcp-config)# network 192.168.10.0 255.255.255.0
R1(dhcp-config)# default-router 192.168.10.1
R1(dhcp-config)# dns-server 192.168.11.5
R1(dhcp-config)# domain-name example.com
```

### Comandos de verificación

![[Temas CCNA II/DHCP/DHCPv4/Comandos#Comandos show|Comandos]]

### Verificación del usuario

Cuando una PC obtiene su dirección por DHCPv4, es posible verificar los parámetros asignados ejecutando el comando `ipconfig /all`. En este listado aparecen todos los valores entregados automáticamente por el servidor DHCP: la dirección IPv4, la máscara de subred, el gateway predeterminado, la dirección del servidor DNS e incluso el sufijo DNS.

> [!NOTE] Verificación de un usuario
> ![[Pasted image 20250929092811.png|800|center]]

#### Usuario de Windows

- El administrador de red libera toda la información de direccionamiento IPv4 actual mediante el comando ``ipconfig /release``
- el administrador de red intenta renovar la información de direccionamiento IPv4 con el comando ``ipconfig /renew``
### Desactivar

![[Temas CCNA II/DHCP/DHCPv4/Comandos#Activar/des Router DHCPv4|Comandos]]

