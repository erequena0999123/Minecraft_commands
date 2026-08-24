# POWER-001

### Nombre
Poderes de Spider man
---
### Velocidad
No tiene

---
### Objeto
Bolas de nieve

---
### Botas
no tiene

---
### Cooldown

1-2 segundos levitacion

---
### Partículas
no tiene

---
### Cloud
no tiene

---
### Sonido
no tiene
...

### Comandos

#### Colocar tags y scoreboards:

tag ManuneitorMC add spider_man </br>
scoreboard objectives add tiempo_telarana dummy </br>

</br>

#### Quitar tags y scoreboards:

scoreboard objectives add tiempo_telarana dummy </br>
scoreboard objectives remove tiempo_telarana
</br>

#### Caminar por paredes:

execute as @a[tag=spider_man] at @s unless block ^ ^1 ^1 minecraft:air run effect give @s minecraft:levitation 1 1 true </br>
execute as @a[tag=spider_man] at @s unless block ~ ~2 ~ air run effect give @s minecraft:levitation 2 1 true </br>
execute as @a[tag=spider_man] at @s unless block ~ ~-1 ~ minecraft:air run effect clear @a minecraft:levitation

</br>

#### Dar bolas de nieve:

execute as @a[tag=spider_man] unless items entity @s hotbar.* minecraft:snowball run give @s minecraft:snowball 2

</br>

#### Efecto de telarañas con bolas de nieve:

execute if entity @a[tag=spider_man] </br>
execute as @e[type=minecraft:snowball] at @s positioned ^ ^1 ^ if block ~ ~ ~ minecraft:air run summon minecraft:interaction ~ ~ ~ {Tags:["reloj_telarana"],Passengers:[{text:''}]} </br>

execute at @e[tag=reloj_telarana] run setblock ~ ~ ~ minecraft:cobweb replace </br>
execute as @e[tag=reloj_telarana] at @s run scoreboard players add @s tiempo_telarana 1 </br>
execute as @e[tag=reloj_telarana, scores={tiempo_telarana=100..}] at @s run fill ~ ~ ~ ~ ~ ~ minecraft:air replace minecraft:cobweb </br>
execute as @e[tag=reloj_telarana, scores={tiempo_telarana=100..}] run kill @s


...


POWER-002

Teletransporte
