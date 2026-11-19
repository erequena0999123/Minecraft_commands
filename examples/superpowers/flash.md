# Flash

Supervelocidad para jugadores con el tag `flash`: mejora movimiento, ataque y desplazamiento acuático. Funciona mientras el poder esté asignado y su circuito permanezca activo; no necesita objeto activador ni recarga.

## Configuración aplicada

| Propiedad | Valor escrito en los comandos |
| --- | --- |
| Tag del poder | `flash` |
| Velocidad de ataque base | `10` |
| Velocidad de movimiento base | `0.3` |
| Efecto de nado | Gracia de delfín II |
| Renovación del efecto de nado | 2 segundos, con partículas visibles |

Los valores de los atributos son parámetros del juego: no equivalen directamente a bloques recorridos o golpes efectivos por segundo. El efecto de nado se renueva mientras se ejecute su bloque.

## Alcance de la implementación actual

Los atributos se aplican a `@p[tag=flash]`, el portador más cercano a cada bloque. Gracia de delfín se aplica a `@a[tag=flash]`, todos los portadores conectados. Se conserva esta mecánica aprobada por el autor. La adaptación de destinatarios para varios jugadores se revisará por separado.

La retirada actual restablece los atributos del portador más cercano y después quita el tag a todas las entidades etiquetadas. Los valores base vuelven al predeterminado, sin recuperar un valor personalizado anterior. Gracia de delfín deja de renovarse y termina al agotarse sus dos segundos restantes, salvo que otro sistema la aplique.

### Comandos

Sustituye `NOMBRE_JUGADOR` por el nombre exacto del destinatario antes de copiar. Cada comando ocupa un bloque independiente, sin `/` inicial. Para usar un comando desde el chat del juego, añade `/`.

#### Asignar el poder:

**Bloque 1: impulso, necesita redstone, incondicional.**

<pre>tag NOMBRE_JUGADOR add flash</pre>

#### Mantener las habilidades:

Circuito de tres bloques en este orden. Primero: **repetición, necesita redstone, incondicional**, con señal continua. Los dos siguientes: **cadena, siempre activo, incondicional**. Orienta las flechas siguiendo la secuencia y mantén cargada la zona.

1. Velocidad de ataque:

<pre>attribute @p[tag=flash] minecraft:attack_speed base set 10</pre>

2. Velocidad de movimiento:

<pre>attribute @p[tag=flash] minecraft:movement_speed base set 0.3</pre>

3. Efecto de nado:

<pre>effect give @a[tag=flash] minecraft:dolphins_grace 2 1 false</pre>

#### Retirada actual del poder:

Conservar este orden y las condiciones indicadas. Esta secuencia conserva el alcance conjunto explicado arriba; no es todavía una retirada individual por solicitud.

**Bloque 1: impulso, necesita redstone, incondicional.** Comprobar que existe un portador:

<pre>execute if entity @e[tag=flash]</pre>

**Bloque 2: cadena, siempre activo, condicional.** Restablecer velocidad de ataque:

<pre>attribute @p[tag=flash] minecraft:attack_speed base reset</pre>

**Bloque 3: cadena, siempre activo, incondicional.** Restablecer velocidad de movimiento:

<pre>attribute @p[tag=flash] minecraft:movement_speed base reset</pre>

**Bloque 4: cadena, siempre activo, incondicional.** Retirar el tag:

<pre>tag @e[tag=flash] remove flash</pre>

[Pruebas y decisiones](../../extras/laboratorios/flash.md) · [Volver a superpoderes](README.md)
