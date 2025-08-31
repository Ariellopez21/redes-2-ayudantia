# Tabla de direcciones MAC

Escenario:

En la sala de administración del Laboratorio de Computación en la Universidad de Magallanes se tiene un Switch con 16 puertos, de los cuales 14 son FastEthernet y 2 son GigabitEthernet.

Se le solicitó al ayudante practicante que conecte los dispositivos finales al Switch.

El ayudante conectó de la siguiente forma cada dispositivo:

| Puerto | Dispositivo | Dirección MAC |
| ------ | ----------- | ------------- |
| Fa0/1  | HAIN        | AB:C1         |
| Fa0/2  | KATAIX      | AB:C2         |
| Fa0/3  | PC1         | A0:01         |
| Fa0/4  | PC2         | A0:02         |
| Fa0/5  | PC4         | A0:04         |
| Fa0/6  | PC3         | A0:03         |
| Fa0/7  | -           | -             |
| Fa0/8  | -           | -             |
| Fa0/9  | -           | -             |
| Fa0/10 | -           | -             |
| Fa0/11 | -           | -             |
| Fa0/12 | -           | -             |
| Fa0/13 | -           | -             |
| Fa0/14 | -           | -             |
| g0/1   | -           | -             |
| g0/2   | -           | -             |
Donde HAIN y KATAIX corresponden a los servidores.

> [!INFO] Por conveniencia las Direcciones MAC solo son de 4 caracteres.

El ayudante acabó satisfecho su conexión y se fue a hacer otras tareas.

Al cabo de 1 hora, se da cuenta que debía seguir las indicaciones que dejó su jefe para él:

- Los servidores deben estar conectados a los GigabitEthernet en orden de menor MAC a mayor MAC.
- Los PC deben estar conectados a los FastEthernet que le corresponden según su MAC, por ejemplo, el PC3 tiene MAC A0:03, entonces le corresponde el Fa0/3.

Durante el transcurso de esta hora, los dispositivos estuvieron **enviando y recibiendo** una serie de tráfico cada 10 minutos, un dispositivo a la vez y sin interrupciones. El temporizador de la tabla de direcciones MAC tiene como **límite 30 minutos**. Tu primera misión es realizar la tabla de direcciones MAC de la siguiente serie de tráfico que ocurrió durante este período:

- **t = 0m:** PC1 → PC2; PC2 → PC1
- **t = 10m:** PC2 → KATAIX; KATAIX → PC2
- **t = 20m:** PC4 → PC1; PC1 → PC4
- **t = 30m:** KATAIX → HAIN; HAIN → KATAIX
- **t = 40m:** PC2 → HAIN; HAIN → PC2
- **t = 50m:** HAIN → PC3; PC3 → HAIN
- **t = 60m:** HAIN → KATAIX; KATAIX → HAIN

Luego, dibuja la conexión tal como se le indicó en la nota que le dejó su jefe al ayudante y vuelve a hacer el seguimiento de las tablas de direcciones MAC durante el flujo de los siguientes 30 minutos:

- **t = 0m:** PC1 → PC3; PC3 → PC1 
- **t = 10m:** PC3 → KATAIX; KATAIX → PC3
- **t = 20m:** PC1 → PC4; PC4 → PC1
- **t = 30m:** KATAIX → PC1; PC1 → KATAIX

> [!success] Se debe realizar la Tabla de direcciones MAC tras el transcurso de los primeros 60 minutos, la reestructuración de puertos del Switch, y la Tabla de direcciones MAC tras la reestructuración y los próximos 30 minutos de tráfico.
