# BOSS-004

### Nombre

EL NIgromante

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

<pre>execute positioned -15 61 19 run summon minecraft:evoker ~ ~1 ~ {Tags:["boss_necromancer", "aura_dmg_boss"],PersistenceRequired:true,CustomName:{text:"El Nigromante",color:"dark_purple",bold:true},CustomNameVisible:true}</pre>

<strong>impulso-necesita redstone (Validado con comparador previamente)</strong>
<pre>/attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:scale base set 1.8</pre>

<strong>cadena-siempre activo</strong>

<pre>/attribute @e[tag=boss_necromancer,limit=1,sort=nearest] minecraft:max_health base set 300</pre>

<pre>/data merge entity @e[tag=boss_necromancer,limit=1,sort=nearest] {Health:300f}</pre>


<strong> Equipo </strong>

<pre>/item replace entity @e[tag=boss_hunter,limit=1,sort=nearest] weapon.mainhand with minecraft:bow[minecraft:enchantments={power:100,punch:2,flame:1,unbreaking:5}]</pre>

<pre>/item replace entity @e[tag=boss_hunter,limit=1,sort=nearest] armor.chest with minecraft:diamond_chestplate[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

<pre>/team join bosses @e[tag=boss_hunter]</pre>
