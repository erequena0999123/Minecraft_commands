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
02. [Componentes de Ítems](#minecraftenchantments)
03. [Atributos de Entidades](#minecraftmax_health)
04. [Equipamiento](#mainhand)
05. [IA y Comportamientos](#follow-range)
06. [Sistema de Bosses](#boss-001)
07. Sistema de Superpoderes
08. Sistema de Objetos Especiales
09. Sistema de Partículas
10. Sistema de Sonidos
11. JSON Text
12. Execute
13. Scoreboards
14. Funciones Útiles
15. Laboratorio
16. Recursos Externos
99. Changelog



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


# minecraft:enchantments

Estado

✔ Verificado

Comando

/give @p minecraft:netherite_sword[
minecraft:enchantments={
sharpness:10,
sweeping_edge:10
}
]

Resultado

Funciona correctamente.

Notas

No utiliza "levels".
No requiere namespace minecraft:
para cada encantamiento.

Compatible con:

✔ give

✔ item replace

# minecraft:custom_name
# minecraft:lore
# minecraft:unbreakable


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


# BOSS-001

Nombre

Caballero Oscuro

Entidad

Zombie

Estado

En desarrollo

---

Vida

150

---

Escala

2

---

Daño

18

---

Velocidad

0.45

---

Armadura

20

---

Arma

Netherite Sword

---

IA

Persigue jugadores.

Rompe puertas.

---

Partículas

Soul Fire

---

Sonidos

...

---

Comandos

...

---

Notas

...
