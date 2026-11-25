# Cómo leer los comandos del manual

**Referencia al 22 de noviembre de 2026: Java Edition 26.3**, versión estable publicada por [Mojang](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-3). Las pruebas históricas conservan la versión y el alcance que indique cada ficha. Al salir una estable, contrasta sus notas con las construcciones usadas antes de actualizar ejemplos afectados.

**Consulta por tema:** [Componentes de ítems](#componentes-de-ítems) · [Atributos](#atributos-de-entidades) · [Equipamiento](#equipamiento) · [IA y comportamiento](#ia-y-comportamiento) · [Execute](#execute)

## Del texto al bloque

Cada recuadro de una ficha contiene un comando para un bloque, sin barra inicial. En el chat del juego añade `/`. Sigue el orden, la orientación de las flechas y los ajustes de impulso, repetición o cadena, condición y redstone de esa ficha. Sustituye `NOMBRE_JUGADOR` por el nombre exacto cuando aparezca.

En el montaje del [Cazador](../examples/bosses/cazador.md), los bloques de cadena con «Siempre activo» ejecutan sus comandos cuando les llega la secuencia del bloque anterior. Este ajuste quedó verificado en las pruebas del montaje.

| Al leer… | Interprétalo así |
|---|---|
| `NoAI:true`, `italic:false` | Para campos booleanos usamos palabras. Las cantidades conservan su tipo: `Health:800f` es vida y `HurtTime:8s` es un valor corto. |
| `minecraft:unbreakable={}` | La presencia del componente vacío activa esta propiedad. |
| `Tags:["boss_colossus"]` | Etiqueta propia del sistema. Respeta mayúsculas de los campos NBT. Usa identificadores vanilla con `minecraft:` para entidades, ítems, efectos y atributos. |
| `@s`, `@p` | El primero es el ejecutor actual; el segundo, el jugador más cercano a la posición de ejecución. Cada bloque establece su propio contexto. |
| `summon` → `attribute` → `item replace` | En los bosses, invoca con los datos iniciales, ajusta atributos y equipa en bloques separados. Tras aumentar la vida máxima, algunas fichas asignan la vida actual con `data merge`. Los modificadores de una pieza equipada permanecen en el objeto. |

En los comandos escribimos datos en SNBT: conservamos las comillas necesarias en cadenas y claves y preferimos comillas dobles en texto simple. Los componentes de texto se escriben directamente como estructuras. Para un nombre con color o una historia de objeto consulta [Textos, nombres y lore](textos.md).

### Nombre y datos de una entidad

Este dato corresponde a la entidad; no es un componente de ítem:

<pre>CustomName:{text:"Guardián",color:"gold",bold:true,obfuscated:false}</pre>

Este filtro detecta el instante en que el contador de daño vale 8 ticks:

<pre>{HurtTime:8s}</pre>

## Componentes de ítems

En `give` e `item replace`, los componentes van entre corchetes después del identificador del objeto.

| Componente | Qué hace |
|---|---|
| `minecraft:enchantments` | Asigna un nivel a cada encantamiento con un mapa directo, por ejemplo `{sharpness:10,sweeping_edge:10}`. |
| `minecraft:custom_name` y `minecraft:lore` | El primero cambia el nombre visible. El segundo añade una línea por entrada en la descripción. El [Yelmo del Alba](textos.md#nombres-de-entidades-y-objetos) combina ambos. |
| `minecraft:custom_data` | Marca una copia para reconocerla aunque otra tenga el mismo nombre. [Doctor Strange](../examples/superpowers/doctor-strange.md) comprueba la marca del reloj en la mano principal. |
| `minecraft:unbreakable={}` | Evita que el objeto pierda durabilidad. [Volar](../examples/superpowers/volar.md) lo usa en las élitras. |
| `minecraft:death_protection={}` | Concede al objeto la propiedad de proteger frente a la muerte. El prefijo `!` quita el componente del objeto entregado. |

**Entregar una espada encantada.** El ejemplo registrado como verificado entrega la espada al jugador más cercano al bloque.

<pre>give @p minecraft:netherite_sword[minecraft:enchantments={sharpness:10,sweeping_edge:10}]</pre>

**Combinar nombre y encantamientos.** La Espada del Vacío lleva nombre rojo oscuro, negrita y texto ofuscado.

<pre>give @p minecraft:netherite_sword[minecraft:custom_name=[{"text":"Espada del Vacío",color:"dark_red","bold":true,obfuscated:true}],minecraft:enchantments={sharpness:10,sweeping_edge:10,unbreaking:10}]</pre>

**Quitar una propiedad.** Este ejemplo entrega un tótem sin su protección frente a la muerte.

<pre>give @p minecraft:totem_of_undying[!minecraft:death_protection]</pre>

## Atributos de entidades

**Tamaño.** La ficha del [Cazador](../examples/bosses/cazador.md) aplica una escala de 1.6 para darle un tamaño mayor. El registro original marcó el uso de este atributo como verificado.

<pre>attribute @e[tag=boss_hunter,limit=1,sort=nearest] minecraft:scale base set 1.6</pre>

**Vida máxima y vida actual.** Con el [Coloso](../examples/bosses/coloso.md) ya invocado, el primer bloque fija su capacidad en 800 puntos de vida. El siguiente le asigna esos 800 puntos de salud actual. Ambos seleccionan al Coloso más cercano.

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:max_health base set 800</pre>

<pre>data merge entity @e[tag=boss_colossus,limit=1,sort=nearest] {Health:800f}</pre>

**Altura de paso.** `step_height` determina el desnivel que puede subir al caminar. El ensayo original registró dos bloques con un zombi. La ficha del Coloso configura cinco.

<pre>attribute @e[tag=boss_colossus,limit=1,sort=nearest] minecraft:step_height base set 5</pre>

**Salto.** `jump_strength` se estudió por separado. En la prueba histórica con el zombi, el autor no observó un cambio de salto. El resultado sigue siendo parcial.

## Equipamiento

`item replace entity` equipa el objeto directamente en la ranura indicada. Estos son los nombres de las ranuras que corresponden a cada parte del equipo.

| Ranura | Uso en el manual |
|---|---|
| `weapon.mainhand` | Mano principal. El [General del Vacío](../examples/bosses/general-del-vacio.md) lleva espada y el [Cazador](../examples/bosses/cazador.md) lleva arco. |
| `weapon.offhand` | Mano secundaria. Se conserva como referencia de ranura. |
| `armor.head` y `armor.chest` | Casco y peto. |
| `armor.legs` y `armor.feet` | Grebas y botas. El [Coloso](../examples/bosses/coloso.md) utiliza las cuatro ranuras de armadura. |

**Equipar la espada del General** una vez invocado:

<pre>item replace entity @e[tag=boss_void_general,limit=1,sort=nearest] weapon.mainhand with minecraft:netherite_sword[minecraft:enchantments={sharpness:7,sweeping_edge:5,fire_aspect:2,unbreaking:5}]</pre>

**Equipar el casco del Coloso** con protección e irrompibilidad por encantamiento:

<pre>item replace entity @e[tag=boss_colossus,limit=1,sort=nearest] armor.head with minecraft:netherite_helmet[minecraft:enchantments={protection:10,unbreaking:5}]</pre>

## IA y comportamiento

- **Alcance de seguimiento.** El Coloso tiene `minecraft:follow_range` en 100 bloques. El atributo ajusta el alcance de su IA para seguir objetivos. La elección del objetivo depende del comportamiento de la criatura.
- **Puertas.** El General del Vacío se invoca con `CanBreakDoors:true` para habilitar el comportamiento de romper puertas del zombi cuando las condiciones del juego lo permiten.
- **Pausa de la IA.** [Doctor Strange](../examples/superpowers/doctor-strange.md) registra las criaturas afectadas antes de aplicar `NoAI:true`. Así puede devolverles la movilidad cuando salen del área o termina la habilidad.

## Execute

Lee la instrucción de izquierda a derecha. Cada parte ajusta quién ejecuta, desde dónde o bajo qué condición. `run` introduce la acción final.

| Parte | Qué hace |
|---|---|
| `as` / `at` | `as` cambia el ejecutor al que se refiere `@s`. `at` toma la posición, orientación y dimensión de la entidad indicada. |
| `if` / `unless` | Continúa si se cumple la condición o, con `unless`, si falla. |
| `positioned` | Sitúa la ejecución en las coordenadas indicadas. Desde allí se mide, por ejemplo, el radio de un lobby. |
| `rotated` / `facing` | El primero establece la orientación de ejecución. El segundo la dirige hacia una posición o entidad. |
| `anchored` | Elige los pies o los ojos como origen para coordenadas locales como `^ ^ ^1`. |
| `store` | Guarda el resultado numérico o el éxito de una instrucción, por ejemplo en un marcador. |

**Aplicar una regla de zona.** Este bloque del [lobby](../extras/utilidades-para-mundos/zonas-y-lobbies/README.md) cambia a aventura a quienes estén en supervivencia dentro de siete bloques del centro de ejemplo.

<pre>execute positioned -5 -24 12 run gamemode adventure @a[gamemode=survival, distance=..7]</pre>

**Detectar la pared frente al portador.** [Spider-Man](../examples/superpowers/spider-man.md) ejecuta la comprobación desde cada portador. `rotated ~ 0` conserva su dirección horizontal y nivela la mirada antes de comprobar el bloque. Así, mirar al suelo no activa por sí solo la levitación frontal.

<pre>execute as @a[tag=spider_man] at @s rotated ~ 0 unless block ^ ^1 ^1 minecraft:air run effect give @s minecraft:levitation 1 1 true</pre>

[Volver al índice principal](../README.md)
