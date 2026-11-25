# Textos, nombres y lore

Un componente de texto combina contenido y estilo. Dentro de un comando Java se puede escribir una cadena simple, un objeto como `{text:"Eco",color:"aqua"}` o una lista de componentes. En una lista, los siguientes heredan el estilo del primero salvo que lo sobrescriban. Para combinar tramos con una base neutra, usa una raíz `{text:"",extra:[...]}`. [Formato de Mojang](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-5)

## Nombres de entidades y objetos

**Entidad.** Este ejemplo crea un soporte con un nombre visible en dorado y negrita. `CustomNameVisible` controla la visibilidad del rótulo.

<pre>summon minecraft:armor_stand ~ ~ ~ {CustomName:{text:"Guardián",color:"gold",bold:true},CustomNameVisible:true}</pre>

**Objeto y relato.** En las piezas de armadura, armas y otros ítems, `minecraft:custom_name` da nombre al objeto. `minecraft:lore` es otro componente, al mismo nivel dentro de los corchetes. Cada entrada de su lista es una línea del tooltip. Este ejemplo da un casco con un nombre de dos colores y dos líneas de historia al jugador más cercano al bloque.

<pre>give @p minecraft:iron_helmet[minecraft:custom_name={text:"",italic:false,extra:[{text:"Yelmo ",color:"gold"},{text:"del Alba",color:"#FF8060",bold:true}]},minecraft:lore=[{text:"Forjado al amanecer.",color:"gray",italic:false},{text:"Aún conserva el calor de la primera fragua.",color:"yellow",italic:true}]] 1</pre>

El nombre y el relato identifican visualmente la pieza. Para detectar el objeto de un poder, las fichas usan una marca independiente en `minecraft:custom_data`. También existe `minecraft:item_name` para sustituir el nombre base del tipo de objeto; usa `custom_name` para un nombre personalizado como los del manual.

## Estilo de cada tramo

| Campo | Qué cambia |
|---|---|
| `color` | Color por nombre (`"dark_red"`, `"aqua"`, `"gold"`…) o hexadecimal `"#RRGGBB"`. |
| `bold`, `italic` | Negrita y cursiva. En nombres y lore puedes usar `italic:false` para pedir letra recta. |
| `underlined`, `strikethrough` | Subrayado y tachado. |
| `obfuscated` | Con `true`, los caracteres cambian de apariencia. El color sigue siendo el elegido para ese tramo. |
| `font`, `shadow_color` | Fuente disponible en el cliente (por ejemplo `"minecraft:default"`) y color de sombra. Un valor de sombra de 0 la hace transparente. |

**Arcoíris estático.** Asigna varios colores a tramos o letras. Este ejemplo muestra cuatro colores en la barra de acción; el mismo componente puede usarse como nombre. Para desplazar los colores con el tiempo haría falta actualizar el texto.

<pre>title @p actionbar {text:"",extra:[{text:"A",color:"red"},{text:"u",color:"gold"},{text:"r",color:"green"},{text:"a",color:"aqua"}]}</pre>

## Otras formas de contenido y dónde funcionan

| Forma | Uso |
|---|---|
| `text` | Texto literal elegido por el autor. |
| `translate`, con `with` y `fallback` opcionales | Clave traducible en el idioma del cliente, argumentos y texto alternativo. |
| `keybind` | Nombre de una tecla según la configuración del jugador, por ejemplo `{keybind:"key.jump"}`. |
| `score`, `selector` | Puntuación o nombres seleccionados. Requieren una superficie que resuelva el contexto, como un mensaje de comando. Un nombre de objeto almacenado no es un contador vivo. |
| `nbt` | Lee una ruta desde `entity`, `block` o `storage`. Admite `interpret` para interpretar el dato como texto y `separator` para separar resultados; también se puede indicar separador con `selector`. |
| `object` | Inserta un gráfico dentro del texto, por ejemplo un sprite de atlas o la cabeza de un jugador. [Formato de objetos de Mojang](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-9) |

Para interacción en superficies como el chat existen `click_event`, `hover_event` e `insertion`. Por ejemplo, en un mensaje, `hover_event:{action:"show_text",value:{text:"Ayuda"}}` muestra ayuda al pasar el cursor. El contexto de visualización decide qué eventos admite: un rótulo sobre una entidad o un aviso de la barra de acción no se convierte en un botón por incluir estos campos.

**Probado en Minecraft.** El autor confirmó que el nombre aparece sobre el soporte, el casco muestra el nombre en dos colores y el lore personalizado, y la barra de acción muestra el texto arcoíris con colores fijos.

[Componentes de ítems](sintaxis.md#componentes-de-ítems) · [Volver al índice](../README.md)
