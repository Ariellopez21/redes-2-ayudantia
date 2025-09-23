
## Negociación automática

Con este comando se procesa el tipo de negociación del etherchannel y de paso se crea con el número `[number]` que se asigne.

```bash
Switch(config-if-range)# channel-group [number] mode [from-LACP | from-PAgP]
```

## Configurar Port-Channel

Recuerde haber creado con anterioridad el port-channel en el [[#Negociación automática|paso anterior]].

```
Switch(config)# interface port-channel [number]
Switch(config-if)# switchport mode [trunk | access]
```

Recuerde usar `Switch(config-if)# switchport trunk allowed vlan [vlan-id]` sí configuró el port-channel como troncal o usar `Switch(config-if)# switchport access vlan [vlan-id]` sí lo configuró como acceso.

## Show

![[EtherChannel]]