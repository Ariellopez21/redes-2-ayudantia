## Dominio de colisiones
 
Imagina una **calle antigua y angosta** (como una de un solo carril en ambos sentidos) donde los autos de ida y vuelta comparten el mismo espacio:

- Esa calle es como un **hub Ethernet**: todos los autos (dispositivos) compiten por el mismo espacio (ancho de banda).
    
- Si dos autos intentan pasar al mismo tiempo en direcciones opuestas, se genera un **choque** → esa es la **colisión** en redes.
    
- Toda esa calle compartida es un **dominio de colisión**.
    

Ahora piensa en una **intersección con semáforo en verde solo en una dirección a la vez**:

- Eso es como un **switch en semidúplex**.
    
- Los autos pueden avanzar, pero solo en un sentido a la vez. Si ambos intentan avanzar sin respetar el semáforo, vuelve a haber colisión.
    

Finalmente, imagina que la calle se amplía y se convierte en una **avenida de doble vía bien separada, con carriles exclusivos**:

- Eso es como un **switch en dúplex completo**.
    
- Cada dirección tiene su propio carril, así que los autos pueden circular al mismo tiempo sin chocar.
    
- En este escenario ya **no existen colisiones**, porque cada carril es independiente.

## Dominio de difusión

Los switches conectados entre sí crean dominios de difusión.

Los dominios de difusión son divididos por dispositivos de capa 3 como un **Switch de capa 3** o un **router**.

A continuación 3 ejemplos de dominio de difusión, donde cada sigla en los dibujos son representativos:
- PC: Computador
- SW: Switch
- R: Router
- SW 3: Switch de capa 3

> [!NOTE] Dominio de difusión 1
> ![[Excalidraw/Módulo 2.md#^frame=yhm_V7ITY09-Fml-hWfUh | 600 |  center]]
> Este es un ejemplo donde solo observas 1 dominio de difusión.


> [!NOTE] Dominio de difusión 2
>  ![[Excalidraw/Módulo 2.md#^frame=vWnoRD3NN2p7KzrpmeyeU | 600 | center]]
>  Este es un ejemplo donde observas 4 dominios de difusión.


> [!NOTE] Dominio de difusión 3
> ![[Excalidraw/Módulo 2.md#^frame=mYx_rqmPFsV2gf4WZhYna | 600 | center]]
> Suponiendo que el Switch de capa 3 actúa como router en todos sus puertos, este es un ejemplo donde se observan ==6 o 7 dominios de difusión==.

Cuando un switch recibe una trama de difusión, la reenvía por cada uno de sus puertos, excepto por el puerto de entrada en el que se recibió la trama de difusión. Cada dispositivo conectado al switch recibe una copia de la trama de difusión y la procesa.