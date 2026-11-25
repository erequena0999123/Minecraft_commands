# Doctor Strange

Simulación de paralización de entidades cercanas mediante `NoAI`, para jugadores con `doctor_strange` que activan el poder sosteniendo el Reloj del Tiempo marcado en la mano principal.

Estado: implementación cerrada con las cuatro mejoras acordadas. Incluye activación con reloj marcado, paralización y restauración, limpieza del objeto y aviso individual de disponibilidad.

## Activación y temporizador

- La instalación crea `tiempo_parado` y lo inicia en cero para los jugadores con el tag.
- Con contador cero y un reloj marcado con `poder:"doctor_strange"` en la mano principal, el sistema fija el contador en 5200. La cadena lo reduce mientras sea positivo.
- El área se mantiene mientras `tiempo_parado=2400..`, con un radio de 50 bloques alrededor de cada portador activo.
- Las criaturas registradas recuperan su IA cuando dejan de estar dentro del área de cualquier portador activo, también al terminar el efecto. Las que ya tenían `NoAI:true` se mantienen en su estado previo.

El sistema se aplica a criaturas con el dato `Health`, hostiles y no hostiles, y excluye jugadores. Funciona en las tres dimensiones vanilla con las entidades cargadas. Actúa sobre su IA; no detiene el tiempo global ni toda la física del mundo. La entrega del reloj sigue limitada por el tag.

El reloj del poder lleva `minecraft:custom_data={poder:"doctor_strange"}`. Un reloj normal no activa la habilidad ni impide recibir el marcado. La entrega comprueba únicamente la barra rápida. Una vez activado, el efecto continúa según el contador aunque se cambie el objeto de la mano.

### Comandos

Sustituye `NOMBRE_JUGADOR` por el nombre exacto del jugador que recibirá el poder antes de copiar el comando. El marcador no se escribe literalmente en el juego. Cada comando ocupa un bloque independiente, sin `/` inicial; para el chat del juego añade esa barra. Las cadenas de instalación y retirada indicadas sin condición se configuran como incondicionales, con las flechas siguiendo el orden mostrado.

#### Colocar tags y scoreboards:

<strong>impulso-necesita redstone</strong>

<pre>tag NOMBRE_JUGADOR add doctor_strange</pre>

<strong>cadena-siempre activo</strong>

<pre>scoreboard objectives add tiempo_parado dummy</pre>
<pre>scoreboard players set @a[tag=doctor_strange] tiempo_parado 0</pre>

</br>

#### Quitar tags y scoreboards:

<strong>impulso-necesita redstone</strong>
<pre>tag @a[tag=doctor_strange] remove doctor_strange</pre>

<strong>cadena-siempre activo</strong>
<pre>scoreboard objectives remove tiempo_parado</pre>

#### Timer y aviso de habilidad disponible:

Cada jugador tiene su propia puntuación en `tiempo_parado`. No hace falta crear un objetivo por jugador. La instalación actual pone a cero a todos los portadores conectados: no repitas esa inicialización mientras haya recargas en curso. La retirada actual elimina el objetivo completo para todos.

Usa estos cinco bloques en orden. El primero es **repetición, necesita redstone, incondicional**; los cuatro siguientes son **cadena, siempre activo, incondicional**. Orienta las flechas siguiendo la secuencia y coloca un comando por bloque. El contador se descuenta una sola vez por ciclo.

1. Activar con el reloj marcado:

<pre>execute as @a[tag=doctor_strange,scores={tiempo_parado=0}] if items entity @s weapon.mainhand minecraft:clock[minecraft:custom_data~{poder:"doctor_strange"}] run scoreboard players set @s tiempo_parado 5200</pre>

2. Identificar a quien está a punto de terminar la recarga:

<pre>tag @a[tag=doctor_strange,scores={tiempo_parado=1}] add ds_aviso_listo</pre>

3. Descontar el contador:

<pre>execute as @a[scores={tiempo_parado=1..}] run scoreboard players remove @s tiempo_parado 1</pre>

