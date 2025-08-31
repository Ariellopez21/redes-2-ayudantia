
| Tipo de problema                             | Cómo arreglar                                                                                                                                                                               | Cómo verificar                                                                    |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| VLAN faltantes                               | - Cree (o vuelva a crear) la VLAN si no existe. <br> - Asegúrese de que el puerto host está asignado a la VLAN correcta.                                                                    | `show vlan [brief]` <br> `show interfaces switchport` <br> `ping`                 |
| Problemas con el puerto troncal del switch   | - Asegúrese de que los enlaces troncales estén configurados correctamente. <br> - Asegúrese de que el puerto es un puerto troncal y está habilitado.                                        | `show interfaces trunk` <br> `show running-config`                                |
| Problemas en los puertos de acceso de switch | - Asigne el puerto a la VLAN correcta. <br> - Asegúrese de que el puerto es un puerto de acceso y está habilitado. <br> - El host está configurado incorrectamente en la subred incorrecta. | `show interfaces switchport` <br> `show running-config interface` <br> `ipconfig` |
| Temas de configuración del router            | - La dirección IPv4 de la subinterfaz del router está configurada incorrectamente. <br> - La subinterfaz del router se asigna al ID de VLAN.                                                | `show ip interface brief` <br> `show interfaces`                                  |

## VLAN faltantes

Sí tiene una VLAN10 con un puerto adjunto, por ejemplo, Fa0/6, al ejecutar `show vlan brief` verá que la interfaz está asociada a la VLAN10.

Sin embargo, si por accidente elimina la VLAN usando  `no vlan 10` antes de desasociar el puerto al mismo, perderá por completo el acceso a dicho puerto, esto lo verá reflejado al volver a ejecutar `show vlan brief` y buscar entre la lista de puertos el Fa0/6 que configuró con la VLAN10, ya que, al eliminar la VLAN10, todo lo asociado se va junto con él.

Corroboramos una vez más usando `show interface Fa0/6 switchport` y observará que la interfaz aparece como que **está asociada aún a la VLAN 10 pero de forma inactiva**.

### Cómo recuperar puertos

Si vuelve a crear la VLAN que eliminó con `(config)# vlan 10` y realiza un `show vlan brief` verá que la VLAN10 volverá a estar disponible y junto a ella se encuentra el puerto que estuvo asociado a él.

## Puerto troncal

Básicamente piense siempre que su alternativa es revisar que los puertos troncales estén configurados correctamente y activos.

- Deben permitir el paso de las VLAN que usted quiera que pasen por ella
- Deben estar activas como ``switchport mode trunk``

A través de `show interfaces trunk` verá todas las interfaces trunk que configuró, si la interfaz que busca no está aquí, quiere decir que ocurrió una de las siguiente situaciones:

- El puerto nunca fue configurado como trunk.
- El puerto está apagado
- Otro.

> [!info] Recemos que nunca sea otro.

Para saber si es puerto está apagado usamos `show run` para entrar a la configuración y buscar que el puerto este encendido.

## Puerto de acceso

Sí usted no puede realizar ping hacia su propio gateway a pesar de tener la configuración en el PC correctamente, probablemente no está configurado el puerto de acceso.

Para revisar utilice `show interface [int] [id] switchport`, ejemplo `show interface fa0/6 switchport` y revise dos cosas:

- Que esté en **modo de acceso**.
- Que diga a cuáles VLANs le tiene permitido el acceso.

## Configuración del router

En el caso de router-on-a-stick puede ocurrir un problema donde todas las VLANs se pueden comunicar entre sí, excepto por una.

Dicha VLAN tiene los puertos de acceso y troncales bien configurados, y como estamos trabajando con router-on-a-stick, al ejecutar el comando `show ip interface brief` podemos corroborar sí:

- Las subinterfaces están activas y con las ips correctamente configuradas
- Si la interfaz troncal está activa usando `no shut`

Pero no podemos corroborar el encapsulamiento, para ello, usamos `show interfaces | include Gig|802.1Q`

Y obtendremos las configuraciones del **encapsulamiento dot1q**, así podemos corroborar que dicho encapsulamiento también fue realizado con éxito o no.

Si tenemos **sospechas del encapsulamiento dot1q** desde el inicio, también podemos revisar usando el comando `show run interface [int] [id].[subint]`, ejemplo: `show run interface g0/0.10` y veremos directamente si la interfaz de la que sospechamos es culpable o no.

Para corregir, basta con sobre escribir el encapsulamiento usando `# encapsulation dot1q [vlan-id]` en el modo de configuración de la subinterfaz donde encontramos el problema.
