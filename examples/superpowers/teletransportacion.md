# Teletransportación

Poder para jugadores identificados con `teletransportar`. Repone perlas de Ender y aplica regeneración temporal cuando detecta su uso. La teletransportación depende del comportamiento vanilla de la perla lanzada; la secuencia no utiliza un comando de teletransporte directo.

## Activación y funcionamiento

La instalación asigna el tag al jugador indicado, crea `lanzar_perla` e inicia en cero el contador de los jugadores etiquetados.

| Propiedad | Valor escrito en los comandos |
| --- | --- |
| Etiqueta | `teletransportar` |
| Objeto | `minecraft:ender_pearl` |
| Objetivo | `lanzar_perla` |
| Criterio | `minecraft.used:minecraft.ender_pearl` |
| Nombre visible del objetivo | Teletransportar |
| Reposición | 16 perlas si no hay ninguna en la barra rápida |
| Regeneración | 2 segundos, amplificador 5 (nivel VI), partículas visibles |

El mantenimiento comprueba `hotbar.*`, la barra rápida. No revisa todo el inventario ni rellena una pila parcialmente consumida. Tras detectar un contador de 1 o más, aplica regeneración y devuelve el contador a cero para procesar usos posteriores.

No asigna un atributo de vida: aplica el efecto temporal `minecraft:regeneration`. Tampoco añade un temporizador propio de recarga ni modifica expresamente la recarga vanilla del objeto. La reposición continua depende de que el circuito permanezca activo.

## Regeneración y momento del daño

La regeneración comienza al lanzar la perla y puede terminar antes de una llegada lejana. No garantiza evitar el daño de la teletransportación.

## Alcance y retirada

La reposición y la regeneración seleccionan entidades con el tag mediante `@e`; la inicialización y el reinicio del contador seleccionan jugadores con `@a`. El poder está concebido para asignarse a jugadores.

`lanzar_perla` es un objetivo compartido del mundo: se crea una vez mientras exista. Si se asigna el poder a otro jugador con el objetivo ya creado, el comando de creación informa de que ya existe; no es necesario eliminarlo para añadir otro portador. Conservar los bloques de cadena sin condición cuando así se indican.

La retirada elimina el objetivo completo y después quita `teletransportar` de todas las entidades etiquetadas. Es una retirada conjunta, no una baja individual. Deja de suministrar perlas y aplicar regeneración mediante este sistema; la limpieza independiente elimina de sus inventarios las perlas marcadas al dejar de tener el tag. No cancela explícitamente el efecto de regeneración ya aplicado, que dura hasta dos segundos. Las perlas normales y las copias antiguas sin marca se conservan.

### Comandos

Sustituye `NOMBRE_JUGADOR` por el nombre exacto del jugador que recibirá el poder antes de copiar el comando. El marcador no se escribe literalmente en el juego. Los comandos están preparados para bloques, sin barra inicial.

#### Colocar tag y scoreboard:

<strong>impulso-necesita redstone</strong>

<pre>tag NOMBRE_JUGADOR add teletransportar</pre>

<strong>cadena-siempre activo</strong>

<pre>scoreboard objectives add lanzar_perla minecraft.used:minecraft.ender_pearl "Teletransportar"</pre>

<pre>scoreboard players set @a[tag=teletransportar] lanzar_perla 0</pre>

#### Mantener el poder:

<strong>repetición-necesita redstone</strong>

<pre>execute as @e[tag=teletransportar] unless items entity @s hotbar.* minecraft:ender_pearl run give @s minecraft:ender_pearl[minecraft:custom_data={poder:"teletransportacion"}] 16</pre>

<strong>cadena-siempre activo</strong>

<pre>effect give @e[tag=teletransportar, scores={lanzar_perla=1..}] minecraft:regeneration 2 5 false</pre>

<pre>scoreboard players set @a[tag=teletransportar, scores={lanzar_perla=1..}] lanzar_perla 0</pre>

#### Quitar el poder:

<strong>impulso-necesita redstone</strong>

<pre>scoreboard objectives remove lanzar_perla</pre>

<strong>cadena-siempre activo</strong>

<pre>tag @e[tag=teletransportar] remove teletransportar</pre>

Cada comando corresponde a un bloque independiente. Los bloques de cadena indicados sin condición se configuran como incondicionales. Colócalos en el orden mostrado, con sus flechas siguiendo cada secuencia.

#### Limpieza continua de objetos marcados:

Circuito independiente de la entrega y retirada del poder. Primer bloque: **repetición, siempre activo, incondicional**. No necesita una señal externa ni depende de que exista algún portador:

<pre>clear @a[tag=!teletransportar] minecraft:ender_pearl[minecraft:custom_data~{poder:"teletransportacion"}]</pre>

Después, tres bloques de **cadena, siempre activo, incondicional**, con las flechas siguiendo la secuencia. Cada comando ocupa un bloque:

<pre>execute in minecraft:overworld as @e[type=minecraft:item] if items entity @s contents minecraft:ender_pearl[minecraft:custom_data~{poder:"teletransportacion"}] run kill @s</pre>

<pre>execute in minecraft:the_nether as @e[type=minecraft:item] if items entity @s contents minecraft:ender_pearl[minecraft:custom_data~{poder:"teletransportacion"}] run kill @s</pre>

<pre>execute in minecraft:the_end as @e[type=minecraft:item] if items entity @s contents minecraft:ender_pearl[minecraft:custom_data~{poder:"teletransportacion"}] run kill @s</pre>

Mantén cargada la zona. Todas las cadenas son incondicionales. Puedes usar repetición con redstone si la señal es permanente; un pulso breve no mantiene la limpieza.

La limpieza alcanza inventarios de jugadores conectados sin el tag y objetos marcados tirados en zonas cargadas de las tres dimensiones, aunque su dueño conserve el poder. No elimina proyectiles lanzados.

Solo se eliminan las copias marcadas. Los cofres y el contenido de contenedores portátiles quedan fuera; al recoger una copia sin tener el tag, se limpia del inventario. Los productos fabricados no se detectan.

[Pruebas y decisiones](../../extras/laboratorios/teletransportacion.md) · [Volver a superpoderes](README.md)
