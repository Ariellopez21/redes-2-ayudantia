# Parte 1

Hacer la siguiente red redundante entre switches

> [!NOTE] Topología con redundancia para STP
> ![[Excalidraw/Módulo 5.md#^frame=mtbS1UeWggUwyBQccUA_I|800|center]]

Inmeditamente packet tracer les activará STP y hará la negociación entre switches para determinar el root bridge y el/los enlaces bloqueados.

Usa el comando:

```bash
 Switch# show spanning-tree 
```

Y obtendrás la MAC del root bridge y la MAC del dispositivo.

> [!NOTE] La MAC del root bridge y del dispositivo serán la misma si están dentro del root bridge.

Escribe las 4 MAC de los switches en la topología.

Y redacta algo pequeño de entre 1 a 2 líneas justificando quién es el root bridge y cuál o cuáles es o son los alternativos.