# Zonas y lobbies

El lobby del servidor conectaba con la zona de supervivencia a pocos bloques de distancia. El [punto de inicio con abeja](punto-de-inicio.md) se construyó en otro mundo, en solitario.

## Cambiar el modo de juego al cruzar el límite

El autor comprobó el cambio de modo en el servidor. Para instalarlo en otro mundo, elige el centro de tu lobby y los radios de entrada y salida según su tamaño. Usa el mismo centro en ambos comandos y deja el radio de salida mayor que el de entrada si quieres conservar la franja de transición. En este ejemplo se usaron `-864 155 486`, 41 y 45 bloques. Ejecuta cada comando periódicamente en un bloque de repetición independiente, en la dimensión del lobby y con los bloques cargados.

**Entrada.** Un jugador en supervivencia pasa a aventura al llegar a 41 bloques del centro o menos.

<pre>execute positioned -864 155 486 run gamemode adventure @a[gamemode=survival,distance=..41]</pre>

**Salida.** Un jugador en aventura pasa a supervivencia a partir de 45 bloques, inclusive.

<pre>execute positioned -864 155 486 run gamemode survival @a[gamemode=adventure,distance=45..]</pre>

La distancia es esférica e incluye la altura. Entre 41 y 45 bloques, sin incluir los extremos, cada jugador conserva su modo. Esto evita cambios repetidos al moverse junto a un único límite. Creativo y espectador quedan fuera de los selectores.

### Variante para mundos con otras actividades en aventura

Usa esta variante si el lobby comparte dimensión con un mapa de aventura, como un escape room. El lobby marca con `lobby_modo_aventura` a quienes entran desde supervivencia. Al llegar al radio de salida, solo devuelve a supervivencia a los jugadores en aventura que llevan esa etiqueta.

Instálala con el lobby vacío. Antes de encender la variante, desactiva los dos bloques de cambio de modo del montaje básico. Coloca los cuatro bloques en línea, con las flechas en orden, en la dimensión del lobby. Usa el mismo centro en todos y conserva un radio de salida mayor que el de entrada.

1. **Repetición · necesita redstone · incondicional.** Mantén la palanca encendida. Marca a los jugadores que llegan al radio interior en supervivencia.

<pre>execute positioned -864 155 486 run tag @a[gamemode=survival,distance=..41,tag=!lobby_modo_aventura] add lobby_modo_aventura</pre>

2. **Cadena · siempre activo · incondicional.** Pasa a aventura a los jugadores marcados en supervivencia dentro del radio interior.

<pre>execute positioned -864 155 486 run gamemode adventure @a[gamemode=survival,distance=..41,tag=lobby_modo_aventura]</pre>

3. **Cadena · siempre activo · incondicional.** Devuelve a supervivencia a los jugadores marcados en aventura que alcanzan el radio de salida.

<pre>execute positioned -864 155 486 run gamemode survival @a[gamemode=adventure,distance=45..,tag=lobby_modo_aventura]</pre>

4. **Cadena · siempre activo · incondicional.** Retira la etiqueta al alcanzar el radio de salida. Si otro sistema ya cambió al jugador a creativo o espectador, este paso solo retira la etiqueta.

<pre>execute positioned -864 155 486 run tag @a[distance=45..,tag=lobby_modo_aventura] remove lobby_modo_aventura</pre>

**Probado en Minecraft.** Al entrar desde supervivencia, el autor recibió la etiqueta y el lobby lo pasó a aventura. Al salir, recuperó supervivencia y perdió la etiqueta. También pudo cambiar a supervivencia manualmente fuera del lobby.

## Acceso desde la abeja a un minijuego

El [botón de inicio con abeja](punto-de-inicio.md) puede enviar al jugador a otra actividad y asignarle el modo de juego que esa actividad requiera. Sitúa el destino fuera del radio de salida del lobby.

**Montaje probado en Minecraft.** El autor añadió dos bloques después del diamante. El primero fue de cadena, siempre activo y condicional, y teletransportó al atacante tras el éxito del bloque anterior. El segundo fue de cadena, siempre activo e incondicional, y asignó aventura al jugador más cercano dentro de un bloque del destino. Con solo el teletransporte, comprobó que el lobby retiraba la etiqueta y devolvía al jugador a supervivencia. Con ambos bloques activos, la etiqueta también se retiró y el jugador terminó en aventura al llegar al escape room.

### Ejemplo con coordenadas fijas

Los siguientes bloques son una adaptación para apuntar al atacante incluso si hay otra persona junto al destino. Usa las coordenadas de tu minijuego en los tres bloques. En este ejemplo, `-800 155 486` queda a 64 bloques del centro del lobby y `adventure` corresponde al escape room. Sustituye `adventure` por el modo que corresponda a tu actividad.

1. **Cadena · siempre activo · condicional.** Después del bloque que entrega el diamante, teletransporta al atacante al punto indicado.

