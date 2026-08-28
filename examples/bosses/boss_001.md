# BOSS-001

### Nombre

General del Vacio

### Entidad

Zombie

### Estado

Terminado

---

### Vida

450

---

### Escala

2.4

---

### Daño

18

---

### Velocidad

0.34

---

### Armadura

Full netherite

18

### Resistencia

12

---

### Arma

Netherite Sword

---

### IA

Persigue jugadores rango de 70

---

### Partículas

Soul Fire

---

### Sonidos

Normales del zombie

---

### Comandos

<strong>impulso-necesita redstone</strong>

<pre>/summon minecraft:zombie ~ ~1 ~ {Tags:["boss_void_general"],PersistenceRequired:true,CanBreakDoors:true,CustomName:{text:"El General del Vacío",color:"dark_red",bold:true},CustomNameVisible:true}</pre>

<strong>impulso-necesita redstone (Validado con comparador previamente)</strong>
<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:scale base set 2.4</pre>

<strong>cadena-siempre activo</strong>

<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:max_health base set 450</pre>

<pre>/data merge entity @e[tag=boss_void_general,limit=1,sort=nearest] {Health:450f}</pre>

<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:attack_damage base set 18</pre>

<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:movement_speed base set 0.34</pre>

<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:armor base set 18</pre>

<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:armor_toughness base set 12</pre>

<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:knockback_resistance base set 0.9</pre>

<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:attack_knockback base set 4</pre>

<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:follow_range base set 70</pre>

<pre>/attribute @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:step_height base set 5</pre>

<pre>/effect give @e[tag=boss_void_general,limit=1,sort=nearest] minecraft:fire_resistance infinite 0 true</pre>

Aplicacion de armadura al boss:

<pre>/item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] weapon.mainhand with minecraft:netherite_sword[minecraft:enchantments={sharpness:7,sweeping_edge:5,fire_aspect:2,unbreaking:5}]</pre>

<pre>/item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] armor.head with minecraft:netherite_helmet[minecraft:enchantments={protection:5,unbreaking:5}]</pre>

<pre>/item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] armor.chest with minecraft:netherite_chestplate[minecraft:enchantments={protection:5,unbreaking:5}]</pre>

<pre>/item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] armor.legs with minecraft:netherite_leggings[minecraft:enchantments={protection:5,unbreaking:5}]</pre>

<pre>/item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] armor.feet with minecraft:netherite_boots[minecraft:enchantments={protection:5,feather_falling:20,unbreaking:5}]</pre>


---

### Notas

Si deseas evitar que se golpeen entre multiples bosses coloca comandos de team, por ejemplo:

<strong>impulso-necesita redstone</strong>
<pre>/team add bosses</pre>


Y si deseas agregar un boss al equipo le colocas al final de la secuencia un bloque de:

<strong>cadena-siempre activo</strong>
<pre>/team join bosses @e[tag=boss_void_general]</pre>
<pre>/team join bosses @e[tag=boss_colossus]</pre>
<pre>/team join bosses @e[tag=boss_hunter]</pre>
<pre>/team join bosses @e[tag=boss_necromancer]</pre>