4. Mostrar el aviso solo al jugador cuya recarga ha terminado:

<pre>execute as @a[tag=doctor_strange,tag=ds_aviso_listo,scores={tiempo_parado=0}] run title @s actionbar [{"text":"D","color":"#FF3333"},{"text":"o","color":"#FF6433"},{"text":"c","color":"#FF9533"},{"text":"t","color":"#FF9533"},{"text":"o","color":"#FFC633"},{"text":"r","color":"#FFF733"},{"text":" "},{"text":"S","color":"#D6FF33"},{"text":"t","color":"#A5FF33"},{"text":"r","color":"#A5FF33"},{"text":"a","color":"#74FF33"},{"text":"n","color":"#43FF33"},{"text":"g","color":"#33FF54"},{"text":"e","color":"#33FF85"},{"text":" "},{"text":"l","color":"#33FF85"},{"text":"i","color":"#33FFB6"},{"text":"s","color":"#33FFE7"},{"text":"t","color":"#33E7FF"},{"text":"o","color":"#33B6FF"},{"text":" "},{"text":"p","color":"#33B6FF"},{"text":"a","color":"#3385FF"},{"text":"r","color":"#3354FF"},{"text":"a","color":"#4333FF"},{"text":" "},{"text":"u","color":"#7433FF"},{"text":"s","color":"#7433FF"},{"text":"a","color":"#A533FF"},{"text":"r","color":"#D633FF"}]</pre>

5. Retirar la marca temporal para no repetir el aviso:

<pre>tag @a[tag=ds_aviso_listo] remove ds_aviso_listo</pre>

El mensaje «Doctor Strange listo para usar» aparece una vez sobre la barra rápida, con el mismo arcoíris estático de Kill aura, al pasar de 1 a 0. No avisa al instalar con cero ni al terminar solo la fase de paralización. Los contadores de jugadores desconectados no bajan con este circuito. Si mantienes el reloj marcado en la mano, el poder vuelve a activarse en la siguiente ejecución después del aviso.

#### Dar Reloj:

<strong>repetición-necesita redstone</strong>
<pre>execute as @a[tag=doctor_strange] unless items entity @s hotbar.* minecraft:clock[minecraft:custom_data~{poder:"doctor_strange"}] run give @s minecraft:clock[minecraft:custom_data={poder:"doctor_strange"},minecraft:custom_name={"text":"","color":"blue","italic":false,"extra":[{"text":"X","obfuscated":true},{"text":" Reloj del Tiempo "},{"text":"X","obfuscated":true}]},minecraft:lore=[{"text":"Uso","color":"gold","bold":true,"italic":false},{"text":"Sostén el reloj en la mano principal.","color":"white","italic":false},{"text":"Al estar listo, paraliza a las criaturas cercanas.","color":"white","italic":false},{"text":""},{"text":"Un relojero atrapó un instante entre sus agujas.","color":"gray","italic":true},{"text":"Al liberarlo, todo ser cercano queda inmóvil.","color":"gray","italic":true}]]</pre>

El autor probó en Minecraft la presentación de «Reloj del Tiempo» y aprobó el nombre con adornos ofuscados, las instrucciones de uso y la historia del objeto.

#### Paralizar y restaurar criaturas en las tres dimensiones:

Usa **un único circuito de ocho bloques** para el área y la restauración, independiente de la entrega y del temporizador.

El bloque 1 es **repetición, siempre activo, incondicional**. Los bloques 2 a 8 son **cadena, siempre activo, incondicional**. Cada comando ocupa un bloque; orienta las flechas siguiendo el orden. Mantén cargada la zona donde se construye el circuito.

**Bloque 1: Registrar las criaturas que no estaban ya sin IA.**

<pre>execute at @a[tag=doctor_strange,scores={tiempo_parado=2400..}] as @e[type=!minecraft:player,tag=!ds_restaurar,distance=..50] if data entity @s Health unless data entity @s {NoAI:true} run tag @s add ds_restaurar</pre>

