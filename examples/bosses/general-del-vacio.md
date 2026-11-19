# General del Vacío

Zombie de combate cercano, ampliado a escala 2.4 y equipado con espada y armadura completa de netherite. Su secuencia aumenta la vida, el alcance y los atributos de ataque y desplazamiento. La resistencia observada combina varias configuraciones; no se atribuye aquí a una causa única sin una comparación en el juego.

## Configuración aplicada

| Propiedad | Valor escrito en los comandos |
| --- | --- |
| Entidad y etiqueta | `minecraft:zombie`, `boss_void_general` |
| Vida máxima y vida inicial | 450 |
| Escala | 2.4 |
| attack_damage | 18 |
| movement_speed | 0.34 |
| armor base | 18 |
| armor_toughness base | 12 |
| knockback_resistance | 0.9 |
| attack_knockback | 4 |
| follow_range | 70 |
| step_height | 5 |

## Equipo y efectos

- Espada de netherite: Sharpness 7, Sweeping Edge 5, Fire Aspect 2 y Unbreaking 5.
- Armadura completa de netherite: Protection 5 y Unbreaking 5; las botas añaden Feather Falling 20.
- Efecto `fire_resistance` de duración infinita.
- La invocación marca PersistenceRequired y CanBreakDoors como true, y muestra el nombre «El General del Vacío» en rojo oscuro.

La cifra 12 corresponde a `armor_toughness`, no a un efecto Resistance. El valor base de armor y el equipo se documentan por separado; la ficha no calcula una reducción final de daño. Soul Fire era una idea visual de la ficha anterior: no hay un comando de partículas en esta secuencia.

## Montaje

Invocación relativa a la posición de ejecución. La secuencia selecciona una entidad mediante tag, cercanía y límite de una; los comandos de equipo `bosses` están en las notas al final. Conservar la configuración de bloques indicada en cada paso.

Estado de desarrollo: terminado según las pruebas históricas del autor. La versión exacta de esas pruebas no está registrada en esta ficha; la compatibilidad con una versión estable posterior se revisa por separado.

### Comandos

<strong>impulso-necesita redstone</strong>

<pre>summon minecraft:zombie ~ ~1 ~ {Tags:["boss_void_general"],PersistenceRequired:true,CanBreakDoors:true,CustomName:{text:"El General del Vacío",color:"dark_red",bold:true},CustomNameVisible:true}</pre>

<strong>impulso-necesita redstone (Validado con comparador previamente)</strong>
<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:scale base set 2.4</pre>

<strong>cadena-siempre activo</strong>

<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:max_health base set 450</pre>

<pre>data merge entity @e[tag=boss_void_general,limit=1,sort=nearest] {Health:450f}</pre>

<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:attack_damage base set 18</pre>

<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:movement_speed base set 0.34</pre>

<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:armor base set 18</pre>

<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:armor_toughness base set 12</pre>

<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:knockback_resistance base set 0.9</pre>

<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:attack_knockback base set 4</pre>

<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:follow_range base set 70</pre>

<pre>attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:step_height base set 5</pre>

<pre>effect give @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:fire_resistance infinite 0 true</pre>

Aplicacion de armadura al boss:

<pre>item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] weapon.mainhand with minecraft:netherite_sword[minecraft:enchantments={sharpness:7,sweeping_edge:5,fire_aspect:2,unbreaking:5}]</pre>

<pre>item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] armor.head with minecraft:netherite_helmet[minecraft:enchantments={protection:5,unbreaking:5}]</pre>

<pre>item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] armor.chest with minecraft:netherite_chestplate[minecraft:enchantments={protection:5,unbreaking:5}]</pre>

<pre>item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] armor.legs with minecraft:netherite_leggings[minecraft:enchantments={protection:5,unbreaking:5}]</pre>

<pre>item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] armor.feet with minecraft:netherite_boots[minecraft:enchantments={protection:5,feather_falling:20,unbreaking:5}]</pre>


---

### Notas

Si deseas evitar que se golpeen entre multiples bosses coloca comandos de team, por ejemplo:

<strong>impulso-necesita redstone</strong>
<pre>team add bosses</pre>


Y si deseas agregar un boss al equipo le colocas al final de la secuencia un bloque de:

<strong>cadena-siempre activo</strong>
<pre>team join bosses @e[tag=boss_void_general]</pre>
<pre>team join bosses @e[tag=boss_colossus]</pre>
<pre>team join bosses @e[tag=boss_hunter]</pre>
<pre>team join bosses @e[tag=boss_necromancer]</pre>





[Volver a bosses](README.md)
