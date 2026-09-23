# BOSS-002

### Nombre

EL Coloso

### Entidad

Zombie husk

### Estado

Terminado

---

### Vida

800

---

### Escala

3

---

### Daño

5

---

### Velocidad

0.43

---

### Armadura

Full netherite

30

### Resistencia

12

---

### Arma

No tiene

---

### IA

Persigue jugadores rango de 100

---

### Partículas

No tiene

---

### Sonidos

Normales del zombie

---

### Comandos

<strong>impulso-necesita redstone</strong>

<pre>execute positioned 15 60 -15 run summon minecraft:husk ~ ~1 ~ {Tags:["boss_colossus"],PersistenceRequired:true,CustomName:{text:"El Coloso",color:"dark_gray",bold:true},CustomNameVisible:true}</pre>

<strong>impulso-necesita redstone (Validado con comparador previamente)</strong>
<pre>/attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:scale base set 3</pre>

<strong>cadena-siempre activo</strong>

<pre>/attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:max_health base set 800</pre>

<pre>/data merge entity @e[tag=boss_colossus,limit=1,sort=nearest] {Health:800f}</pre>

<pre>/attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:attack_damage base set 5</pre>

<pre>/attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:armor base set 30</pre>

<pre>/attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:armor_toughness base set 20</pre>

<pre>/attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:knockback_resistance base set 1</pre>

<pre>/attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:movement_speed base set 0.43</pre>

<pre>/attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:follow_range base set 100</pre>

<pre>/attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:step_height base set 5</pre>

<pre>/effect give @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:fire_resistance infinite 0 true</pre>

<strong> Equipo </strong>

<pre>/item replace entity @e[tag=boss_colossus,limit=1,sort=nearest] armor.head with minecraft:netherite_helmet[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

<pre>/item replace entity @e[tag=boss_colossus,limit=1,sort=nearest] armor.chest with minecraft:netherite_chestplate[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

<pre>/item replace entity @e[tag=boss_colossus,limit=1,sort=nearest] armor.legs with minecraft:netherite_leggings[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

<pre>/item replace entity @e[tag=boss_colossus,limit=1,sort=nearest] armor.feet with minecraft:netherite_boots[minecraft:enchantments={protection:10,feather_falling:20,unbreaking:5}]</pre>

<pre>team join bosses @e[tag=boss_colossus]</pre>
