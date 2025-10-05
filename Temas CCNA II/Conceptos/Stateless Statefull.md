## Stateless

El ejemplo más común es referente a DHCPv6, donde se habla de:

- DHCPv6 statefull (Servidor dedicado o con estado)
- DHCPv6 stateless + SLAAC (Servidor sin estado)

**Stateless** significa que **ningún servidor** lleva un **seguimiento** de qué direcciones IPv6 se asignan. Los hosts crean sus propias direcciones (ej. con SLAAC) y opcionalmente consultan un servidor DHCPv6 para datos adicionales.

## Statefull

Tomando el mismo caso mencionado de DHCPv6, un servidor **con estado** es aquel que **realiza seguimiento** de la información de direcciones de red para saber qué direcciones IPv6 se están utilizando y cuáles están disponibles.

## Analogía

### Servicios web service (REST) 

Sobre **stateless**:

En servicios web, **stateless** significa que cada petición contiene toda la información necesaria, porque el servidor **no guarda el contexto** de interacciones previas. REST es un ejemplo claro de arquitectura sin estado.

### Con videojuegos en internet

Sobre **statefull**:

En un juego online de 1 jugador como **Super Smash Flash 2** o **Friday Night Funkin**, si hay un sistema de usuario/guardado en la nube, puedes cerrar sesión y al volver días después **tu avance sigue ahí** (niveles, puntajes, skins).

Sobre **stateless**:

Entras a jugar en navegador, cierras la pestaña y al volver partes desde cero porque **no se guardó tu progreso**.
Cada vez que juegas, debes entregar toda la información desde el inicio (como si nunca hubieras estado ahí antes). Por ejemplo **Juegos FRIV**.

