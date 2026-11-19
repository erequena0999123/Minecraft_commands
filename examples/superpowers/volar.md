# Volar

Poder de vuelo mediante elytras y cohetes para jugadores identificados con `volar`. Entrega elytras irrompibles, repone cohetes y asigna un multiplicador base de daño por caída de cero a cada jugador conectado que tenga `volar`.

## Activación y funcionamiento

La instalación asigna el tag al jugador indicado y entrega unas elytras a todos los jugadores que tengan esa etiqueta. El jugador debe equiparlas y utilizarlas para planear; los cohetes permiten impulsarse durante el vuelo.

| Propiedad | Valor escrito en los comandos |
| --- | --- |
| Etiqueta | `volar` |
| Objeto | `minecraft:elytra` |
| unbreakable | `{}`: no pierde durabilidad por uso |
| Encantamiento | Protection 10 |
| fall_damage_multiplier base | 0 |
| Vida máxima adicional al equipar la elytra | 12 puntos (6 corazones), ranura del pecho |
| Reposición | 64 cohetes si no hay ninguno en la barra rápida |

La reposición comprueba `hotbar.*`, es decir, la barra rápida. No comprueba todo el inventario ni rellena continuamente una pila parcialmente consumida. Se mantiene mientras el bloque correspondiente esté activo y el jugador tenga el tag. No hay temporizador de recarga.

## Exclusividad y retirada

El bloque de exclusividad de elytras normales solo se ejecuta si existe al menos un jugador conectado con `volar`. Mientras se cumple esa condición, `clear` elimina elytras del inventario de los jugadores sin el tag, incluidas las obtenidas por otros medios. Cuando no queda ningún portador conectado, el bloque deja de eliminarlas. No devuelve las elytras ya borradas.

La asignación de `fall_damage_multiplier` se ejecuta individualmente como cada jugador con `volar`, sin depender de su distancia al bloque. La entrega y la reposición también alcanzan a todos los jugadores con la etiqueta. Al ejecutar la secuencia de asignación se actualiza la protección de todos los portadores conectados; las incorporaciones posteriores necesitan ejecutar de nuevo esa secuencia.

La retirada restablece el daño por caída de todos los jugadores con `volar` y después elimina la etiqueta. Recupera el valor predeterminado, no valores personalizados anteriores.

Después de retirar el poder, la limpieza continua elimina las elytras y los cohetes marcados del inventario de quienes ya no tengan `volar`, aunque no quede ningún portador.

### Comandos

Sustituye `NOMBRE_JUGADOR` por el nombre exacto del jugador que recibirá el poder antes de copiar el comando. El marcador no se escribe literalmente en el juego. Los comandos están preparados para bloques, sin barra inicial.

#### Colocar tag y entregar el poder:

<strong>impulso-necesita redstone</strong>

<pre>tag NOMBRE_JUGADOR add volar</pre>

<strong>cadena-necesita redstone</strong>

<pre>give @a[tag=volar] minecraft:elytra[minecraft:custom_data={poder:"volar"},minecraft:unbreakable={}, minecraft:enchantments={protection:10},minecraft:attribute_modifiers=[{id:"poderes:volar_vida",type:"minecraft:max_health",amount:12,operation:"add_value",slot:"chest"}]] 1</pre>

<strong>cadena-siempre activo</strong>

<pre>execute as @a[tag=volar] run attribute @s minecraft:fall_damage_multiplier base set 0</pre>

#### Mantener el poder y su exclusividad:

<strong>repetición-necesita redstone</strong>

<pre>execute as @a[tag=volar] unless items entity @s hotbar.* minecraft:firework_rocket run give @s minecraft:firework_rocket[minecraft:custom_data={poder:"volar"}] 64</pre>

#### Vida máxima y Resistencia al llevar equipada la elytra especial:

<strong>repetición-siempre activo-incondicional</strong>

<pre>execute as @a[tag=volar] if items entity @s armor.chest minecraft:elytra[minecraft:custom_data~{poder:"volar"}] run effect give @s minecraft:resistance 1 0 true</pre>

