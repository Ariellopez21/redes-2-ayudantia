Para evitar fallos en la formación de EtherChannel, todos los puertos deben coincidir en:

- **Velocidad y dúplex.**
    
- **Configuración de VLAN:**
    - VLAN nativa (en troncales).
    - VLANs permitidas (en troncales).
    - VLAN de acceso (en puertos de acceso).
        

#### Errores típicos

- Los puertos no están en la **misma VLAN** o no están configurados como troncales de forma consistente.
    
- Configurar **troncal solo en algunos puertos** del grupo (debe configurarse en la interfaz `port-channel`, no en cada puerto físico).
    
- **Rango de VLANs permitidas distinto** en un EtherChannel troncal → impide la formación del canal.
    
- **Incompatibilidad en la negociación** de PAgP o LACP entre ambos extremos (ej. `auto` con `auto`).
    

#### Nota

Es común confundir protocolos:

- **PAgP / LACP → agregación de enlaces (EtherChannel).**
- **DTP → negociación automática de troncales.**

En la práctica: primero se configura el **EtherChannel** (PAgP o LACP), y luego se ajusta el **modo troncal** (DTP si corresponde).

## Solución de problemas

Paso a paso...

#### Paso 1

**Ver la información de resumen de EtherChannel** usando `show etherchannel summary`.

Siempre es útil saber sí realmente está habilitado el port-channel y qué puertos están relacionados.

#### Paso 2

Toca ver salidas más detalladas, yendo a `show run | begin interface port-channel` y observar uno a uno cómo se comunican las negociaciones de cada interfaz, puede ser que por accidente un puerto esté en `on` y todos los demás en `active/pasive` y eso lo cambié todo.

#### Paso 3

Sí en el paso 1 o 2 encontró problemas, corregir los errores correspondientes.

Sí configuró mal algún puerto con el ejemplo anterior respecto al `on` y `pasive/active`, entonces, debe directamente eliminar el port-channel y volver a crear el enlace.

Un ejemplo de cómo reconfigurar sería, eliminar el enlace: `S1(config)# no interface port-channel 1`, luego, volver a crear el canal usando `range` y dentro asignar correctamente los protocolos automáticos usando `LACP` o `PAgP` en los modos correctos para que la negociación funcione. Finalmente, entrar al port-channel usando `interface port-channel 1` y configurar el `switchport` correspondiente.

#### Paso 4

Verificar que esté todo en orden a través de los comandos utilizados en paso 1 y 2.