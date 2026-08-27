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

Persigue jugadores.

---

### Partículas

Soul Fire

---

### Sonidos

Noormales del zombie

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

---

### Notas

...
