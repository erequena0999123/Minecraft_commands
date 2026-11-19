# Spider-Man

Poder para jugadores identificados con `spider_man`: aplica levitación según los bloques próximos al personaje, entrega bolas de nieve y genera telarañas temporales mediante entidades auxiliares.

## Activación y recursos

La instalación asigna el tag al jugador indicado y crea `tiempo_telarana`. La entrega está limitada a jugadores con `spider_man`: comprueba si tienen una bola marcada con `poder:"spider_man"` en la barra rápida y entrega dos cuando no encuentra ninguna. Una bola normal no impide la reposición. El objeto se llama «Telarañas», con «Tela» en rojo y «rañas» en azul, sin cursiva.

## Mecánicas documentadas

- Escalada mediante levitación de 1 o 2 segundos, con amplificador 1: pared frontal con dirección horizontal y bloque sobre el portador. Saltar es opcional.
- La levitación deja de renovarse al perder ambas detecciones o el tag y termina al agotarse la duración aplicada.
- La estela se genera en la posición real de la bola de nieve, sin desplazamiento local superior; sigue su trayectoria.
- La cadena comprueba la marca `poder:"spider_man"` en el objeto de cada proyectil y que su lanzador sea un jugador con `spider_man`. Los proyectiles que cumplen crean marcadores `reloj_telarana` y las cadenas colocan telarañas en sus posiciones.
- La movilidad cerca de los marcadores combina un bono de velocidad de 0.8, Weaving I renovado durante 5 segundos y gravedad ×4, con radio de 2 bloques.
- Los marcadores acumulan contador y se eliminan desde 100 junto con la telaraña de su posición. La duración depende de la frecuencia del circuito.

La identidad del objeto se comprueba en `Item.components."minecraft:custom_data"` de la bola lanzada; el nombre visible no autoriza el poder. `on origin` comprueba al lanzador después de fijar la posición del proyectil, por lo que la red sigue la bola y no el objeto que el jugador sostenga después de lanzarla. Las bolas sin la marca no generan redes aunque se llamen «Telarañas».

### Comandos

Sustituye `NOMBRE_JUGADOR` por el nombre exacto del jugador que recibirá el poder antes de copiar el comando. El marcador no se escribe literalmente en el juego.

#### Colocar tags y scoreboards:
<p>
<strong>impulso-necesita redstone</strong>

<pre>tag NOMBRE_JUGADOR add spider_man</pre>

<strong>cadena-siempre activo</strong>

<pre>scoreboard objectives add tiempo_telarana dummy</pre>

</br>

#### Retirar el poder a un jugador:

<strong>impulso-necesita redstone</strong>

<pre>tag NOMBRE_JUGADOR remove spider_man</pre>

Este es el único comando necesario para la retirada individual. Sustituye el marcador por el nombre exacto del jugador. Mantén funcionando los circuitos de movilidad, retirada de telarañas y limpieza de objetos. Conserva el objetivo de scoreboard `tiempo_telarana`, de tipo `dummy`: es compartido y los marcadores existentes lo necesitan para terminar su duración. El objetivo se conserva aunque no queden portadores; no hace falta esperar a que terminen las redes para quitar el tag. La entrega y la generación de redes requieren el tag, por lo que dejan de autorizar al jugador que lo pierde.

La limpieza continua elimina de su inventario las bolas con la marca del poder. Los modificadores propios de velocidad y gravedad se retiran en la siguiente ejecución del circuito de movilidad; Weaving puede conservar hasta cinco segundos de duración. Las telarañas ya creadas terminan mediante su temporizador habitual. La levitación ya aplicada termina al agotarse su duración restante de uno o dos segundos.

#### Caminar por paredes:

La escalada se activa al acercarse a una pared situada delante del portador según su orientación horizontal, o al quedar bajo un bloque dos unidades sobre sus pies. Saltar es opcional. Bajar la mirada hacia el suelo no inclina la comprobación frontal; la detección superior es independiente de la mirada.

**Bloque 1: repetición, necesita redstone, incondicional.** Mantener señal continua:

<pre>execute as @a[tag=spider_man] at @s rotated ~ 0 unless block ^ ^1 ^1 minecraft:air run effect give @s minecraft:levitation 1 1 true</pre>

**Bloque 2: cadena, siempre activo, incondicional.** Orientar las flechas para continuar la secuencia:

<pre>execute as @a[tag=spider_man] at @s unless block ~ ~2 ~ minecraft:air run effect give @s minecraft:levitation 2 1 true</pre>

Conservar únicamente estos dos bloques de escalada. Cuando dejan de cumplirse ambas detecciones, la levitación deja de renovarse y se agota con su duración restante: hasta un segundo por pared y hasta dos por techo. Si se retira el tag ocurre lo mismo. Mantener cargada la zona del circuito.

#### Dar bolas de nieve:

<strong>repetición-necesita redstone</strong>

<pre>execute as @a[tag=spider_man] unless items entity @s hotbar.* minecraft:snowball[minecraft:custom_data~{poder:"spider_man"}] run give @s minecraft:snowball[minecraft:custom_data={poder:"spider_man"},minecraft:custom_name=[{text:"Tela",color:"red",italic:false},{text:"rañas",color:"blue",italic:false}]] 2</pre>

</br>

#### Efecto de telarañas con bolas de nieve:

<strong>repetición-necesita redstone</strong>

<pre>execute if entity @a[tag=spider_man]</pre>

