# Catálogo de partículas

Usa estas fichas para añadir una señal visible a una entidad, un lugar o una habilidad. El comando `particle` dibuja el efecto. Los cambios de daño, movimiento o estado se programan por separado.

## Cómo leer una emisión

En el siguiente ejemplo, configura un bloque de **impulso · incondicional · necesita redstone** y pulsa un botón para ver una emisión sobre el bloque.

<pre>particle minecraft:soul_fire_flame ~ ~1 ~ 0.25 0.35 0.25 0.01 3 normal @a[distance=..24]</pre>

| Parte del ejemplo | Qué puedes ajustar |
|---|---|
| `minecraft:soul_fire_flame` | Elige el aspecto. Algunas partículas admiten datos propios. La llama de almas ya tiene su color. |
| `~ ~1 ~` | Origen, un bloque por encima de la posición de ejecución. Con `at @s` puedes llevar ese origen a una entidad. |
| `0.25 0.35 0.25` | Dispersión aleatoria en X, Y y Z. Aumenta el segundo número para alargar la figura verticalmente. |
| `0.01` | Parámetro de velocidad. Su efecto visible depende de la partícula. |
| `3` | Cantidad solicitada por emisión. En repetición se vuelve a emitir cada vez que se ejecuta el bloque. |
| `normal @a[distance=..24]` | Selecciona espectadores a 24 bloques o menos del origen de ejecución. El modo `normal` aplica el alcance habitual de visualización. `force` permite enviar el efecto a más distancia. |

## Diseños

- [Soul Fire · aura de llama de almas](soul_fire.md). Emisión móvil alrededor de una criatura marcada.

Ideas para futuras fichas: chispas eléctricas (`electric_spark`), partículas de portal (`portal`) y polvo de color (`dust`).

[Volver a Extras](../../extras/README.md) · [Volver al índice principal](../../README.md)
