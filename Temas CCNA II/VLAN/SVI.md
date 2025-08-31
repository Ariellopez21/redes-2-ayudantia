### VLAN de administración

De manera predeterminada, el switch está configurado para controlar su **administración** a través de la VLAN 1. Todos los puertos se asignan a la VLAN 1 de manera predeterminada.

Por motivos de seguridad, se considera una práctica recomendada utilizar una VLAN distinta de la VLAN 1 para la **VLAN de administración**, como la VLAN 99 en el ejemplo.

> [!info] Switch VLAN Interface, es la configuración de las VLAN en un switch.

La SVI se activa de la siguiente forma:

![[Temas CCNA II/Comandos#Configurar VLAN Crear|Comandos]]

---

> [!example] Nota sobre SVI
> El **SVI** para **`VLAN [id]`** no aparecerá como "activo / activo" hasta que **se cree** la `VLAN [id]` y **haya** un dispositivo conectado a un puerto de switch asociado con `VLAN [id]`.

