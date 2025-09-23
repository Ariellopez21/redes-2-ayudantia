## Consideraciones importantes

- **Soporte:** todas las interfaces deben ser compatibles con EtherChannel, aunque no estén físicamente contiguas.
    
- **Velocidad y dúplex:** todas las interfaces del grupo deben configurarse con la **misma velocidad** y el **mismo dúplex**.
    
- **Coincidencia de VLAN:** todas las interfaces deben pertenecer a la **misma VLAN** o estar configuradas como **troncales**.
    
- **Rango de VLAN:** en EtherChannel troncales, el **rango de VLANs permitidas** debe ser idéntico en todas las interfaces; si no coincide, el canal no se forma, incluso si los modos de negociación son correctos.


> [!NOTE] EtherChannel correctamente configurado!
> ![[Pasted image 20250922232536.png|center|500]]

## Serie de pasos

**Paso 1. Seleccionar interfaces físicas**

- Use el comando `interface range` para elegir varias interfaces al mismo tiempo.

Ej:
```bash
Switch(config)# interface range fa0/1 - 2
```

**Paso 2. Asignar las interfaces a un grupo EtherChannel**

- Cree el canal con `channel-group [number] mode active`.
    
- El número identifica el grupo (ej. `1`).
    
- El modo `active` indica que usará **LACP**.
    
Ej:
```bash
Switch(config-if-range)# channel-group 1 mode active
Creating a port-channel interface Port-channel 1
Switch(config-if-range)#
```

**Paso 3. Configurar la interfaz lógica Port-Channel**

- Ingrese a la interfaz lógica creada automáticamente (`port-channel [number]`).
    
- Ajuste aquí las configuraciones de capa 2 (acceso o troncal).

Ej:
```
Switch(config)# interface port-channel 1
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20,30
```

