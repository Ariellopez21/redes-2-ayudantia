### Problemas de la capa de acceso a la red

A partir del siguiente ejemplo:

```bash
S1# show interfaces fastEthernet 0/18

FastEthernet0/18 is up, line protocol is up (connected)

Hardware is Fast Ethernet, address is 0025.83e6.9092 (bia 0025.83e6.9092)MTU 1500 bytes, BW 100000 Kbit/sec, DLY 100 usec,
```

- El primer parámetro ``FastEthernet0/18 is up`` se refiere a la capa de hardware e indica si la interfaz está recibiendo una señal de detección de portadora.
- El segundo parámetro ``line protocol is up`` se refiere a la capa de enlace de datos e indica si se reciben los **keepalives** del protocolo de capa de enlace de datos.
