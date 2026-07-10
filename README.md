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
06. [Sistema de Bosses](examples/bosses)
07. [Sistema de Superpoderes](#power-001)
08. [Sistema de Objetos Especiales](#legendarios)
09. [Sistema de Partículas](#soul-fire)
10. [Sistema de Sonidos](#enderman)
11. [JSON Text](#color)
12. [Execute](#execute-as)
13. [Scoreboards](#crear-objetivos)
14. [Funciones Útiles](#eliminar-entidades)
15. [Laboratorio](#lab-001)
16. [Recursos Externos](#documentación)
99. [Changelog](#v001)



# Introducción

Esta biblioteca recopila todos los comandos, pruebas y descubrimientos
realizados durante el desarrollo del mapa.

Toda la información incluida aquí ha sido verificada
directamente dentro de Minecraft Java 1.21.6.

Objetivos

- Documentar todos los sistemas.
- Evitar repetir pruebas.
- Mantener compatibilidad.
- Facilitar mantenimiento.
- Crear una base reutilizable.


# Componentes

Desde 1.20.5 los Items utilizan Data Components.

Ejemplo

minecraft:diamond_sword[
minecraft:enchantments={sharpness:5}
]




# minecraft:max_health

Estado

✔ Verificado

Comando

/attribute ...

Resultado

Aumenta la vida máxima.

Notas

Debe ejecutarse después

/data merge entity ... {Health:100f}

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

/item replace entity ...

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







Legendarios

Artefactos

Reliquias

Llaves

Objetos de misión

Objetos permanentes


# Soul Fire

Comando

...

Uso

Boss Infernal

---

Electric Spark

...

---

Portal

...

---

Dust

...


# Enderman

...

---

Wither

...

---

Lightning

...

---

Custom Ambient

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


execute as

execute at

execute if

execute unless

execute store

execute positioned

execute facing

execute rotated

execute anchored


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


LAB-001

Atributos

Resultado

✔

Conclusiones

...

---

LAB-002

Componentes

Resultado

✔

...

---

LAB-003

Bosses

...

---

LAB-004

Execute

...

---

LAB-005

IA

...


## Documentación

Minecraft Wiki

https://minecraft.wiki

---

## Generador

https://www.gamergeeks.net/apps/minecraft/give-command-generator

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
