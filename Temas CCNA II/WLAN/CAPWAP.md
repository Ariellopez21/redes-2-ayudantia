## Qué es

- **CAPWAP** (estándar IEEE) permite que un **WLC** administre varios **AP/WLAN** y se encarga de **encapsular y reenviar** el tráfico entre el AP y el WLC.
    
- Deriva de **LWAPP**, pero agrega **seguridad con DTLS (Datagram Transport Layer Security)**.
    
- Crea **túneles sobre UDP (Protocolo de Datagramas de Usuario)** y puede operar con **IPv4 o IPv6** (por defecto, **IPv4**).
    
- **Puertos UDP** usados: **5246** y **5247**.
    
- En los túneles, el **campo de protocolo IP** difiere: con **IPv4 usa 17** y con **IPv6 usa 136**.z

> [!NOTE] Funcionamiento CAPWAP
> ![[Pasted image 20251104075514.png]]

## Arquitectura MAC dividida

Concepto clave: Control de acceso a medios divididos (MAC).

Concepto CAPWAP split MAC realiza funciones que un AP individual realiza y las distribuye entre dos componentes funcionales:

- Funciones AP MAC
- Funciones WLC MAC

## Encriptación de DTLS

DTLS es un protocolo que proporciona seguridad entre un AP y un WLC.

Encripta los datos y evita escuchas o alteraciones, generando privacidad en el plano de control y evitando ataques man-in-the-middle.

El cifrado está deshabilitado de forma predeterminada.

> [!NOTE] Encapsulación CAPWAP
> ![[Pasted image 20251104080211.png]]

## AP FlexConnect

Permite configurar y controlar APs a través de un enlace WAN sin necesidad de implementar un WLC en cada oficina porque usa CAPWAP.

Hay dos modos de operar:

- Modo conectado: WLC es accesible; el AP FlexConnect tiene conectividad CAPWAP con su WLC y envía tráfico a través del tunel CAPWAP.
- Modo independiente: WLC es inalcanzable; el AP FlexConnect asume algunas funciones WLC porque se ha perdido la conectividad CAPWAP sobre el WLC.

> [!NOTE] AP FlexConnect
> ![[Pasted image 20251104080707.png]]
