# Cazador

Stray equipado con un arco de Power 100 y un peto de diamante. La configuración conserva un combatiente a distancia de escala 1.6 y 200 de vida. El peto es la única pieza de armadura equipada por estos comandos.

## Configuración aplicada

| Propiedad | Valor escrito en los comandos |
| --- | --- |
| Entidad y etiqueta | `minecraft:stray`, `boss_hunter` |
| Vida máxima y vida inicial | 200 |
| Escala | 1.6 |
| attack_damage | 20 |
| movement_speed | 0.32 |
| armor base | 10 |
| knockback_resistance | 0.4 |
| follow_range | 70 |

El valor 20 es el atributo attack_damage asignado; no se presenta como medición del daño final de una flecha. La secuencia no asigna armor_toughness ni aplica un efecto Resistance.

## Equipo y efectos

- Arco: Power 100, Punch 2, Flame 1 y Unbreaking 5.
- Peto de diamante: Protection 10 y Unbreaking 5.
- Efecto `fire_resistance` de duración infinita.
- Nombre «El Cazador» en aguamarina oscura, visible; PersistenceRequired true.
- Se incorpora al equipo `bosses`, que debe existir previamente.

## Cómo montarlo

Adapta la posición de ejemplo `18 59 14`; el stray aparece un bloque por encima. Activa el impulso de escala después de invocarlo. La cadena fija su vida máxima en 200, llena esa vida y aplica los atributos antes de equipar el arco y el peto.

Copia un comando por bloque siguiendo el orden de abajo. Para la configuración usa un solo ejemplar con la etiqueta de esta ficha: los selectores con `limit=1,sort=nearest` eligen el más cercano a cada bloque. Consulta la [preparación del equipo bosses](README.md#preparación-del-equipo-bosses) antes de usar `team join`.

## Qué comprobar

Al terminar verás «El Cazador» a escala 1.6 con el arco en la mano y un peto de diamante. Su ataque a distancia depende del arco encantado; el 20 de la tabla corresponde al atributo de ataque del mob.

Estado de desarrollo: terminado según las pruebas históricas del autor. La versión exacta de esas pruebas no está registrada en esta ficha; la compatibilidad con una versión estable posterior se revisa por separado.

### Comandos

<strong>impulso-necesita redstone</strong>

<pre>execute positioned 18 59 14 run summon minecraft:stray ~ ~1 ~ {Tags:["boss_hunter"],PersistenceRequired:true,CustomName:{text:"El Cazador",color:"dark_aqua",bold:true},CustomNameVisible:true}</pre>

<strong>impulso-necesita redstone (Validado con comparador previamente)</strong>
<pre>attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:scale base set 1.6</pre>

<strong>cadena-siempre activo</strong>

<pre>attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:max_health base set 200</pre>

<pre>data merge entity @e[tag=boss_hunter,limit=1,sort=nearest] {Health:200f}</pre>

<pre>attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:attack_damage base set 20</pre>

<pre>attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:armor base set 10</pre>

<pre>attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:movement_speed base set 0.32</pre>

<pre>attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:follow_range base set 70</pre>

<pre>attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:knockback_resistance base set 0.4</pre>

<pre>effect give @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:fire_resistance infinite 0 true</pre>

**Equipamiento**

<pre>item replace entity @e[tag=boss_hunter,limit=1,sort=nearest] weapon.mainhand with minecraft:bow[minecraft:enchantments={power:100,punch:2,flame:1,unbreaking:5}]</pre>

<pre>item replace entity @e[tag=boss_hunter,limit=1,sort=nearest] armor.chest with minecraft:diamond_chestplate[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

**Pertenencia al equipo**

<pre>team join bosses @e[tag=boss_hunter]</pre>

[Volver a bosses](README.md)