**Bloque 2: Paralizar las registradas que siguen cerca de un portador activo.**

<pre>execute at @a[tag=doctor_strange,scores={tiempo_parado=2400..}] as @e[tag=ds_restaurar,distance=..50] run data merge entity @s {NoAI:true}</pre>

**Bloques 3 a 5: Restaurar las que ya no tienen ningún portador activo a 50 bloques.**

<pre>execute in minecraft:overworld as @e[tag=ds_restaurar] at @s unless entity @a[tag=doctor_strange,scores={tiempo_parado=2400..},distance=..50] run data merge entity @s {NoAI:false}</pre>

<pre>execute in minecraft:the_nether as @e[tag=ds_restaurar] at @s unless entity @a[tag=doctor_strange,scores={tiempo_parado=2400..},distance=..50] run data merge entity @s {NoAI:false}</pre>

<pre>execute in minecraft:the_end as @e[tag=ds_restaurar] at @s unless entity @a[tag=doctor_strange,scores={tiempo_parado=2400..},distance=..50] run data merge entity @s {NoAI:false}</pre>

**Bloques 6 a 8: Finalizar el seguimiento de las restauradas.**

<pre>execute in minecraft:overworld as @e[tag=ds_restaurar] at @s unless entity @a[tag=doctor_strange,scores={tiempo_parado=2400..},distance=..50] run tag @s remove ds_restaurar</pre>

<pre>execute in minecraft:the_nether as @e[tag=ds_restaurar] at @s unless entity @a[tag=doctor_strange,scores={tiempo_parado=2400..},distance=..50] run tag @s remove ds_restaurar</pre>

<pre>execute in minecraft:the_end as @e[tag=ds_restaurar] at @s unless entity @a[tag=doctor_strange,scores={tiempo_parado=2400..},distance=..50] run tag @s remove ds_restaurar</pre>

La etiqueta `ds_restaurar` está reservada a este circuito. No la retires manualmente de criaturas paralizadas: permite recuperarlas.

Mantén el circuito activo durante la recarga y después de retirar el poder. La restauración revisa las tres dimensiones vanilla aunque alguna se quede sin jugadores, pero solo procesa entidades cargadas. Una criatura descargada se procesa al volver a cargarse.

#### Limpieza continua de relojes marcados:

Usa un circuito independiente. Primer bloque: **repetición, siempre activo, incondicional**. Los tres siguientes: **cadena, siempre activo, incondicional**, con las flechas siguiendo el orden. Cada comando ocupa un bloque.

<pre>clear @a[tag=!doctor_strange] minecraft:clock[minecraft:custom_data~{poder:"doctor_strange"}]</pre>

<pre>execute in minecraft:overworld as @e[type=minecraft:item] if items entity @s contents minecraft:clock[minecraft:custom_data~{poder:"doctor_strange"}] run kill @s</pre>

<pre>execute in minecraft:the_nether as @e[type=minecraft:item] if items entity @s contents minecraft:clock[minecraft:custom_data~{poder:"doctor_strange"}] run kill @s</pre>

<pre>execute in minecraft:the_end as @e[type=minecraft:item] if items entity @s contents minecraft:clock[minecraft:custom_data~{poder:"doctor_strange"}] run kill @s</pre>

Mantén cargada la zona del circuito y déjalo activo también después de retirar el poder. Elimina solo relojes con la marca del poder: de los inventarios de jugadores conectados sin `doctor_strange` y del suelo en zonas cargadas de las tres dimensiones vanilla. También elimina un reloj marcado que deje caer el propio portador.

Los relojes normales se conservan. La limpieza no inspecciona cofres ni contenedores portátiles; una copia guardada se limpia al recogerla sin tener el tag. Tampoco reconoce los relojes antiguos sin marca ni los productos fabricados con ellos.

[Pruebas y decisiones](../../extras/laboratorios/doctor-strange.md) · [Volver a superpoderes](README.md)