La elytra equipada añade seis corazones de vida máxima. Con la vida base normal permite 16 corazones en total. El beneficio desaparece al desequiparla; llevarla en el inventario no lo activa.

La vida adicional se recupera mediante los mecanismos normales del juego; este modificador no cura continuamente.

La vida adicional pertenece al objeto. La limpieza continua retira la elytra marcada a quienes no tengan `volar`.

Mantén cargado y activo este bloque. Renueva Resistencia I solo con `volar` y la elytra marcada equipada. Al quitarla, el efecto se agota en un segundo como máximo.

#### Limpieza permanente de elytras y cohetes marcados:

Conservar el bloque adicional de exclusividad anterior con redstone: retira elytras normales de no portadores mientras exista un portador conectado.

<strong>repetición-necesita redstone-incondicional</strong>

<pre>execute if entity @a[tag=volar] run clear @a[tag=!volar] minecraft:elytra</pre>

Añadir un circuito independiente de **repetición, siempre activo, incondicional** seguido de bloques de **cadena, siempre activo, incondicional**. No depende de que quede un portador ni de la señal de instalación o retirada. Flechas siguiendo el orden; cada comando ocupa un bloque. Mantener cargada la zona del circuito. Si se configura el primer bloque como necesita redstone, mantener una señal permanente.

<pre>clear @a[tag=!volar] minecraft:elytra[minecraft:custom_data~{poder:"volar"}]</pre>

<pre>clear @a[tag=!volar] minecraft:firework_rocket[minecraft:custom_data~{poder:"volar"}]</pre>

<pre>execute in minecraft:overworld as @e[type=minecraft:item] if items entity @s contents minecraft:elytra[minecraft:custom_data~{poder:"volar"}] run kill @s</pre>

<pre>execute in minecraft:overworld as @e[type=minecraft:item] if items entity @s contents minecraft:firework_rocket[minecraft:custom_data~{poder:"volar"}] run kill @s</pre>

<pre>execute in minecraft:the_nether as @e[type=minecraft:item] if items entity @s contents minecraft:elytra[minecraft:custom_data~{poder:"volar"}] run kill @s</pre>

<pre>execute in minecraft:the_nether as @e[type=minecraft:item] if items entity @s contents minecraft:firework_rocket[minecraft:custom_data~{poder:"volar"}] run kill @s</pre>

<pre>execute in minecraft:the_end as @e[type=minecraft:item] if items entity @s contents minecraft:elytra[minecraft:custom_data~{poder:"volar"}] run kill @s</pre>

<pre>execute in minecraft:the_end as @e[type=minecraft:item] if items entity @s contents minecraft:firework_rocket[minecraft:custom_data~{poder:"volar"}] run kill @s</pre>

La limpieza permanente afecta solo copias marcadas: inventarios de jugadores conectados sin `volar` y objetos tirados cargados en las tres dimensiones vanilla. Los objetos tirados se eliminan aunque haya portadores. No elimina entidades de cohete en vuelo. Cofres y contenido de contenedores portátiles quedan fuera; al recuperar un objeto marcado en el inventario sin el tag, se limpia. Los objetos normales no coinciden con esta marca. La exclusividad anterior de elytras normales sigue teniendo su condición temporal.

#### Quitar el poder:

<strong>impulso-necesita redstone-incondicional</strong>

<pre>execute if entity @a[tag=volar]</pre>

<strong>cadena-siempre activo-condicional</strong>

<pre>execute as @a[tag=volar] run attribute @s minecraft:fall_damage_multiplier base reset</pre>

<strong>cadena-siempre activo-condicional</strong>

<pre>tag @e[tag=volar] remove volar</pre>

Coloca los tres bloques en ese orden y orienta sus flechas siguiendo la secuencia. El restablecimiento debe ejecutarse antes de quitar la etiqueta; los bloques de cadena dependen del resultado del bloque anterior.

Conserva el orden y la orientación de los bloques de cadena de instalación. El bloque de entrega está indicado como necesita redstone y requiere activación para ejecutar esa parte de la secuencia.

[Pruebas y decisiones](../../extras/laboratorios/volar.md) · [Volver a superpoderes](README.md)
