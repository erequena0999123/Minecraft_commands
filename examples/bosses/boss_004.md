# BOSS-004

### Nombre

EL Nigromante

### Entidad

Evoker

### Estado

Terminado

---

### Vida

300

---

### Escala

1.8

---

### Daño

20

---

### Velocidad

0.26

---

### Armadura

No tiene

8

### Resistencia

12

---

### Arma

No tiene

---

### IA

Persigue jugadores rango de 150

---

### Partículas

No tiene

---

### Sonidos

Normales de Evoker

---

### Comandos

<strong>impulso-necesita redstone</strong>

<pre>execute positioned -15 61 19 run summon minecraft:evoker ~ ~1 ~ {Tags:["boss_necromancer", "aura_dmg_boss"],PersistenceRequired:true,CustomName:{text:"El Nigromante",color:"dark_purple",bold:true},CustomNameVisible:true}</pre>

<strong>impulso-necesita redstone (Validado con comparador previamente)</strong>
<pre>/attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:scale base set 1.8</pre>

<strong>cadena-siempre activo</strong>

<pre>/attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:max_health base set 300</pre>

<pre>/data merge entity @e[tag=boss_necromancer,limit=1,sort=nearest] {Health:300f}</pre>

<pre>/attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:attack_damage base set 20</pre>

<pre>/attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:armor base set 8</pre>

<pre>/attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:movement_speed base set 0.26</pre>

<pre>/attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:follow_range base set 150</pre>

<pre>/effect give @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:fire_resistance infinite 0 true</pre>


<strong>repetir-necesita redstone</strong>

<pre>execute at @e[tag=aura_dmg_boss] run damage @n[type=minecraft:player, distance=..5] 2 minecraft:indirect_magic</pre>


<strong> Equipo </strong>

<pre>/team join bosses @e[tag=boss_necromancer]</pre>
