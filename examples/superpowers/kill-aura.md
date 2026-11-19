# Kill aura

Poder de daño cercano para jugadores con `aura_dmg`, activado mediante una calavera de esqueleto en la mano principal.

## Activación y temporizador

- La instalación crea `tiempo_aura` y lo inicia en cero para los jugadores con el tag.
- Con contador cero y calavera marcada con `poder:"kill_aura"` en la mano principal, fija el contador en 5200 y lo reduce mientras sea positivo.
- La condición de daño es `tiempo_aura=1200..`; la reactivación necesita volver a cero.

## Selección y daño actuales

Desde la posición de cada jugador con la habilidad activa, el sistema selecciona la criatura permitida más cercana dentro de 5 bloques y ordena 2 de daño de tipo `indirect_magic` por ejecución.

La lista reúne 35 tipos hostiles revisados para Java 26.3, incluidos Wither, dragón del End, Warden, Creaking, Parched e ilusionista. Los jugadores, animales de granja, aldeanos, caballos, objetos tirados y marcos quedan fuera.

<details>
<summary>Lista completa de tipos permitidos</summary>

`blaze`, `bogged`, `breeze`, `creaking`, `creeper`, `drowned`, `elder_guardian`, `ender_dragon`, `endermite`, `evoker`, `ghast`, `guardian`, `hoglin`, `husk`, `illusioner`, `magma_cube`, `parched`, `phantom`, `piglin_brute`, `pillager`, `ravager`, `shulker`, `silverfish`, `skeleton`, `slime`, `stray`, `vex`, `vindicator`, `warden`, `witch`, `wither`, `wither_skeleton`, `zoglin`, `zombie`, `zombie_villager`.

</details>

La selección es por tipo de entidad, no por su agresividad en ese instante. Endermen, piglins, lobos, arañas y arañas de cueva quedan fuera incluso si atacan. Las monturas que solo se vuelven hostiles con un jinete enemigo también quedan fuera. Los bosses personalizados basados en los tipos admitidos son elegibles. El filtro no comprueba paredes.

Estar en la lista no elimina inmunidades: algunas criaturas, como el Creaking vinculado a un corazón o el dragón del End, pueden no recibir el daño solicitado. Si la más cercana no admite el daño, el comando no elige automáticamente otra.

La entrega repone una calavera del poder si el jugador con `aura_dmg` no tiene una marcada en la barra rápida. Una calavera normal no activa el poder ni bloquea su reposición. Una vez iniciado, el temporizador sigue aunque se cambie el objeto de la mano.

### Comandos

Sustituye `NOMBRE_JUGADOR` por el nombre exacto del jugador que recibirá el poder antes de copiar el comando. El marcador no se escribe literalmente en el juego.

#### Colocar tags y scoreboards:

<strong>impulso-necesita redstone</strong>

<pre>tag NOMBRE_JUGADOR add aura_dmg</pre>

<strong>cadena-siempre activo</strong>

<pre>scoreboard objectives add tiempo_aura dummy</pre>
<pre>scoreboard players set @a[tag=aura_dmg] tiempo_aura 0</pre>

</br>

#### Quitar tags y scoreboards:

<strong>impulso-necesita redstone</strong>
<pre>tag @a[tag=aura_dmg] remove aura_dmg</pre>

<strong>cadena-siempre activo</strong>
<pre>scoreboard objectives remove tiempo_aura</pre>

#### Timer y aviso de habilidad disponible:

Cada jugador tiene su propia puntuación en `tiempo_aura`; el objetivo se comparte, pero los contadores son individuales. No hace falta un objetivo diferente por jugador. La instalación actual pone a cero a todos los portadores conectados: no repitas esa inicialización mientras haya cooldowns en curso. La retirada actual elimina el objetivo completo para todos.

Usa estos cinco bloques en orden, con las flechas siguiendo la secuencia. El primero es **repetición, necesita redstone, incondicional**; los cuatro siguientes son **cadena, siempre activo, incondicional**. Cada comando ocupa un bloque; el descuento se ejecuta una vez por ciclo.

1. Activar con la calavera marcada:

<pre>execute as @a[tag=aura_dmg, scores={tiempo_aura=0}] if items entity @s weapon.mainhand minecraft:skeleton_skull[minecraft:custom_data~{poder:"kill_aura"}] run scoreboard players set @s tiempo_aura 5200</pre>

2. Identificar a quien está a punto de terminar:

<pre>tag @a[tag=aura_dmg, scores={tiempo_aura=1}] add aura_aviso_listo</pre>

3. Descontar el contador:

<pre>execute as @a[scores={tiempo_aura=1..}] run scoreboard players remove @s tiempo_aura 1</pre>

4. Avisar solo a ese jugador cuando llega a cero:

<pre>execute as @a[tag=aura_dmg,tag=aura_aviso_listo,scores={tiempo_aura=0}] run title @s actionbar [{"text":"K","color":"#FF3333"},{"text":"i","color":"#FF6433"},{"text":"l","color":"#FF9533"},{"text":"l","color":"#FFC633"},{"text":" "},{"text":"a","color":"#FFF733"},{"text":"u","color":"#D6FF33"},{"text":"r","color":"#A5FF33"},{"text":"a","color":"#74FF33"},{"text":" "},{"text":"l","color":"#43FF33"},{"text":"i","color":"#33FF54"},{"text":"s","color":"#33FF85"},{"text":"t","color":"#33FFB6"},{"text":"a","color":"#33FFE7"},{"text":" "},{"text":"p","color":"#33E7FF"},{"text":"a","color":"#33B6FF"},{"text":"r","color":"#3385FF"},{"text":"a","color":"#3354FF"},{"text":" "},{"text":"u","color":"#4333FF"},{"text":"s","color":"#7433FF"},{"text":"a","color":"#A533FF"},{"text":"r","color":"#D633FF"}]</pre>

