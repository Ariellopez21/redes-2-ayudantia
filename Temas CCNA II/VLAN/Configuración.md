![[VLAN]]

## Crear

En el modo `(config)#`:

```bash
S1(config)# vlan [vlan-id]
```

Asigna nombre:

```bash
S1(config-vlan)# name [name]
```

#### Crear en rangos

Se puede utilizar rangos usando `-` o varios números separados por una coma `,` para asignar varias configuraciones de VLAN al mismo tiempo.

> [!example] Ejemplo 1
> ```bash
> S1(config)# vlan 10,20,30
> ```

> [!example] Ejemplo 2
> ```bash
> S1(config)# vlan 10-30
> ```

## Eliminar una VLAN

### Comando

```bash
S1(config)# no vlan [id]
```

##### Información importante

> [!danger] Precaución
> Antes de borrar una VLAN, asegurese de reasignar todos los puertos de acceso a otra VLAN diferente a la que eliminará.

> [!question] ¿Por qué?
> Los puertos que no se trasladen de una VLAN que fue borrada, no se podrán comunicar y los perderá a menos que recupere el estado de la configuración antes de borrar la VLAN.

## Configuración de puertos en VLAN

### Puerto de Acceso

En el modo `(config)#` ingrese a la interfaz que desea darle acceso a la VLAN y determine que el puerto será de modo **acceso**.

```bash
S1(config)# interface [int-id]
S1(config-if)# switchport mode access
S1(config-if)# switchport access vlan [id]
```

> [!example] Cambiar el acceso de las VLAN en una interfaz 
> Sí al ejecutar `switchport access vlan [id]` **te equivocas** de VLAN, es decir, querías ingresar la VLAN 19 y pusiste la 18, basta con **volver a ingresar** el comando para que se actualice la VLAN.
> **¡Recuerda!** Esto se debe a que solo se puede asignar una **única VLAN** por **interfaz de acceso**.

#### Crear en rangos

Use `interface-range` para configurar en varias interfaces al mismo tiempo.

```bash
S1(config)# interface-range [int-id-range]
S1(config-if-range)# switchport mode access
S1(config-if-range)# switchport access vlan [id]
```


### Puerto de VLAN de Voz

Como se vio en la sección [[Tipos de VLAN#VLAN de Voz|VLAN de Voz]], este es el tipo de tráfico que se admite de forma **compartida** en un **puerto de acceso**.


> [!example] Ejemplo
> ```bash
> S1(config)# vlan 10
> S1(config-vlan)# name STUDENT
> S1(config)# vlan 150
> S1(config-vlan)# name VOICE
> S1(config)# interface fa0/18
> S1(config-if)# switchport mode access
> S1(config-if)# switchport access vlan 10
> S1(config-if)# mls qos trust cos
> S1(config-if)# switchport voice vlan 150
> ```

> [!info] La implementación de QoS no está contemplada en este curso.


> [!note] Sobre switchport
> El comando `switchport access vlan [id]` fuerza la creación de una VLAN si no se creó de antemano con el siguiente comando en el modo de configuración:
> `(config)# vlan [id]`


### Puerto Troncal

En el modo `(config)#` ingrese a la **interfaz** que desea utilizar cómo **troncal** y determine el **puerto** que será de modo **trunk**, adicionalmente, determine las **VLAN** que desea **permitir** el acceso por dicho **puerto troncal** a través del comando que finaliza con `[vlan-list]`

```bash
S1(config)# interface [int-id]
S1(config-if)# switchport mode trunk
S1(config-if)# switchport trunk allowed vlan [vlan-list]
```

> [!important] Sobre VLAN Nativa
> Es importante considerar que en este paso se puede cambiar la **VLAN Nativa**.
> Tal como se mencionó en [[Tipos de VLAN#VLAN Nativa]].
> Por lo tanto, debe utilizar,
> ```bash
> S1(config-if)# switchport trunk native vlan [vlan-id]
> ```
> Y **designar** la **VLAN Nativa** como una **diferente** a la **VLAN Predeterminada**, además, que **todos los enlaces troncales** deben tener la **misma** **VLAN Nativa**.

> [!example] Ejemplo de configuración
> Suponga que desea admitir las VLAN 10, 20, 30, 99.
> Donde cada una corresponde a una VLAN de tráfico excepto la VLAN 99 que es administrativa y nativa al mismo tiempo.
> ```bash
> S1(config)# interface fastEthernet 0/1
> S1(config-if)# switchport mode trunk
> S1(config-if)# switchport trunk native vlan 99
> S1(config-if)# switchport trunk allowed vlan 10,20,30,99
> ```

#### Eliminar Puerto Troncal y Nativo

Utilice el comando `no` para eliminar las configuraciones realizadas.

> [!example] Ejemplo de eliminación de puertos
> ```bash
> S1(config-if)# no switchport trunk allowed vlan
> S1(config-if)# no switchport trunk native vlan
> ```