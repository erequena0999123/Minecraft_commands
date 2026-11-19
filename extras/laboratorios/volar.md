# Laboratorio: Volar

[Ficha y comandos](../../examples/superpowers/volar.md) · [Volver a laboratorios](../laboratorios.md)

## Protección contra caídas para todos los portadores

El usuario autorizó extender la asignación a todos los jugadores con volar para admitir más de un portador. Se sustituye únicamente attribute @p[tag=volar] minecraft:fall_damage_multiplier base set 0 por execute as @a[tag=volar] run attribute @s minecraft:fall_damage_multiplier base set 0. Se conserva la configuración del bloque de cadena y el resto del circuito. La protección se asigna al ejecutar la secuencia; no se convierte en un mantenimiento nuevo ni se da por probado con varias personas.

La retirada conjunta existente se conserva por ahora, pendiente de elegir y probar el mecanismo de solicitud individual. Este cambio no altera elytra, vida, Resistencia, cohetes ni limpieza. Referencia estable de la revisión: Java26.3 según índice oficial consultado el17noviembre2026; no identifica la instalación de futuros usuarios.

**Pendiente de prueba:** ejecutar asignación con dos portadores conectados y comprobar el atributo de ambos. El usuario no está obligado a disponer ahora de medios para hacer esa prueba; no atribuirle un resultado no reportado.

## Resultados y decisiones

- Confirmado por el autor: los seis corazones adicionales aparecen al equipar la elytra y no se aplican al llevarla en el inventario. El modificador de +12 puntos de vida máxima es la solución actual.
- Confirmado: limpieza de elytras y cohetes marcados tanto del suelo como del inventario de jugadores sin `volar`. No se indicó una prueba de cada dimensión.
- Confirmado el 14 de noviembre de 2026: retirada del poder con restablecimiento de daño por caída y posterior reasignación.
- Resistencia I fue probada; el autor consideró pequeña su protección y decidió conservarla.
- Alternativa descartada: Absorción III renovada continuamente. El autor comprobó que mantenía los corazones y resultaba excesiva. Se sustituyó por vida máxima adicional en el equipo.
- Migración desde la alternativa anterior: desactivar el bloque de Absorción y sustituir las elytras entregadas antes de añadir el modificador. Cambiar el comando de entrega no actualiza objetos existentes.
- Pendiente: eficacia de Protection 10 en la elytra e interacción con efectos de Resistencia de otras fuentes.

La versión exacta ejecutada, el número de jugadores y otras condiciones no indicadas por el autor permanecen sin registrar. Una comprobación documental o una prueba de otro poder no acredita estas condiciones.

<details>
<summary>Notas anteriores y fuentes</summary>

Archivo de las explicaciones anteriores, conservadas para consultar el origen de los cambios. Sus menciones de pruebas pendientes reflejan el momento en que se escribieron; los resultados actualizados figuran arriba.

Estado de desarrollo: implementación recuperada el 14 de noviembre de 2026. Ese día el autor confirmó en Minecraft que la retirada de tres bloques funciona, incluido el restablecimiento del daño por caída, y que después pudo volver a asignar el poder. La versión exacta y el número de jugadores de esa prueba no fueron indicados; no se extiende esa confirmación a otras condiciones.

El autor confirmó la limpieza de elytras y cohetes marcados en el suelo y en inventarios de jugadores sin `volar`. Solo probó Volar: no se extiende esa confirmación a perlas, bolas de nieve ni calaveras ni a dimensiones o condiciones no indicadas. Probó Resistencia I y considera insuficiente su protección; probó después Absorción III y pidió retirarla porque los corazones se reponían continuamente. Se sustituye por +12 puntos de vida máxima en la elytra, manteniendo Resistencia I. El nuevo modificador queda pendiente de prueba. Cambios incorporados el 16 de noviembre de 2026. Referencia: Java 26.3 según el [índice oficial](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs) y [sintaxis oficial de componentes, predicados y slot contents](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-20-5).

Esta comprobación depende de los portadores conectados seleccionados por `@a`, no de si alguien está volando en ese instante. El cambio de exclusividad temporal se incorporó el 16 de noviembre de 2026 y está pendiente de prueba específica en Minecraft.

Absorción III se retiró tras la prueba del autor: la renovación continua mantenía los corazones y resultaba demasiado potente. Desactivar o retirar el antiguo bloque que daba `minecraft:absorption`; el efecto de un segundo se agotará. Sustituir las elytras especiales ya entregadas por las de la nueva entrega: actualizar el comando no cambia los objetos existentes. No hace falta un bloque periódico para aplicar la vida máxima.

La vida adicional está incluida en el componente `minecraft:attribute_modifiers` de la elytra entregada, con `minecraft:max_health`, `amount:12`, `operation:"add_value"` y `slot:"chest"`. Aumenta la vida máxima seis corazones solo mientras esa elytra está equipada en el pecho. Con una base normal de 20 puntos, permite 32 puntos (16 corazones); respeta otros modificadores de vida existentes. Al desequiparla, se retira automáticamente este modificador. Llevarla en el inventario no lo activa.

Este aumento de capacidad no rellena continuamente la vida ni aplica curación. Los corazones adicionales se llenan mediante los mecanismos normales de recuperación del juego. Al quitar la elytra se pierde la capacidad adicional; no debe usarse para almacenar vida por encima del máximo restante.

El modificador de equipo sigue al objeto y no comprueba por sí mismo el tag; la limpieza continua existente retira la elytra marcada a quienes no tengan `volar`. La vida máxima adicional queda pendiente de prueba en Minecraft. Formato de modificadores según las [notas oficiales de Java 1.21](https://feedback.minecraft.net/hc/en-us/articles/27547857163917-Minecraft-Java-Edition-1-21-Tricky-Trials) y [Java 1.21.5](https://feedback.minecraft.net/hc/en-us/articles/35298208390797-Minecraft-Java-Edition-1-21-5-Spring-to-Life).

El bloque de repetición inicia este circuito y debe permanecer cargado. Renueva Resistencia I (amplificador 0) únicamente con `volar` y la elytra marcada en la ranura del pecho. Llevarla en el inventario no activa el beneficio. Al quitarla o perder el tag, deja de renovarse y el efecto de este sistema se agota en un segundo como máximo. No se usa `effect clear` para no borrar Resistencia de otras fuentes; los efectos del mismo tipo comparten su gestión vanilla. Resistencia es un efecto de estado, no un atributo de armadura. La interacción con efectos más fuertes queda pendiente de prueba. Protection 10 se conserva; su eficacia en elytras no se da por demostrada.

La retirada comprueba que hay jugadores con `volar`, restablece su `fall_damage_multiplier` base al valor predeterminado y después elimina la etiqueta. Si varios jugadores tienen el tag, el restablecimiento alcanza a todos ellos. No recupera valores base personalizados anteriores.

Tras la retirada deja de reponer cohetes y la limpieza continua elimina las elytras y los cohetes marcados del inventario de quienes ya no tengan `volar`, aunque no quede ningún portador. El poder puede asignarse de nuevo mediante la secuencia de instalación. Las copias anteriores sin marca no se reconocen: deben retirarse manualmente y sustituirse mediante la nueva entrega; no se borran por ser irrompibles.

</details>
