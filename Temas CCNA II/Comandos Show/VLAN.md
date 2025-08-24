
- `show vlan brief`: Nombre de las VLANs, state, y puertos en uso por VLAN.
- `show vlan id [vlan-id]`: info. específica de la VLAN.
- `show vlan name [vlan-name]`
- `show vlan summary`: Resumen de info de las VLANs.

- `show interfaces [interface] [interface-id] switchport`: Entre la información que entrega está el campo `Access Mode VLAN: [id]` y `Trunking Mode VLAN: [id]` lo que permite saber a qué VLAN está asignada la interfaz.

> [!example] Verifique la configuración de enlaces troncales
> ```bash
> S1# show interfaces fa0/1 switchport
> ```
> Obtendrá información de estado como los siguientes:
> - Switchport
> - Administrative Mode
> - Operational Mode
> - Encapsulation
> - Native VLAN
> - VLAN Enabled

