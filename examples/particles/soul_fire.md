# Soul Fire · aura de llama de almas

Una pequeña nube de llamas azules sigue al Nigromante. La ficha usa la etiqueta que ya recibe el [boss al invocarlo](../bosses/nigromante.md). Puedes adaptar el selector a otra criatura marcada. El efecto visual es independiente de su aura de daño.

**Montaje.** Con el Nigromante presente, coloca un bloque de **repetición · incondicional · necesita redstone** y añade una palanca.

<pre>execute as @e[type=minecraft:evoker,tag=boss_necromancer] at @s run particle minecraft:soul_fire_flame ~ ~1 ~ 0.25 0.35 0.25 0.01 3 normal @a[distance=..24]</pre>

**Qué observar.** Cerca de la criatura deberían aparecer llamas a la altura del torso y acompañarla al desplazarse. Al apagar la palanca cesan las emisiones y las llamas ya visibles se disipan. Si se ve demasiado denso, baja la cantidad de `3` a `1`. Cada criatura seleccionada genera su propia emisión.

**Probado en Minecraft.** El autor confirmó que la emisión de llamas azules sigue al Nigromante cuando se desplaza y se detiene al apagar la palanca.

[Catálogo de partículas](README.md) · [Volver a Extras](../../extras/README.md) · [Volver al índice principal](../../README.md)
