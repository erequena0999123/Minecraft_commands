# Nigromante

Evoker ampliado a escala 1.8, con 300 de vida y una habilidad de daño cercano ejecutada por un bloque de repetición separado. La secuencia conserva la entidad base y añade el aura mediante la etiqueta `aura_dmg_boss`.

## Configuración aplicada

| Propiedad | Valor escrito en los comandos |
| --- | --- |
| Entidad y etiquetas | `minecraft:evoker`, `boss_necromancer`, `aura_dmg_boss` |
| Vida máxima y vida inicial | 300 |
| Escala | 1.8 |
| attack_damage | 20 |
| movement_speed | 0.26 |
| armor base | 8 |
| follow_range | 150 |

El valor 20 identifica el atributo asignado, no una medición del daño de todos los ataques propios del evoker. No se equipa armadura ni arma, no se asigna armor_toughness y no se aplica un efecto Resistance.

## Habilidad y efectos

- El bucle se posiciona en cada entidad con `aura_dmg_boss` y ordena 2 de daño de tipo `indirect_magic` al jugador más cercano dentro de 5 bloques.
- Esa cifra es por ejecución del comando, no un daño por segundo calculado. La frecuencia depende del circuito de repetición.
- Efecto `fire_resistance` de duración infinita.
- Nombre «El Nigromante» en morado oscuro, visible; PersistenceRequired true.
- Se incorpora al equipo `bosses`, que debe existir previamente.

## Cómo montarlo

Cambia la posición de ejemplo `-15 61 19`; el evoker aparece un bloque por encima. Activa el segundo impulso para la escala y continúa con la cadena de vida, atributos y resistencia al fuego. Instala aparte el bloque de repetición del aura con su propia señal.

Copia un comando por bloque siguiendo el orden de abajo. Para la configuración usa un solo ejemplar con la etiqueta de esta ficha: los selectores con `limit=1,sort=nearest` eligen el más cercano a cada bloque. Consulta la [preparación del equipo bosses](README.md#preparación-del-equipo-bosses) antes de usar `team join`.

## Qué comprobar

Con la señal del aura apagada, el evoker conserva su configuración inicial. Al encenderla, cada entidad con `aura_dmg_boss` intenta dañar al jugador más cercano dentro de cinco bloques. Puedes comprobar ese cambio sin volver a invocar al boss.

Estado de desarrollo: terminado según las pruebas históricas del autor. La versión exacta de esas pruebas no está registrada en esta ficha; la compatibilidad con una versión estable posterior se revisa por separado.

### Comandos

<strong>impulso-necesita redstone</strong>

<pre>execute positioned -15 61 19 run summon minecraft:evoker ~ ~1 ~ {Tags:["boss_necromancer", "aura_dmg_boss"],PersistenceRequired:true,CustomName:{text:"El Nigromante",color:"dark_purple",bold:true},CustomNameVisible:true}</pre>

<strong>impulso-necesita redstone (Validado con comparador previamente)</strong>
<pre>attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:scale base set 1.8</pre>

<strong>cadena-siempre activo</strong>

<pre>attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:max_health base set 300</pre>

<pre>data merge entity @e[tag=boss_necromancer,limit=1,sort=nearest] {Health:300f}</pre>

<pre>attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:attack_damage base set 20</pre>

<pre>attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:armor base set 8</pre>

<pre>attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:movement_speed base set 0.26</pre>

<pre>attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:follow_range base set 150</pre>

<pre>effect give @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:fire_resistance infinite 0 true</pre>


<strong>repetición-necesita redstone</strong>

<pre>execute at @e[tag=aura_dmg_boss] run damage @n[type=minecraft:player, distance=..5] 2 minecraft:indirect_magic</pre>


**Pertenencia al equipo**

<pre>team join bosses @e[tag=boss_necromancer]</pre>

[Volver a bosses](README.md)
