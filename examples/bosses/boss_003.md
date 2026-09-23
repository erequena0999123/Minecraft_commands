# BOSS-002

### Nombre

EL Cazador

### Entidad

Stray

### Estado

Terminado

---

### Vida

200

---

### Escala

1.6

---

### Daño

20

---

### Velocidad

0.32

---

### Armadura

Peto de Diamante

10

### Resistencia

12

---

### Arma

Arco

---

### IA

Persigue jugadores rango de 70

---

### Partículas

No tiene

---

### Sonidos

Normales de Stray

---

### Comandos

<strong>impulso-necesita redstone</strong>

<pre>execute positioned 18 59 14 run summon minecraft:stray ~ ~1 ~ {Tags:["boss_hunter"],PersistenceRequired:true,CustomName:{text:"El Cazador",color:"dark_aqua",bold:true},CustomNameVisible:true}</pre>

<strong>impulso-necesita redstone (Validado con comparador previamente)</strong>
<pre>/attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:scale base set 1.6</pre>

<strong>cadena-siempre activo</strong>

<pre>/attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:max_health base set 200</pre>

<pre>/data merge entity @e[tag=boss_hunter,limit=1,sort=nearest] {Health:200f}</pre>

<pre>/attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:attack_damage base set 20</pre>

<pre>/attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:armor base set 10</pre>

<pre>/attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:movement_speed base set 0.32</pre>

<pre>/attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:follow_range base set 70</pre>

<pre>/attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:knockback_resistance base set 0.4</pre>

<pre>/effect give @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:fire_resistance infinite 0 true</pre>

<strong> Equipo </strong>

<pre>/item replace entity @e[tag=boss_hunter,limit=1,sort=nearest] weapon.mainhand with minecraft:bow[minecraft:enchantments={power:100,punch:2,flame:1,unbreaking:5}]</pre>

<pre>/item replace entity @e[tag=boss_hunter,limit=1,sort=nearest] armor.chest with minecraft:diamond_chestplate[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

<pre>/team join bosses @e[tag=boss_hunter]</pre>
