### Mitigación de ataques de VLAN

1. Eliminar los troncales en cualquier puerto de acceso (usar switchport mode access en los puertos de acceso).
2. Idealmente, las opciones automáticas de negociación troncal como dynamic auto o desirable deben estar desactivadas y funcionar únicamente con troncales estáticos.
3. Las VLAN Nativas deberían usarse solamente en los enlaces troncales.
4. Las VLAN nativa nunca deberían compartirse con una VLAN de datos.