<pre>execute as @e[type=minecraft:bee,tag=input] if data entity @s {HurtTime:8s} on attacker if entity @s[type=minecraft:player] run tp @s -800 155 486</pre>

2. **Cadena · siempre activo · incondicional.** Comprueba que el atacante llegó al punto y retira la etiqueta del lobby antes de aplicar el modo del minijuego.

<pre>execute positioned -800 155 486 as @e[type=minecraft:bee,tag=input] if data entity @s {HurtTime:8s} on attacker if entity @s[type=minecraft:player,distance=..1] run tag @s remove lobby_modo_aventura</pre>

3. **Cadena · siempre activo · incondicional.** Aplica el modo del minijuego al atacante que está junto al destino. El bloque es incondicional porque quien ya estaba en aventura puede llegar sin etiqueta del lobby.

<pre>execute positioned -800 155 486 as @e[type=minecraft:bee,tag=input] if data entity @s {HurtTime:8s} on attacker if entity @s[type=minecraft:player,distance=..1,tag=!lobby_modo_aventura] run gamemode adventure @s</pre>

Los comandos de coordenadas fijas son una adaptación del montaje probado. Queda comprobar con un segundo jugador que un espectador situado en el destino conserva su modo.

## Protección frente a hostiles y explosivos

Sustituye la limpieza general anterior por este **bloque de repetición, necesita redstone, incondicional**. Déjalo alimentado y cargado en la dimensión del lobby. Los números son los del ejemplo: cambia el centro y el radio al instalarlo. La distancia se evalúa desde ese centro para cada entidad.

<pre>execute positioned -864 155 486 as @e[distance=..41] if predicate {type:"minecraft:entity_properties",entity:"this",predicate:{"minecraft:entity_type":["minecraft:blaze","minecraft:bogged","minecraft:breeze","minecraft:creaking","minecraft:creeper","minecraft:drowned","minecraft:elder_guardian","minecraft:ender_dragon","minecraft:endermite","minecraft:evoker","minecraft:ghast","minecraft:guardian","minecraft:hoglin","minecraft:husk","minecraft:illusioner","minecraft:magma_cube","minecraft:parched","minecraft:phantom","minecraft:piglin_brute","minecraft:pillager","minecraft:ravager","minecraft:shulker","minecraft:silverfish","minecraft:skeleton","minecraft:slime","minecraft:stray","minecraft:vex","minecraft:vindicator","minecraft:warden","minecraft:witch","minecraft:wither","minecraft:wither_skeleton","minecraft:zoglin","minecraft:zombie","minecraft:zombie_villager","minecraft:tnt","minecraft:tnt_minecart","minecraft:end_crystal","minecraft:fireball","minecraft:small_fireball","minecraft:wither_skull","minecraft:dragon_fireball"]}} run kill @s</pre>

La lista usa los 35 tipos hostiles de la [ficha de Kill Aura](../../../examples/superpowers/kill-aura.md) para Java 26.3. Incluye también TNT encendida, vagonetas con TNT, cristales del End colocados, bolas de fuego grandes y pequeñas, calaveras del Wither y proyectiles del dragón. Los objetos de inventario, la abeja del botón, su rótulo y los marcos se conservan. La clasificación es por especie: criaturas neutrales como arañas o endermen quedan fuera aunque se enfaden. Revisa los tipos si cambias de versión. [Cambios técnicos de Java 26.3](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-3)

**Probado en el juego.** El autor confirmó que la protección retira la TNT encendida. Con creepers comprobó el límite de la zona: dentro del radio se eliminan y fuera pueden aparecer y permanecer. También comprobó que un cristal del End desaparece automáticamente al colocarlo dentro de la zona protegida.

Con el mismo filtro activo, el autor comprobó que la abeja del botón permanece y responde cuando un jugador la golpea. También confirmó que el rótulo «Click para Iniciar» sigue visible encima de la abeja. La limpieza actúa sobre entidades cargadas en cada ejecución; una explosión ya iniciada o procedente del exterior puede alcanzar el interior.

## Retirar mecheros dentro del lobby

Usa un bloque independiente de **repetición, necesita redstone, incondicional**, con la palanca encendida en la dimensión del lobby. Si montaste el barrido de fuego anterior, desactívalo antes de encender el nuevo circuito.

<pre>execute positioned -864 155 486 run clear @a[distance=..41] minecraft:flint_and_steel</pre>

Usa el centro y el radio de protección de tu mundo. En este ejemplo, el bloque retira todos los mecheros del inventario de cada jugador situado a 41 bloques o menos del centro, incluido quien esté en creativo. La regla conserva el fuego decorativo normal y el de almas. Los mecheros retirados no se devuelven al salir.

**Probado en el juego.** El autor conservó el mechero en el inventario fuera del radio y comprobó que desaparecía al entrar en el lobby. El fuego decorativo siguió encendido.

[Resultados de las pruebas](../../laboratorios/lobby.md) · [Volver a Extras](../../README.md)