5. Retirar la marca temporal para no repetir el aviso:

<pre>tag @a[tag=aura_aviso_listo] remove aura_aviso_listo</pre>

El mensaje multicolor aparece una vez sobre la barra rápida al terminar cada cooldown, no al iniciar con cero. Los contadores de jugadores desconectados no bajan con este circuito. Si mantienes la calavera en la mano, la habilidad vuelve a activarse en la siguiente ejecución después de llegar a cero.

#### Dar Calavera

<strong>repetición-necesita redstone</strong>
<pre>execute as @a[tag=aura_dmg] unless items entity @s hotbar.* minecraft:skeleton_skull[minecraft:custom_data~{poder:"kill_aura"}] run give @s minecraft:skeleton_skull[minecraft:custom_data={poder:"kill_aura"},minecraft:custom_name=[{text:"Kill aura", color:"red", lore:[[{"text":"El Reloj que controla el tiempo","italic":true}]], obfuscated:true}]]</pre>

#### Uso de la habilidad

Sustituye el bloque de daño anterior por estos **cuatro bloques en orden**, con las flechas siguiendo la secuencia. Conserva un solo circuito de daño para evitar ejecuciones duplicadas.

1. Limpiar marcas de selección anteriores:

<strong>repetición-necesita redstone-incondicional</strong>

<pre>execute at @a run tag @e[tag=aura_objetivo] remove aura_objetivo</pre>

2. Marcar las criaturas permitidas a un máximo de 5 bloques de los portadores activos:

<strong>cadena-siempre activo-incondicional</strong>

<pre>execute at @a[tag=aura_dmg,scores={tiempo_aura=1200..}] as @e[distance=..5] if predicate {type:"minecraft:entity_properties",entity:"this",predicate:{"minecraft:entity_type":["minecraft:blaze","minecraft:bogged","minecraft:breeze","minecraft:creaking","minecraft:creeper","minecraft:drowned","minecraft:elder_guardian","minecraft:ender_dragon","minecraft:endermite","minecraft:evoker","minecraft:ghast","minecraft:guardian","minecraft:hoglin","minecraft:husk","minecraft:illusioner","minecraft:magma_cube","minecraft:parched","minecraft:phantom","minecraft:piglin_brute","minecraft:pillager","minecraft:ravager","minecraft:shulker","minecraft:silverfish","minecraft:skeleton","minecraft:slime","minecraft:stray","minecraft:vex","minecraft:vindicator","minecraft:warden","minecraft:witch","minecraft:wither","minecraft:wither_skeleton","minecraft:zoglin","minecraft:zombie","minecraft:zombie_villager"]}} run tag @s add aura_objetivo</pre>

3. Dañar una sola criatura seleccionada por portador:

<strong>cadena-siempre activo-incondicional</strong>

<pre>execute at @a[tag=aura_dmg,scores={tiempo_aura=1200..}] run damage @n[tag=aura_objetivo,distance=..5] 2 minecraft:indirect_magic</pre>

4. Retirar las marcas temporales:

<strong>cadena-siempre activo-incondicional</strong>

<pre>execute at @a run tag @e[tag=aura_objetivo] remove aura_objetivo</pre>

Mantén cargada la zona del circuito. `execute at` sitúa cada búsqueda en la dimensión y posición del jugador; las marcas se limpian en las dimensiones donde hay jugadores conectados. La etiqueta `aura_objetivo` queda reservada a este circuito. Dos portadores pueden seleccionar la misma criatura; el juego determina cómo se aplica el daño recibido.

#### Limpieza continua de objetos marcados:

Circuito independiente de la entrega y retirada del poder. Primer bloque: **repetición, siempre activo, incondicional**. No necesita una señal externa ni depende de que exista algún portador:

<pre>clear @a[tag=!aura_dmg] minecraft:skeleton_skull[minecraft:custom_data~{poder:"kill_aura"}]</pre>

Después, tres bloques de **cadena, siempre activo, incondicional**, con las flechas siguiendo la secuencia. Cada comando ocupa un bloque:

<pre>execute in minecraft:overworld as @e[type=minecraft:item] if items entity @s contents minecraft:skeleton_skull[minecraft:custom_data~{poder:"kill_aura"}] run kill @s</pre>

<pre>execute in minecraft:the_nether as @e[type=minecraft:item] if items entity @s contents minecraft:skeleton_skull[minecraft:custom_data~{poder:"kill_aura"}] run kill @s</pre>

<pre>execute in minecraft:the_end as @e[type=minecraft:item] if items entity @s contents minecraft:skeleton_skull[minecraft:custom_data~{poder:"kill_aura"}] run kill @s</pre>

Mantén cargada la zona. Todas las cadenas son incondicionales. Puedes usar repetición con redstone si la señal es permanente; un pulso breve no mantiene la limpieza.

La limpieza alcanza inventarios de jugadores conectados sin el tag y objetos marcados tirados en zonas cargadas de las tres dimensiones, aunque su dueño conserve el poder. No elimina proyectiles lanzados.

Solo se eliminan las copias marcadas. Los cofres y el contenido de contenedores portátiles quedan fuera; al recoger una copia sin tener el tag, se limpia del inventario. Los productos fabricados no se detectan.

[Pruebas y decisiones](../../extras/laboratorios/kill-aura.md) · [Volver a superpoderes](README.md)
