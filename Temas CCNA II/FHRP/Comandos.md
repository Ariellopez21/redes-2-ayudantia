Entra a la **interfaz que actúa como gateway predeterminado** en tu router.  

Dentro de ella se utiliza el modo `standby`, que corresponde a la configuración del **router virtual** y del **grupo HSRP** asociado.
## Configurar gateway virtual

Define la **dirección IP virtual compartida** entre los routers del grupo HSRP.  

Esta será la IP configurada como _gateway predeterminado_ en los hosts de la red.

```bash
Router(config-if)# standby [id-group] ip [virtual-gateway]
```

## Configurar prioridad del puerto

Determina **qué router debe ser el activo** (el que reenvía tráfico).  

El valor por defecto es **100**, y el rango permitido va de **0 a 255**.  

Cuanto mayor es la prioridad, mayor probabilidad de que ese router sea el activo.

```bash
Router(config-if)# standby [id-group] priority [0-255]
```

> [!NOTE] Si dos routers tienen la misma prioridad, el de **IP más alta** será elegido como activo.

## Configurar intento de prioridad

Permite que un router con **mayor prioridad** recupere el rol de activo cuando vuelva a estar disponible tras una falla.

```bash
Router(config-if)# standby [id-group] preempt
```

> [!NOTE] Si este comando no está habilitado, el router que haya quedado activo **mantendrá el control**, aunque otro tenga una prioridad superior.
