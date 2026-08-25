# POWER-002

### Nombre
Poderes de Doctor Strange
---
### Habilidades:
<ul>
  <li>Poder detener a las entidades dentro de su rango</li>
 
</ul>

---
### Items
Reloj

---
### Equipo
no tiene

---
### Cooldown
<ul>
  <li>2 minutos y 20 segundos de paralizacion del tiempo</li>
  <li>2 minutos de cooldown para volver a usar la habilidad</li>
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

<strong>impulso-necesita redstone</strong>

<pre>tag ManuneitorMC add doctor_strange</pre>


<strong>cadena-siempre activo</strong>

<pre>/scoreboard objectives add tiempo_parado dummy</pre>
<pre>scoreboard players set @a[tag=doctor_strange] tiempo_parado 0</pre>

</br>

#### Quitar tags y scoreboards:

<strong>impulso-necesita redstone</strong>
<pre>tag @a[tag=doctor_strange] remove doctor_strange</pre>


<strong>cadena-siempre activo</strong>
<pre>/scoreboard objectives remove tiempo_parado</pre>



#### Timer de uso de la habilidad:

<strong>repetir-necesita redstone</strong>
<pre>execute as @a[tag=doctor_strange, scores={tiempo_parado=0}] if items entity @s weapon.mainhand minecraft:clock run scoreboard players set @s tiempo_parado 5200</pre>


<strong>cadena-siempre activo</strong>
<pre>execute as @a[scores={tiempo_parado=1..}] run scoreboard players remove @s tiempo_parado 1</pre>



#### Dar Reloj:

<strong>repetir-necesita redstone</strong>
<pre>execute as @a[tag=doctor_strange] unless items entity @s hotbar.* minecraft:clock run give @s minecraft:clock[minecraft:custom_name=[{text:'Reloj del Tiempo', color:'blue', lore:[[{"text":"El Reloj que controla el tiempo","italic":true}]], obfuscated:true}]]</pre>



#### Paralizar y desparalizar entidades dentro del rango:


<strong>repetir-necesita redstone (Bloques de repeticion separados)</strong>
<pre>/execute as @a[tag=doctor_strange, scores={tiempo_parado=2400..}] at @s as @e[type=!minecraft:player,distance=..50] run data merge entity @s {NoAI:true}</pre>

<pre>/execute as @a[tag=doctor_strange, scores={tiempo_parado=..2400}] at @s as @e[type=!minecraft:player,distance=..50] run data merge entity @s {NoAI:false}</pre>


