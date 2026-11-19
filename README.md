# Minecraft_commands
This repository was made to have a guidance into Json sintaxis from Minecraft 1.21.6+ current versions


# Minecraft Command Library (MCL)
### Biblioteca Técnica del Proyecto

Versión del Proyecto: Alpha
Versión de Minecraft: Java Edition 1.21.6 (26.2)
Estado: En desarrollo

---

# Índice

00. [Introducción](#introducción)
01. [Sintaxis Minecraft 1.21.6](#componentes)
02. [Componentes de Ítems](docs/Componentes_Items.md)
03. [Atributos de Entidades](#minecraftmax_health)
04. [Equipamiento](#mainhand)
05. [IA y Comportamientos](#follow-range)
06. [Sistema de Bosses](examples/bosses/README.md)
07. [Sistema de Superpoderes](examples/superpowers/README.md)
08. [Objetos especiales — extras](extras/objetos-especiales.md)
09. [Sistema de Partículas](examples/particles)
10. [Sonidos — extras](extras/sonidos.md)
11. [JSON Text](#color)
12. [Execute](#execute)
13. [Scoreboards](#crear-objetivos)
14. [Funciones Útiles](#eliminar-entidades)
15. [Laboratorios — extras](extras/laboratorios.md)
16. [Recursos Externos](#documentación)
99. [Changelog](#v001)



# Introducción

Esta biblioteca recopila todos los comandos, pruebas y descubrimientos
realizados durante el desarrollo del mapa.

Toda la información incluida aquí ha sido verificada
directamente dentro de Minecraft Java 1.21.6.

Objetivos

<ul>
<li> Documentar todos los sistemas.</li>
<li> Evitar repetir pruebas.</li>
<li> Mantener compatibilidad.</li>
<li> Facilitar mantenimiento.</li>
<li> Crear una base reutilizable.</li>
</ul>

# Componentes

Desde 1.20.5 los ítems utilizan Data Components. Los siguientes fragmentos muestran estructuras; no son comandos completos.

## Nombre de entidad: NBT de la entidad

Este dato corresponde a la entidad; no es un componente de ítem:

<pre>CustomName:{text:"",color:"",bold:true,obfuscated:true}</pre>

Otro fragmento de dato de entidad:

<pre>{HurtTime:8s}</pre>

## Componentes de ítems

<pre>minecraft:death_protection={}</pre>

<pre>minecraft:enchantments={sharpness:255}</pre>

<pre>minecraft:diamond_sword[minecraft:enchantments={sharpness:5}]</pre>

Comando para bloque. Para ejecutarlo desde el chat del juego, añade `/`:

<pre>give @p minecraft:netherite_sword[minecraft:custom_name=[{"text":"Espada del Vacío",color:"dark_red","bold":true,obfuscated:true}],minecraft:enchantments={sharpness:10,sweeping_edge:10,unbreaking:10}]</pre>

Eliminar un componente del objeto entregado, también desde un bloque:

<pre>give @p minecraft:totem_of_undying[!minecraft:death_protection]</pre>

# Convenciones del Proyecto

<ul>
<li>Usar true/false en lugar de 1b/0b cuando la sintaxis lo permita.</li>
<li>Usar CustomName como objeto NBT ({text:"...",color:"..."}) para entidades.</li>
<li>Usar siempre Tags únicos (boss_guardian, boss_colossus, etc.).</li>
<li>Aplicar atributos con /attribute y equipamiento con /item replace en bloques separados.</li>
<li>Mantener el /summon lo más limpio posible.</li>
<li>Presentar un comando por bloque copiable y en una sola línea. Los fragmentos con puntos suspensivos son esquemas, no comandos ejecutables.</li>
<li>Omitir la barra inicial en ejemplos para bloques; añadirla para el chat del juego.</li>
<li>En SNBT, usar cadenas con comillas dobles cuando no sea necesario escapar su contenido. Mantener las mayúsculas exactas de los campos y los tipos numéricos.</li>
<li>Asignar poderes con NOMBRE_JUGADOR, sustituido por el nombre real antes de ejecutar.</li>
</ul>

# minecraft:max_health

Estado

✔ Verificado

Esquema incompleto, no ejecutable (la barra indica uso desde el chat del juego):

<pre>/attribute ...</pre>

Resultado

Aumenta la vida máxima.

Notas

Debe ejecutarse después

<pre>/data merge entity ... {Health:100f}</pre>

Este es otro esquema: sustituye el selector antes de ejecutarlo.

para rellenar la vida.


# minecraft:step_height

Estado

✔ Verificado

Resultado

El zombie puede subir bloques de hasta
2 bloques sin saltar.

Importancia

Muy alta.

Utilidad

Bosses gigantes.


# minecraft:jump_strength

Estado

⚠ Parcial

Resultado

El atributo existe.

El zombie NO lo utiliza.


# MainHand

Esquema incompleto para el chat del juego; falta el destinatario, la ranura y el objeto:

<pre>/item replace entity ...</pre>

---

# OffHand

...

---

# Helmet

...

---

# Chestplate

...

---

# Leggings

...

---

# Boots

...


# Follow Range

Resultado

✔

---

# Can Break Doors

Resultado

✔

---

# Step Height

Resultado

✔

---

# Aggro

...

---

# Target

...







Color

Bold

Italic

ClickEvent

HoverEvent

Insertion

Obfuscated

Extra

Translate

Keybind

{
"text":"ERROR",
"color":"red",
"obfuscated":true
}


# Execute

execute as


---

execute at

---

execute if

execute unless

execute store

---

execute positioned

ejemplo:

<pre>execute positioned -5 -24 12 run gamemode adventure @a[gamemode=survival, distance=..7]</pre>

---

execute facing

execute rotated

execute anchored

---

Crear objetivos

Detectar jugadores

Cooldowns

Kills

Deaths

Daño

Variables

Temporizadores


Eliminar entidades

Kill

Teleport

Clear

Particle

Title

Tellraw

Clone

Fill

Summon

Item Replace

Attribute

Data Merge

Data Modify


## Documentación

Minecraft Wiki

https://minecraft.wiki

---

## Generador

https://www.gamergeeks.net/apps/minecraft/give-command-generator

https://www.digminecraft.com/generators/

Uso

Generador de Items.

Compatible con versiones modernas.

---

## Videos

https://www.youtube.com/watch?v=P6yX-XKof3g

Descripción

Explicación de los nuevos Data Components.

---

## Mojang

https://www.minecraft.net

---

## Bugs

https://bugs.mojang.com


# v0.0.1

Proyecto iniciado.

---

Se descubre

minecraft:scale

✔

---

Se descubre

step_height

✔

---

jump_strength

No afecta zombies.

---

Nueva sintaxis

minecraft:enchantments={
sharpness:10
}

✔

---

Se verifica

attribute

✔

---

Se verifica

data merge Health

✔

---

Se verifica

Always Active

✔