<strong>cadena-siempre activo-condicional</strong>
<pre>execute as @e[type=minecraft:snowball,nbt={Item:{components:{"minecraft:custom_data":{poder:"spider_man"}}}}] at @s on origin if entity @s[type=minecraft:player,tag=spider_man] if block ~ ~ ~ minecraft:air run summon minecraft:interaction ~ ~ ~ {Tags:["reloj_telarana"],Passengers:[{text:""}]}</pre>

<strong>cadena-siempre activo-incondicional</strong>

<pre>execute at @e[tag=reloj_telarana] run setblock ~ ~ ~ minecraft:cobweb replace</pre>
<pre>execute as @e[tag=reloj_telarana] at @s run scoreboard players add @s tiempo_telarana 1</pre>
<pre>execute as @e[tag=reloj_telarana, scores={tiempo_telarana=100..}] at @s run fill ~ ~ ~ ~ ~ ~ minecraft:air replace minecraft:cobweb</pre>
<pre>execute as @e[tag=reloj_telarana, scores={tiempo_telarana=100..}] run kill @s</pre>

Mantén alimentado y cargado este circuito aunque no haya jugadores con el tag. Las cadenas que colocan redes, incrementan el contador y retiran bloques y marcadores siguen siendo incondicionales: deben continuar cuando ya no se generen bolas válidas. El objetivo `tiempo_telarana` tiene que existir durante todo ese seguimiento.

</p>

#### Movilidad junto a las telarañas del poder:

Circuito independiente de cinco bloques, en el orden mostrado. El primero es **repetición, siempre activo, incondicional**. Los cuatro siguientes son **cadena, siempre activo, incondicional**. Un comando por bloque y flechas siguiendo la secuencia.

Los jugadores con `spider_man` reciben la mejora cuando hay un marcador `reloj_telarana` a un máximo de 2 bloques de un punto situado 0.9 bloques sobre sus pies. Se conserva este margen alrededor de las redes: no es contacto exclusivo con cobweb ni se aplica a telarañas manuales sin marcador.

1. Retirar el modificador de velocidad anterior:

<pre>execute as @a run attribute @s minecraft:movement_speed modifier remove poderes:spider_red</pre>

2. Aplicar el bono de velocidad de 0.8 cerca de las redes:

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..2] run attribute @s minecraft:movement_speed modifier add poderes:spider_red 0.8 add_multiplied_total</pre>

3. Renovar Weaving I durante cinco segundos, sin partículas:

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..2] run effect give @s minecraft:weaving 5 0 true</pre>

4. Retirar el modificador de gravedad anterior:

<pre>execute as @a run attribute @s minecraft:gravity modifier remove poderes:spider_caida</pre>

5. Aplicar gravedad ×4 cerca de las redes:

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..2] run attribute @s minecraft:gravity modifier add poderes:spider_caida 3 add_multiplied_total</pre>

Los modificadores propios no cambian los valores base ni eliminan modificadores ajenos. La velocidad y la gravedad adicionales dejan de reañadirse en el siguiente ciclo al perder el tag o salir del radio. Dentro del radio la gravedad también modifica el salto y la caída fuera del bloque de telaraña. Weaving puede permanecer hasta cinco segundos después de salir; conserva su comportamiento vanilla de generar telarañas al morir.

Mantén cargado y activo el circuito, también después de retirar el poder: los comandos de retirada alcanzan a todos los jugadores conectados aunque hayan perdido el tag. No acumules este circuito con las variantes de prueba anteriores. Si lo apagas mientras conserva modificadores un jugador, estos requieren retirada manual; consulta el laboratorio para desmontar la instalación. Los jugadores desconectados se procesan al volver con el circuito activo.

#### Limpieza continua de objetos marcados:

Circuito independiente de la entrega y retirada del poder. Primer bloque: **repetición, siempre activo, incondicional**. No necesita una señal externa ni depende de que exista algún portador:

<pre>clear @a[tag=!spider_man] minecraft:snowball[minecraft:custom_data~{poder:"spider_man"}]</pre>

Después, tres bloques de **cadena, siempre activo, incondicional**, con las flechas siguiendo la secuencia. Cada comando ocupa un bloque:

<pre>execute in minecraft:overworld as @e[type=minecraft:item] if items entity @s contents minecraft:snowball[minecraft:custom_data~{poder:"spider_man"}] run kill @s</pre>

<pre>execute in minecraft:the_nether as @e[type=minecraft:item] if items entity @s contents minecraft:snowball[minecraft:custom_data~{poder:"spider_man"}] run kill @s</pre>

<pre>execute in minecraft:the_end as @e[type=minecraft:item] if items entity @s contents minecraft:snowball[minecraft:custom_data~{poder:"spider_man"}] run kill @s</pre>

Mantén cargada la zona. Todas las cadenas son incondicionales. Puedes usar repetición con redstone si la señal es permanente; un pulso breve no mantiene la limpieza.

La limpieza alcanza inventarios de jugadores conectados sin el tag y objetos marcados tirados en zonas cargadas de las tres dimensiones, aunque su dueño conserve el poder. No elimina proyectiles lanzados.

El nombre visible no interviene en la limpieza: se comprueba la marca `poder:"spider_man"`. Las bolas normales, incluso renombradas a mano, se conservan.

Solo se eliminan las copias marcadas. Los cofres y el contenido de contenedores portátiles quedan fuera; al recoger una copia sin tener el tag, se limpia del inventario. Los productos fabricados no se detectan.

[Pruebas y decisiones](../../extras/laboratorios/spider-man.md) · [Volver a superpoderes](README.md)
