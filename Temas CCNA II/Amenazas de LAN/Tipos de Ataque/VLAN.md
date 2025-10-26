## Ataques de VLAN

Tenemos 2:

- VLAN Hopping Attack.
- VLAN Double - Tagging Atack

### Ataque de Salto de VLAN

Permite que el tráfico de una red de área local virtual pueda ser visto por otra red de área local virtual. Todo esto, sin tener intervención de otro dispositivo tal como un router.

Un actor de amenaza va a configurar un host para que funcione como un switch y luego usando un host va a tomar ventaja de la función automática del puerto troncal que está activado de forma predeterminada en la mayoría de los puertos del switch.

Estos son los conocidos como: dynamic auto o dynamic desirable de los puertos del switch.

El actor de amenaza va a configurar el host para falsificar la señal de 802.1Q y los mensajes de DTP de manera que se forme el troncal entre el host y el switch. Una vez establecido el troncal de manera exitosa, va a poder enviar y recibir tráfico en cualquier red de área local virtual de manera efectiva saltando entre cualquier VLAN a través de las cuales quieren conectarse.

### Ataque de Doble etiqueta de VLAN

Un actor de amenaza va a introducir una etiqueta de 802.1Q escondida dentro de una trama que ya tiene un etiquetado de VLAN 802.1Q.

Supongamos, un atacante va a construir un mensaje que va a comunicar su VLAN actual, que será la VLAN 10, con la VLAN dirigida de VLAN 20.

El atacante está en la VLAN 10 y va a construir una trama que va a tener un encabezado de VLAN externo con VLAN 10 y un encabezado de LAN interno con la VLAN 20, cuando se envía el mensaje hacia un primer switch, el switch verá el encabezado externo de la VLAN 10, el switch va a remover el encabezado y **enviará el tráfico hacia cualquier dispositivo funcionando con la VLAN 10.**

El switch ve que la VLAN 10 también es la VLAN nativa de manera que también va a remover dicha etiqueta y enviará el tráfico a través del enlace troncal, ahora, mientras la trama se mueve a través del enlace troncal se remueve el primer encabeza de VLAN 10 (ahora es cuando ocurre lo mencionado a lo largo de toda esta explicación).

Posterior a esto, queda expuesta la etiqueta de la VLAN 20, el segundo switch va a recibir la trama, va a remover la trama de la VLAN 20 y **enviará el tráfico hacia cualquier dispositivo funcionando con la VLAN 20.** Lo que permite al atacante, enviar el tráfico hasta un host que fue atacado.

Esto le permite al atacante que se encuentra en la VLAN 10, comunicarse con el host de la VLAN 20 que fue atacado, gracias a un doble etiqueta de VLAN.

> [!NOTE] Este escenario solo funciona cuando el actor de amenaza está en la misma VLAN que la VLAN Nativa

> [!warning] La VLAN Nativa **nunca** debe ser la misma VLAN que una VLAN de datos.

> [!info] [[Temas CCNA II/Seguridad LAN/Mitigación Ataques/VLAN|Mitigación VLAN]]
