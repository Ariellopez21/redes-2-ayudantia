## 12.5.1 Canal de frecuencia de saturación

Los WLAN tienen **transmisores y receptores sintonizados** a frecuencias específicas de **ondas de radio** para comunicarse.  
Una práctica común es asignar las frecuencias en rangos, los cuales se dividen en rangos más pequeños llamados **canales**.

Si la **demanda** de un **canal** específico es demasiado **alta**, es probable que se **sature**, lo que degrada la calidad de la comunicación.  
Con el tiempo se desarrollaron técnicas para mejorar la comunicación inalámbrica y evitar la saturación, usando los canales de forma más eficiente.

---

### Técnicas de modulación

| Técnica | Descripción |
|----------|--------------|
| **DSSS (Espectro de extensión de la secuencia directa)** | Técnica que extiende la señal sobre una banda de frecuencia más amplia para evitar interferencias y ocultar la señal original. Fue usada en **802.11b** (2.4 GHz). |
| **FHSS (Espectro ensanchado por salto de frecuencia)** | La señal portadora cambia rápidamente entre varios canales. El emisor y receptor deben estar sincronizados. Disminuye la congestión y fue usado en el estándar **802.11 original**. También lo usan los **walkie-talkies**, teléfonos de 900 MHz y **Bluetooth** (variante FHSS). |
| **OFDM (Multiplexación por división de frecuencias ortogonales)** | Permite que un solo canal use múltiples subcanales en frecuencias adyacentes, sin interferencia entre ellos. Se utiliza en **802.11a/g/n/ac**, y **802.11ax** usa una variación llamada **OFDMA** (Acceso múltiple por división de frecuencia ortogonal). |

---
## 12.5.2 Selección de canales

Una práctica recomendada en WLAN con múltiples AP es usar **canales no superpuestos**.  
Los estándares **802.11b/g/n** operan en el rango de **2.4 GHz a 2.5 GHz**.  
Cada canal tiene **22 MHz** de ancho y está separado del siguiente por **5 MHz**.  
El estándar **802.11b** define **11 canales** en América del Norte (13 en Europa, 14 en Japón).

### Canales superpuestos de 2.4GHz en América Norte

La interferencia ocurre cuando una señal se superpone a un canal reservado para otra señal.  
La mejor práctica para WLAN de 2.4 GHz es usar **canales no superpuestos**.  
Si hay tres AP adyacentes, usar los canales **1, 6 y 11**.

### Canales no superpuestos de 2.4GHz para 802.11b/g/n

Los estándares **802.11a/n/ac** usan la banda de **5 GHz** con **24 canales** divididos en tres secciones.  
Cada canal está separado del siguiente por **20 MHz**.  
Aunque hay ligera superposición, no se interfieren entre sí.  
La banda de 5 GHz permite **mayor velocidad** y **menos interferencia** gracias al número de canales disponibles.

### Primeros ocho canales no interferentes de 5 GHz

Al igual que con las WLAN de 2.4 GHz, elija canales que **no interfieran** al configurar múltiples AP de 5 GHz adyacentes.

## 12.5.3 Planifique la implementación de WLAN

La cantidad de usuarios que puede admitir una WLAN depende del diseño del sitio, la cantidad de cuerpos y dispositivos presentes, las velocidades de datos esperadas, el uso de canales no superpuestos y las configuraciones de potencia de transmisión.

### Recomendaciones para la ubicación de los AP:

- Considere si se usará el cableado existente o zonas donde no se puedan colocar AP.  
- Identifique fuentes potenciales de interferencia: **hornos microondas**, **cámaras inalámbricas**, **luces fluorescentes**, **detectores de movimiento**, u otros dispositivos en 2.4 GHz.  
- Coloque los **AP por encima de las obstrucciones**.  
- Coloque los **AP cerca del techo** y **centrados en su área de cobertura**.  
- Sitúe los AP donde estén los usuarios (por ejemplo, salas de reuniones).  
- Si se usa **modo mixto (IEEE 802.11)**, los clientes antiguos pueden reducir la velocidad de la red.

Al estimar la cobertura esperada, tenga en cuenta:
- El estándar WLAN implementado.  
- La naturaleza del entorno.  
- La potencia de transmisión configurada.  

Esto ayudará a planificar adecuadamente las áreas de cobertura.
