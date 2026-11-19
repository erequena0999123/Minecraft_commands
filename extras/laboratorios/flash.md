# Laboratorio: Flash

[Ficha y comandos](../../examples/superpowers/flash.md) · [Volver a laboratorios](../laboratorios.md)

## Presentación normalizada y funcionamiento ratificado por el autor

El usuario aclaró que Flash funciona satisfactoriamente en sus pruebas y no requiere cambios de sus habilidades. Solicitó únicamente normalizar la ficha como las demás. Se reorganizaron explicación, tabla de valores, alcance, instalación y retirada con bloques copiables y configuración explícita. Se verificó que los ocho comandos quedan idénticos y en el mismo orden; se conservan los parámetros de redstone/condición indicados en el documento previo. No se convierte esta normalización editorial en una prueba nueva de varios portadores.

La revisión de retiradas individuales queda separada y pendiente de elegir cómo solicita el jugador su retirada. El alcance @p de los atributos se explica sin invalidar el uso satisfactorio que reporta el autor.

## Resultados y decisiones

- Implementación recuperada y compartida el 14 de noviembre de 2026.
- No se registró una prueba nueva en esta revisión.
- El alcance de `@p` en atributos difiere del alcance de `@a` en el efecto de nado; la reorganización editorial conserva esos comandos.

La versión exacta ejecutada, el número de jugadores y otras condiciones no indicadas por el autor permanecen sin registrar. Una comprobación documental o una prueba de otro poder no acredita estas condiciones.

<details>
<summary>Notas anteriores y fuentes</summary>

Archivo de las explicaciones anteriores, conservadas para consultar el origen de los cambios. Sus menciones de pruebas pendientes reflejan el momento en que se escribieron; los resultados actualizados figuran arriba.

Estado de desarrollo: implementación recuperada y compartida por el autor el 14 de noviembre de 2026. La versión exacta y las condiciones de las pruebas originales no están registradas; no se ha realizado aquí una prueba nueva en Minecraft.

Los valores de los atributos no representan por sí solos una medición de velocidad en bloques por segundo ni de golpes efectivos por segundo. El poder no utiliza objeto activador ni temporizador de recarga: se mantiene mediante la etiqueta y el circuito activo.

La retirada restablece las bases de ambos atributos a sus valores predeterminados y después quita `flash` de todas las entidades que tengan esa etiqueta. No recupera valores base personalizados anteriores. Si varios jugadores tienen el poder, los atributos no se restablecen a todos con esta secuencia; se conserva el comportamiento del código aportado.

</details>
