## OSPF

### Comandos

Crea la lista de OSPF, en este caso, la 1:

```bash
R1(config)# router ospf 1
```

Configura router ID para elegir al maestro como los root bridge, etc.

```bash
R1(config-router)# router-id [A.B.C.D]
```

Configura la interfaz de la red LAN (esta no intercambia paquetes Hello con los router):

```bash
R1(config-router)# passive-interface [int]
```

Configura la **wildcard**:

```bash
R1(config-router)# network [A.B.C.D] [W.X.Y.Z] area [id]
```

- El área generalmente es 0, `area 0`.
- La wildcard corresponde a la IPv4 `A.B.C.D` de la red que queremos aprender.
- Y la segunda parte `W.X.Y.Z` corresponde a la máscara de subred invertida.

Ej:

- Sí la máscara de una `/24` es `255.255.255.0`, su wildcard es `0.0.0.255`
- Sí la máscara de una `/30` es `255.255.255.252`, su wildcard es `0.0.0.3`

> [!info] La suma entre cada 8 bits debe ser siempre `255`

> [!success] Sí mis 8 bits son $128$, mi invertido es  $255-128=127\therefore128+127=255$

Comandos de verificación:

```bash
show ip ospf neighbor
show ip route ospf
show ip ospf interface brief
```