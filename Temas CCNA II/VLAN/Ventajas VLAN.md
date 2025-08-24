
- Dominios de difusión más pequeños.
- Seguridad mejorada: Solo los usuarios de la misma VLAN pueden comunicarse entre sí **sin  enrutamiento**.
- Mejora la eficiencia del depto TI.
- Reducción de costos.
- Mejor rendimiento.
- Administración más simple de proyectos y aplicaciones.

#### Ejemplo de beneficios de una VLAN

Una red sin VLAN organizada de la siguiente manera, tendría un dominio de difusión extenso y eso, a medida que la red vaya haciéndose cada vez más grande, provocaría mala optimización de recursos en la red.

> [!info] Red sin VLAN
> ![[Pasted image 20250822090743.png|800|center]]
> - Sí PC1 quiere enviar una difusión, este paquete será enviado a todos los PCs conectados a cada Switch, o sea, a PC2, PC3, PC4, PC5 y PC6.
> - Pensemos en una red más grande, imagina que cada Switch tiene capacidad de 24 puertos y cada puerto está ocupado... Significaría que si PC1 envía una difusión tendría que reenviarse dicho paquete a más de 50 dispositivos diferentes.

Sin embargo, una red organizada de la siguiente manera, tendría dominios de difusión más pequeños gracias a la reducción de costos por la implementación de VLANs.

> [!info] Red con VLAN
> ![[Pasted image 20250822091113.png|800|center]]
> - Sí PC1 quiere enviar una difusión, esta solo será enviara a los PCs conectados a la VLAN 10, en este caso, únicamente a PC4.
> - Sí la red crece, esto no afecta de manera desmedida, ya que únicamente se estaría enviando las difusiones a cada dispositivo que pertenezca a un docente, es decir, a la VLAN 10.
