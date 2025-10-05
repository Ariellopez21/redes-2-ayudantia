## Retransmisión DHCP

Esto hará que R1 retransmita transmisiones DHCPv6 al servidor DHCPv6.

```bash
R1(config-if)# ipv6 dhcp relay destination [ip-dhcpv6-server] [int][int-id]
```

- `[int][int-id]`: Corresponde a la interfaz de mi dispositivo, por la que quiero que salga la información.
- Recordemos que estamos en el modo `(config-if)`, o sea, ya estamos dentro de la interfaz del dispositivo por la que entra la información.

> [!info] Considera que, este comando se configura en la interfaz que frente a los clientes DHCPv6

Ej:

```bash
R1(config)# interface gigabitethernet 0/0/1
R1(config-if)# ipv6 dhcp relay destination 2001:db8:acad:1::2 G0/0/0
```

## Router como DHCP stateless

```bash
R1(config-if)# ipv6 nd other-config-flag
```

## Router como DHCP statefull

```bash
R1(config-if)# ipv6 nd managed-config-flag
R1(config-if)# ipv6 nd prefix default no-autoconfig
```