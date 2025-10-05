
## Descripción general

![[Stateless Statefull#Stateless]]

### Mensajes RA y RS

Los **mensajes RA** son enviados por un router IPv6 cada 200 segundos y SLAAC los utiliza para proporcionar direccionamiento y otra información de configuración que normalmente proporcionaría un servidor DHCP.

Un host también puede enviar un mensaje **Router Solicitation (RS)** solicitando que un router habilitado para IPv6 envíe al host un RA.

> [!NOTE] Sobre Mensajes RS
> Cuando un host está configurado para obtener su información de **direccionamiento automáticamente**, envía un **mensaje RS** a la dirección de **multidifusión** IPv6 de `ff02::2`.

## Activación de SLAAC

1. **Verificar direcciones IPv6**: Ingresar a la interfaz que se desea verificar que tenga SLAAC activo, sí no posee la **IPv6 all-nodes group** `ff02::2`, entonces toca **habilitar enrutamiento**.

```bash
R1# show ipv6 [int][int-id]
```

2. **Habilitar enrutamiento**: Para incluir las interfaces al grupo de difusión `ff02::2`

```bash
R1(config)# ipv6 unicast-routing
```

3. **Verificar que SLAAC esté habilitado**: Volvemos a la interfaz que queríamos que pertenezca al grupo de difusión y debería tener incluido el grupo `ff02::2`, por lo tanto ya está habilitado para **enviar mensajes ICMPv6 RA**.

```bash
R1# show ipv6 int [int][int-id] | section Joined
```

## Only SLAAC

Método **Solo SLAAC** está habilitado de forma predeterminada cuando se ejecuta `ipv6 unicast-routing`

La tabla debería verse así:

| Flag | value |
| ---- | ----- |
| A    | 1     |
| O    | 0     |
| M    | 0     |

> [!NOTE] identificador único extendido (EUI)
> - El cliente puede crear su propio ID de interfaz utilizando el método Extended Unique Identifier (EUI-64) o hacer que se genere aleatoriamente.
> - Para más información, [[#Generar ID de Interfaz|clic aquí]].

Cuando la configuración está en modo Only SLAAC, se incluye: Prefijo, longitud de prefijo, servidor DNS, la MTU y default gateway a partir del mismo router.

## Generar ID de Interfaz

Cuando un host obtiene su dirección IPv6 mediante **SLAAC**, el router le entrega el **prefijo de 64 bits** de la red a través de los mensajes RA. El **host** debe completar los **otros 64 bits** (EUI) y puede hacerlo de dos formas:

1. **Generación aleatoria:** el sistema operativo inventa un número aleatorio de 64 bits. Así funcionan hoy en día la mayoría de los Windows 10 y otros sistemas modernos, porque protege la privacidad del usuario.
    
2. **EUI-64:** el host toma su **MAC de 48 bits**, le inserta `FFFE` en medio y con eso obtiene los 64 bits necesarios. Este método antes era el común, pero tiene el problema de que la dirección IPv6 queda ligada a la MAC, haciendo más fácil rastrear al dispositivo.

> [!NOTE] En resumen
> Con SLAAC el router da la “mitad” de la dirección (prefijo de red) y el host completa la otra mitad (ID de interfaz) usando aleatorio o EUI-64.

## Detección de direcciones duplicadas (DAD)

Cuando un host crea una dirección IPv6 con SLAAC, **no se asegura automáticamente que sea única** en la red. Por eso existe el proceso **DAD (Duplicate Address Detection)**.

El host envía un mensaje ICMPv6 llamado **Neighbor Solicitation (NS)** a una dirección especial de multidifusión que representa los últimos 24 bits de su dirección.

- **Si nadie responde**, significa que esa dirección no está en uso y el host puede usarla.
    
- **Si alguien responde** con un **Neighbor Advertisement (NA)**, significa que ya hay otro dispositivo con esa dirección, y el host debe generar un nuevo identificador de interfaz.
    

Aunque la probabilidad de colisión en 64 bits es mínima (18 quintillones de combinaciones posibles), la mayoría de los sistemas operativos ejecutan **DAD por seguridad**.

> [!NOTE] Nota
> No solo con SLAAC, el proceso **DAD** también lo hacen los hosts si la dirección se configuró **manualmente** o por **DHCPv6**.

