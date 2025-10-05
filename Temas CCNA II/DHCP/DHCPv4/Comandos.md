## Excluir direcciones

```
Router(config)# ip dhcp excluded-address [unique-addr | range-addr]
```

## POOL

```
  Router(config)# ip dhcp pool pool-name    
  Router(dhcp-config)#
```

## Activar/des Router DHCPv4

```bash
R1(config)# service dhcp
R1(config)# no service dhcp
```

## comandos del pool de DHCPv4


- Definir el conjunto de direcciones:

```bash
network network-number [mask | / prefix-length] 
```

- Definir el router o gateway predeterminado:

```bash
default-router address [ address2 … address8 ] 
```

- Definir un servidor DNS:

```bash
dns-server address [ address2 … address8 ] 
```

- Definir el nombre de dominio:

```bash
domain-name domain 
```

- Definir la duración de la concesión DHCP:

```bash
lease {days [hours [ minutes]] | infinite} 
```

- Definir el servidor WINS con NetBIOS:

```bash
netbios-name-server address [ address2 … address8 ] 
```

## Comandos show

![[DHCPv4]]
## Retransmisión DHCP

Esto hará que R1 retransmita transmisiones DHCPv4 al servidor DHCPv4.

```bash
R1(config-if)# ip helper-address [ip-dhcpv4-server]
```

## Router como cliente (SOHO)

Entrar a la interfaz objetivo

```
SOHO(config)# int [int][id]
```

Dentro usar:

```
SOHO(config-if)# ip address dhcp
```