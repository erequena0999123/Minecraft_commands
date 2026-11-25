# Marcadores y temporizadores

Un objetivo del scoreboard guarda una puntuación por jugador o entidad. El criterio determina qué la cambia. Con `dummy`, los comandos escriben el valor; en [Teletransportación](../examples/superpowers/teletransportacion.md), un criterio de uso de perlas registra el lanzamiento. En [Doctor Strange](../examples/superpowers/doctor-strange.md), cada portador tiene su propia cuenta atrás.

## Por qué una telaraña sigue contando al retirar el poder

En [Spider-Man](../examples/superpowers/spider-man.md), `tiempo_telarana` se crea una vez como objetivo `dummy`. Cada marcador con la etiqueta `reloj_telarana` representa una posición de la red. El circuito suma uno a la puntuación de cada marcador en cada ejecución.

<pre>execute as @e[tag=reloj_telarana] at @s run scoreboard players add @s tiempo_telarana 1</pre>

Al llegar a `100..` (100 o más), la secuencia reemplaza por aire la telaraña de esa posición y después retira el marcador. A 20 ejecuciones por segundo son unos cinco segundos. Quitarle al jugador la etiqueta del poder impide generar nuevas redes; los marcadores existentes siguen contando mientras el circuito esté cargado y activo. Si se elimina el objetivo compartido, se pierde la cuenta que permite limpiar esas redes.

[Volver al índice](../README.md)
