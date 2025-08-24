El **Protocolo de Enlace Troncal Dinámico (DTP)** permite **negociar automáticamente** la formación de un enlace troncal entre switches Cisco vecinos.

DTP solo funciona si ambos extremos son **switches Cisco** (no funciona con routers, servidores ni switches de otros fabricantes).

El protocolo se utiliza únicamente para **negociar enlaces troncales**; no afecta a enlaces de acceso.

#### Modos de `switchport mode`

- **access**  
    El puerto se fija como **puerto de acceso**, no negocia **trunk**.

- **dynamic auto**  
    El puerto espera que el vecino inicie la negociación **trunk**. 
    Es decir, si el vecino está en **dynamic desirable** o **trunk**, el enlace se convierte en troncal.

- **dynamic desirable**  
    El puerto **intenta activamente** formar un enlace troncal.  
    ➝ Si el vecino está en **dynamic auto**, **dynamic desirable** o **trunk**, el enlace se convierte en troncal.

- **trunk**  
    Fuerza al puerto a trabajar como troncal **sin negociación**.

> [!warning] El modo por defecto en un switch Cisco es `dynamic auto`.

A continuación una tabla que muestra cuando la negociación determina un estado de enlace **Trunk**. 

Cuando el estado de negociación **no es troncal**, se determina un **enlace de acceso**.

|Negociación|access|auto|desirable|trunk|
|---|---|---|---|---|
|**access**|Access|Access|Access|Access|
|**auto**|Access|Access|**Trunk**|**Trunk**|
|**desirable**|Access|**Trunk**|**Trunk**|**Trunk**|
|**trunk**|Access|**Trunk**|**Trunk**|**Trunk**|

> [!NOTE] Notas importantes
> - Si ambos puertos están en **dynamic auto**, **no** se genera un enlace troncal (queda en **Access**).
> - Si un puerto está en **access** y el otro en **trunk**, el resultado es **Access** (no troncal).
> - Cisco recomienda **deshabilitar DTP** en enlaces troncales estáticos para evitar negociaciones no deseadas, usando:
> ```bash
> Switch(config-if)# switchport mode trunk
> Switch(config-if)# switchport nonegotiate
> ```

