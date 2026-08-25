# POWER-001

### Nombre
Poderes de Spider man
---
### Habilidades:
<ul>
  <li>Poder escalar paredes</li>
  <li>Lanzar telas de arañas</li>
</ul>

---
### Items
Bolas de nieve

---
### Equipo
no tiene

---
### Cooldown
<ul>
  <li>1-2 segundos levitacion</li>
  <li>5 segundos de telarañas</li>
</ul>

---

### Partículas
no tiene

---
### Cloud
no tiene

---
### Sonido
no tiene

---

### Comandos

#### Colocar tags y scoreboards:
<p>
<strong>impulso-necesita redstone</strong>

<pre>tag ManuneitorMC add spider_man</pre>

<strong>cadena-siempre activo</strong>

<pre>scoreboard objectives add tiempo_telarana dummy</pre> 

</br>

#### Quitar tags y scoreboards:

<strong>impulso-necesita redstone</strong>

<pre>tag @a[tag=spider_man] remove spider_man</pre>  

<strong>cadena-siempre activo</strong>

<pre>scoreboard objectives remove tiempo_telarana</pre>

</br>

#### Caminar por paredes:

<strong>repeticion-necesita redstone</strong>

<pre>execute as @a[tag=spider_man] at @s unless block ^ ^1 ^1 minecraft:air run effect give @s minecraft:levitation 1 1 true</pre>

<strong>cadena-siempre activo</strong>

<pre>execute as @a[tag=spider_man] at @s unless block ~ ~2 ~ air run effect give @s minecraft:levitation 2 1 true</pre>
<pre>execute as @a[tag=spider_man] at @s unless block ~ ~-1 ~ minecraft:air run effect clear @a minecraft:levitation</pre>

</br>

#### Dar bolas de nieve:

<strong>repeticion-necesita redstone</strong>

<pre>execute as @a[tag=spider_man] unless items entity @s hotbar.* minecraft:snowball run give @s minecraft:snowball 2</pre>

</br>

#### Efecto de telarañas con bolas de nieve:

<strong>repeticion-necesita redstone</strong>

<pre>execute if entity @a[tag=spider_man]</pre>

<strong>cadena-siempre activo-condicional</strong>
<pre>execute as @e[type=minecraft:snowball] at @s positioned ^ ^1 ^ if block ~ ~ ~ minecraft:air run summon minecraft:interaction ~ ~ ~ {Tags:["reloj_telarana"],Passengers:[{text:''}]} </pre>

<strong>cadena-siempre activo-incondicional</strong>

<pre>execute at @e[tag=reloj_telarana] run setblock ~ ~ ~ minecraft:cobweb replace </pre>
<pre>execute as @e[tag=reloj_telarana] at @s run scoreboard players add @s tiempo_telarana 1 </pre>
<pre>execute as @e[tag=reloj_telarana, scores={tiempo_telarana=100..}] at @s run fill ~ ~ ~ ~ ~ ~ minecraft:air replace minecraft:cobweb </pre>
<pre>execute as @e[tag=reloj_telarana, scores={tiempo_telarana=100..}] run kill @s </pre>

</p>
