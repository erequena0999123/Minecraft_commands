# Coloso

Husk gigante orientado a resistir y distraer, con 800 de vida y escala 3. Usa armadura completa de netherite y no recibe un arma en la secuencia. Su attack_damage configurado es 5, por debajo del General del Vacío; el diseño conserva su papel de tanque.

## Configuración aplicada

| Propiedad | Valor escrito en los comandos |
| --- | --- |
| Entidad y etiqueta | `minecraft:husk`, `boss_colossus` |
| Vida máxima y vida inicial | 800 |
| Escala | 3 |
| attack_damage | 5 |
| movement_speed | 0.43 |
| armor base | 30 |
| armor_toughness base | 20 |
| knockback_resistance | 1 |
| follow_range | 100 |
| step_height | 5 |

## Equipo y efectos

- Armadura completa de netherite: Protection 10 y Unbreaking 5; botas con Feather Falling 20.
- Efecto `fire_resistance` de duración infinita.
- Nombre «El Coloso» en gris oscuro, visible; PersistenceRequired true.
- Se incorpora al equipo `bosses`, que debe existir previamente.

La dureza aplicada es 20. El antiguo texto «Resistencia 12» no coincidía con el comando. No hay un efecto Resistance en esta secuencia ni una equivalencia establecida con la resistencia efectiva de otros bosses.

## Cómo montarlo

Cambia la posición de ejemplo `15 60 -15` por el punto de tu mundo. El husk aparece un bloque por encima. Tras el impulso de invocación, activa el impulso de escala y sigue la cadena: configura primero los 800 puntos de vida y después los atributos, el efecto y las cuatro piezas de armadura.

Copia un comando por bloque siguiendo el orden de abajo. Para la configuración usa un solo ejemplar con la etiqueta de esta ficha: los selectores con `limit=1,sort=nearest` eligen el más cercano a cada bloque. Consulta la [preparación del equipo bosses](README.md#preparación-del-equipo-bosses) antes de usar `team join`.

## Qué comprobar

Se reconoce por su tamaño triple, la armadura completa y las manos sin arma asignada. Para interpretar su aguante, distingue la armadura base de 30, la dureza de 20 y los encantamientos de sus piezas.

Estado de desarrollo: terminado según las pruebas históricas del autor. La versión exacta de esas pruebas no está registrada en esta ficha; la compatibilidad con una versión estable posterior se revisa por separado.

### Comandos

<strong>impulso-necesita redstone</strong>

<pre>execute positioned 15 60 -15 run summon minecraft:husk ~ ~1 ~ {Tags:["boss_colossus"],PersistenceRequired:true,CustomName:{text:"El Coloso",color:"dark_gray",bold:true},CustomNameVisible:true}</pre>

<strong>impulso-necesita redstone (Validado con comparador previamente)</strong>
<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:scale base set 3</pre>

<strong>cadena-siempre activo</strong>

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:max_health base set 800</pre>

<pre>data merge entity @e[tag=boss_colossus,limit=1,sort=nearest] {Health:800f}</pre>

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:attack_damage base set 5</pre>

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:armor base set 30</pre>

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:armor_toughness base set 20</pre>

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:knockback_resistance base set 1</pre>

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:movement_speed base set 0.43</pre>

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:follow_range base set 100</pre>

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:step_height base set 5</pre>

<pre>effect give @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:fire_resistance infinite 0 true</pre>

**Equipamiento**

<pre>item replace entity @e[tag=boss_colossus,limit=1,sort=nearest] armor.head with minecraft:netherite_helmet[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

<pre>item replace entity @e[tag=boss_colossus,limit=1,sort=nearest] armor.chest with minecraft:netherite_chestplate[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

<pre>item replace entity @e[tag=boss_colossus,limit=1,sort=nearest] armor.legs with minecraft:netherite_leggings[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

<pre>item replace entity @e[tag=boss_colossus,limit=1,sort=nearest] armor.feet with minecraft:netherite_boots[minecraft:enchantments={protection:10,feather_falling:20,unbreaking:5}]</pre>

**Pertenencia al equipo**

<pre>team join bosses @e[tag=boss_colossus]</pre>

[Volver a bosses](README.md)
