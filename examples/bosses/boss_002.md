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

0.34

---

### Armadura

Full netherite

18

### Resistencia

12

---

### Arma

No tiene

---

### IA

Persigue jugadores rango de 70

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
