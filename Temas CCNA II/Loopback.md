
## Loopback IPv4

La interfaz de **bucle invertido (loopback)** es una **interfaz lógica** interna del router. **No está asignado a un puerto físico** y **nunca se puede conectar a ningún otro dispositivo**. Se la considera una interfaz de software que se coloca automáticamente en estado "up" (activo), siempre que el router esté en funcionamiento.

La interfaz loopback es **útil para probar** y administrar un dispositivo Cisco IOS, ya que asegura que por lo menos una **interfaz** esté **siempre disponible**. Por ejemplo, se puede usar con fines de prueba, como la prueba de procesos de routing interno, mediante la emulación de redes detrás del router.

Las interfaces de **bucle invertido** también se utilizan comúnmente en entornos de laboratorio para crear **interfaces adicionales**. Por ejemplo, puede crear varias interfaces de bucle invertido en un router para **simular más redes** con fines de práctica de configuración y pruebas. En este plan de estudios, a menudo usamos una interfaz de bucle invertido para **simular un enlace a Internet**.

```cli
R1(config)# interface loopback [id]
R1(config-if)# ip address [ipv4-address] [subnet-mask]
```

> [!important] La dirección IPv4 para cada interfaz de bucle invertido debe ser única y no debe ser utilizada por ninguna otra interfaz
