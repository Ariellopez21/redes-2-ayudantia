La comunicación consta de dos routers donde uno asume el rol de activo (reenvío) y el otro de reserva (backup).

Existen configuraciones para determinar cuál quieres que sea el activo, aplicar condiciones de cuándo activar el reserva y obviamente también existen configuraciones predeterminadas.

## Prioridad e intento de prioridad

### Prioridad

El **rol de router activo o de reserva** en HSRP se define mediante un **proceso de elección**:

- Por defecto, el router con la **IP más alta** se convierte en el **activo**.
    
- Para tener más control, se usa el **valor de prioridad HSRP** (por defecto es **100**, rango **0–255**).
    
    - El router con **mayor prioridad** será el **activo**.
        
    - Si hay empate, gana el de **IP más alta**.
    
### Intento de prioridad (Preemption)

Permite que un router con **mayor prioridad** asuma el rol activo **cuando vuelve a estar disponible**.

- Si está **habilitado**, el router más prioritario **recupera el control**.
    
- Si está **deshabilitado**, el router que ya está activo **permanece así**, aunque exista otro con prioridad mayor.

### Comandos

![[Temas CCNA II/FHRP/Comandos#Configurar gateway virtual|Comandos]]

![[Temas CCNA II/FHRP/Comandos#Configurar prioridad del puerto]]

![[Temas CCNA II/FHRP/Comandos#Configurar intento de prioridad]]

## Estados y temporizadores

 Cuando se configura una **interfaz con HSRP** o se habilita primero con una configuración HSRP existente, el **router envía** y **recibe paquetes de saludo** del HSRP para comenzar el **proceso** de determinar qué estado asumirá en el **grupo HSRP**.

El router HSRP **activo** y el de **reserva** envían **paquetes de saludo** a la **dirección de multidifusión del grupo HSRP cada 3 segundos**, de forma predeterminada. 

El router de **reserva se convertirá en activo si no recibe un mensaje de saludo del router activo después de 10 segundos**. Puede bajar estas configuraciones del temporizador para agilizar las fallas o el intento de prioridad. 

> [!error] Precaución
> Para evitar el **aumento del uso de la CPU** y **cambios de estado de reserva innecesarios**, no configure el temporizador de saludo a **menos de 1 segundo** o el temporizador de espera a **menos de 4 segundos**.

### Tipos de mensaje

- Saludo: cada 3 segs. (predt.)
- Espera: cada 10 segs. (predt.)

### Tabla de estados

| **Estado de HSRP** | **Descripción**                                                                                                                                                               |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Inicial**        | Este estado se ingresa a través de un cambio de configuración o cuando una interfaz está disponible en primer lugar.                                                          |
| **Aprendizaje**    | El router no ha determinado la dirección IP virtual ni ha visto un mensaje de saludo desde el router activo. En este estado, el router espera para escuchar al router activo. |
| **Escucha**        | El router conoce la dirección IP virtual, pero no es el router activo ni el router en espera. Escucha los mensajes de saludo de esos routers.                                 |
| **Hablar**         | El router envía mensajes de saludo periódicos y participa activamente en la elección del router activo y/o en espera.                                                         |
| **En espera**      | El router es candidato a convertirse en el próximo router activo y envía mensajes de saludo periódicos.                                                                       |
