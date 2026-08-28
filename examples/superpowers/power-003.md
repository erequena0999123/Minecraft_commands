# POWER-003

### Nombre
Poderes de Kill aura
---
### Habilidades:
<ul>
  <li>Poder hacer daño a las entidades dentro de su rango (cuentan objetos tirados en el piso)</li>
 
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

<pre>tag ManuneitorMC add aura_dmg</pre>


<strong>cadena-siempre activo</strong>

<pre>/scoreboard objectives add tiempo_aura dummy</pre>
<pre>scoreboard players set @a[tag=aura_dmg] tiempo_aura 0</pre>

</br>

#### Quitar tags y scoreboards:

<strong>impulso-necesita redstone</strong>
<pre>tag @a[tag=aura_dmg] remove aura_dmg</pre>


<strong>cadena-siempre activo</strong>
<pre>scoreboard objectives remove tiempo_aura</pre>



#### Timer de uso de la habilidad:

<strong>repetir-necesita redstone</strong>
<pre>execute as @a[tag=doctor_strange, scores={tiempo_parado=0}] if items entity @s weapon.mainhand minecraft:clock run scoreboard players set @s tiempo_parado 

### Dar Calavera

<strong>repetir-necesita redstone</strong>
<pre>execute as @a[tag=aura_dmg] unless items entity @s hotbar.* minecraft:skeleton_skull run give @s minecraft:wither_skeleton_skull[minecraft:custom_name=[{text:'Kill aura', color:'red', lore:[[{"text":"El Reloj que controla el tiempo","italic":true}]], obfuscated:true}]]</pre>
  
