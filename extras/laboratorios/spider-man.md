# Laboratorio: Spider-Man

[Ficha y comandos](../../examples/superpowers/spider-man.md) · [Volver a laboratorios](../laboratorios.md)

## Resultado vigente: quién puede lanzar telarañas

| Lanzador | Bola lanzada | Resultado observado |
|---|---|---|
| Portador de Spider-Man | Especial, marcada por el poder | Generó telarañas. |
| El mismo portador | Normal | No generó telarañas. |
| Otro jugador sin el poder, con un portador activo | Normal | No generó telarañas. |

El circuito comprueba primero la marca del proyectil y después la etiqueta `spider_man` de quien lo lanzó. Además, la limpieza retira las bolas especiales del inventario de quienes carecen de la etiqueta. Un lanzamiento efectivo de una bola marcada por alguien sin el poder queda descrito por la lógica del comando; la prueba multijugador reportada fue con una bola normal.

La movilidad en las redes y la trayectoria desde el portador ya fueron aprobadas. Los apartados de pruebas que siguen documentan las etapas del desarrollo. La [ficha del poder](../../examples/superpowers/spider-man.md) reúne los comandos vigentes.

## Decisión vigente: escalada sin salto obligatorio, integrada

El usuario cambió la preferencia de inicio: elige conservar la versión anterior a la propuesta OnGround, con escalada al acercarse y salto opcional. Se descarta el control de suelo como requisito. No se registra que haya probado la propuesta OnGround; se conserva como alternativa histórica sin integrar.

Se integra en la ficha la secuencia de dos comandos previamente probada: frontal con rotated ~ 0 y comprobación superior ~ ~2 ~, ambos sin condición OnGround. Primero repetición necesita redstone incondicional; segundo cadena siempre activo incondicional. La retirada global histórica por bloque inferior se elimina del circuito vigente; su código y antecedentes permanecen en las secciones históricas de este laboratorio. La prueba de tres bloques propuesta tampoco debe seguir activa.

El usuario elige acercarse para iniciar escalada y poder saltar de forma opcional. Su apreciación de que saltar facilita o acelera el movimiento se conserva como experiencia del juego, sin cambiar amplificadores ni añadir una bonificación por salto. La pérdida de pared/techo o tag deja agotar el residual original de uno o dos segundos; no se introduce retirada inmediata global.

La ficha queda con 21 comandos copiables y dos bloques de escalada. Movilidad en redes, trayectoria, objeto marcado, filtro y limpieza permanecen idénticos. Se completan las modificaciones funcionales acordadas dentro de los resultados reportados; no se acredita una auditoría universal de versiones, concurrencia, servidor o efectos de otras fuentes. No quedan pruebas OnGround solicitadas por el usuario.

## Frontal horizontal confirmado; recuperar inicio en el aire

El usuario confirmó que rotated ~ 0 elimina activación por mirar a los pies/suelo, mantiene la pared a la altura del cuerpo y no interfiere con el techo. No se declara resuelto todo el problema original del servidor ni probado el control de suelo que se propone a continuación.

### Siguiente prueba: control OnGround y retirada individual

Se conserva exactamente rotated ~ 0, alcance, duraciones y amplificador. Se añade OnGround:false en ambas aplicaciones para que el portador tenga que estar en el aire. Es una aproximación al salto de enganche solicitado: también puede entrar en ella al caer desde un borde; no detecta exclusivamente la tecla de salto. Se añade una retirada con OnGround:true dirigida solo a portadores apoyados en el suelo, para evitar que uno de ellos borre la levitación de otro que trepa. Esto sustituye la retirada global histórica durante esta prueba; no se presenta como probada todavía.

Usar tres bloques en orden: primero repetición, necesita redstone, incondicional, con señal continua; segundo y tercero cadena, siempre activo, incondicional. Desactivar variantes antiguas de levitación mientras se prueba. Un comando por bloque:

1.

<pre>execute as @a[tag=spider_man,nbt={OnGround:false}] at @s rotated ~ 0 unless block ^ ^1 ^1 minecraft:air run effect give @s minecraft:levitation 1 1 true</pre>

2.

<pre>execute as @a[tag=spider_man,nbt={OnGround:false}] at @s unless block ~ ~2 ~ minecraft:air run effect give @s minecraft:levitation 2 1 true</pre>

3.

<pre>effect clear @a[tag=spider_man,nbt={OnGround:true}] minecraft:levitation</pre>

Prueba en suelo plano frente a pared: no debe empezar sin saltar; saltar pegado a ella debe iniciar subida, y el techo debe seguir funcionando mientras está en el aire. Al apartarse tanto de pared frontal como del techo, deja de renovarse y conserva el residual configurado de uno o dos segundos; al tocar suelo se intenta retirar inmediatamente en el siguiente ciclo. Comprobar también ausencia de activación al mirar al suelo. Probar inicialmente lejos de redes para no mezclar gravedad x4 y escalada.

**Pendiente de prueba:** el control OnGround en su servidor y la retirada individual. No atribuir a estos comandos una conservación de levitación de otras fuentes: el tercer comando limpia ese tipo de efecto en portadores en el suelo. La pérdida del tag deja el residual ya aplicado; no se introduce ahora seguimiento extra para limpiarlo instantáneamente. La ficha principal sigue sin cambios hasta validar esta secuencia completa.

## Techo confirmado; siguiente ajuste de detección frontal horizontal

El usuario probó el comando superior en la cadena conectada y confirmó que mantiene levitación bajo un bloque sobre el personaje aunque no lo esté mirando. Es coherente con la comprobación relativa ~ ~2 ~; no se cambia esa mecánica. No se infiere de ese reporte una causa definitiva del problema inicial del servidor.

### Prueba pendiente: añadir solo rotated ~ 0 al primer comando

Se conserva la comprobación superior y su cadena siempre activa e incondicional. Se sustituye únicamente el primer comando, en repetición necesita redstone incondicional, por:

<pre>execute as @a[tag=spider_man] at @s rotated ~ 0 unless block ^ ^1 ^1 minecraft:air run effect give @s minecraft:levitation 1 1 true</pre>

La rotación de ejecución conserva la orientación horizontal y fija la inclinación de cálculo en cero, sin mover la cámara del jugador. Así ^ ^1 ^1 comprueba una posición un bloque por encima de sus pies y uno hacia delante horizontalmente en lugar de inclinar esa comprobación al mirar al suelo. No se cambia distancia, nivel ni duración. Se conserva el criterio de bloque distinto de minecraft:air; no se introduce todavía filtro de colisión o material.

Probar en suelo plano sin pared delante ni techo cercano: mirar abajo no debería iniciar levitación. Después probar frente a una pared cambiando la inclinación de la mirada; la dirección horizontal sigue importando. La comprobación superior aprobada debe seguir manteniendo levitación bajo techo. Mantener desactivado el tercer comando de retirada durante esta prueba para aislar el cambio.

El requisito de salto todavía no se añade: se abordará después de confirmar la eliminación de la activación por suelo. No presentar este estado intermedio como escalada final ni cambiar todavía la ficha vigente. Movilidad en redes, filtros, trayectoria y limpieza se conservan.

## Detección frontal confirmada; añadir techo como condición independiente

El usuario probó solo el primer comando: levita mirando al suelo y a paredes de frente en direcciones horizontales; al apartar la mirada de la pared cae. No funciona con un bloque por encima. Se confirma ese alcance del primer comando, no una causa definitiva del problema inicial del servidor ni una prueba de funcionamiento con las cadenas restauradas.

El primer comando depende de la orientación local del jugador; por eso mirar al suelo puede cumplir la comprobación de un bloque distinto de aire. El objetivo sigue siendo corregir después esa activación indeseada y recuperar el salto de enganche que el usuario prefiere. No modificar aún el primer comando mientras se prueba techo.

### Siguiente prueba: segundo bloque de techo

Conservar el primer comando de repetición y añadir de nuevo solo la siguiente cadena, configurada cadena, siempre activo, incondicional, orientada tras el bloque de repetición. Mantener señal continua del primero y la zona cargada. El tercer comando de retirada sigue desactivado durante esta prueba.

<pre>execute as @a[tag=spider_man] at @s unless block ~ ~2 ~ minecraft:air run effect give @s minecraft:levitation 2 1 true</pre>

La configuración incondicional es relevante: la detección de techo debe poder ejecutarse cuando no se detecte pared frontal. No se conoce si la cadena anterior era condicional; no atribuirle ese fallo sin confirmación. Siempre activo y condición son ajustes distintos.

La comprobación usa un bloque dos unidades por encima de los pies con coordenadas relativas del mundo, no un rayo hacia donde mira. Probar bajo un techo situado en esa posición, sin pared frontal que active el primer comando. Debe renovar levitación por la comprobación superior y dejar de renovarla al salir de debajo del techo si tampoco se cumple la frontal; queda el tiempo residual configurado. Probar lejos de telarañas para evitar sus modificadores de gravedad.

Estado: prueba pendiente. La ficha actual no cambia. Después se revisarán suelo, salto inicial y salida de la escalada sin modificar los módulos aprobados.

## Renovación directa confirmada; aislar detección frontal

El usuario probó la aplicación directa en el bloque de repetición del servidor y reportó levitación sostenida, sin agotarse mientras el bloque seguía activo. Se confirma renovación continua en esa prueba, no una duración infinita intrínseca del efecto ni ausencia de toda posible interferencia en otras circunstancias.

### Siguiente prueba pendiente: solo primer comando original

Restaurar el primer comando con su condición frontal y mantener desactivadas las cadenas de techo y retirada durante la comparación. Bloque repetición, necesita redstone, incondicional, alimentado continuamente y zona cargada:

<pre>execute as @a[tag=spider_man] at @s unless block ^ ^1 ^1 minecraft:air run effect give @s minecraft:levitation 1 1 true</pre>

Jugador con spider_man frente a una pared vertical, mirando horizontalmente hacia ella y manteniéndose cerca mientras sube. Observar si la subida se sostiene o se corta antes de alcanzar el borde superior; después apartar la mirada y observar el agotamiento del efecto. Realizar lejos de las redes del poder para evitar gravedad aumentada de su circuito de movilidad. Esta prueba no exige salto inicial: el tercer comando de suelo permanece desactivado solo para aislar la detección. La mecánica final deseada sigue siendo saltar y engancharse.

No cambiar alcance, nivel ni duración. Si solo este comando se corta, continuar comprobando pérdida de condición frontal; si se mantiene, aislar después la comprobación de techo en su cadena. No declarar causa resuelta hasta observar el resultado. La ficha y los demás módulos se conservan.

## Escalada: comparación exacta de local y servidor

El usuario aportó los comandos: servidor tiene dos bloques (frente y encima); local tiene esos mismos dos y un tercero que retira levitación de @a si un portador tiene bloque distinto de aire un bloque debajo. Primer bloque repetición necesita redstone; siguientes cadena siempre activo. No precisó condición de las cadenas. Se transcriben sin escapes de Markdown en ~ y con namespace explícito minecraft:air; no se atribuye ese formato a una corrección de mecánica.

### Servidor: dos comandos aportados

<pre>execute as @a[tag=spider_man] at @s unless block ^ ^1 ^1 minecraft:air run effect give @s minecraft:levitation 1 1 true</pre>

<pre>execute as @a[tag=spider_man] at @s unless block ~ ~2 ~ minecraft:air run effect give @s minecraft:levitation 2 1 true</pre>

### Local: tercer comando adicional

<pre>execute as @a[tag=spider_man] at @s unless block ~ ~-1 ~ minecraft:air run effect clear @a minecraft:levitation</pre>

El usuario reporta que local exige saltar para engancharse a una pared y permite continuar bajo techo; quiere conservar esa mecánica. El servidor muestra levitación que aparece y desaparece rápidamente, incluso con pared de hierro igual a la de local. La diferencia de comandos por sí sola no demuestra una incompatibilidad del servidor ni que la limpieza global esté actuando: la versión de servidor aportada no tiene effect clear. La hipótesis previa de interferencia de @a no explica directamente ese fragmento. No invalidar la preferencia histórica por el comando local ni cambiarlo todavía.

Los comandos de servidor solo aplican el efecto cuando coinciden las comprobaciones; si dejan de cumplirse, el efecto aplicado no es infinito. La orientación local ^ ^1 ^1 también depende de dónde mira el jugador. Todavía no se ha aislado pérdida de condición, ejecución del circuito u otra interferencia. No afirmar una causa a partir de la percepción de interrupción.

### Diagnóstico mínimo: renovación sin comprobaciones

Prueba temporal en el servidor, sin editar la ficha ni las mecánicas aprobadas. Guardar el primer comando original; desactivar los demás bloques de escalada durante la prueba. Sustituir temporalmente el primer bloque por:

<pre>effect give NOMBRE_JUGADOR minecraft:levitation 1 1 true</pre>

Reemplazar NOMBRE_JUGADOR por el jugador de prueba. Configurar repetición, necesita redstone, incondicional y alimentar de forma continua durante unos segundos, manteniendo la zona cargada; después apagar. El objetivo individual evita elevar otros portadores conectados. Se conserva nivel y duración del primer comando; solo se retiran sus condiciones de posición y tag para diagnosticar la renovación.

Si el efecto se mantiene sin cortes, la renovación funciona en esa prueba y corresponde aislar las detecciones/condiciones originales. Si sigue interrumpiéndose, revisar señal de redstone, ejecución y otras órdenes o sistemas que afecten al jugador. Ninguno de los resultados prueba por sí solo una causa única. Al terminar, restaurar el comando original y su montaje; no dejar la levitación incondicional como implementación final.

Estado: prueba pendiente. No cambia trayectoria, movilidad en redes, objetos ni limpieza. Las barras invertidas ante ~ en el mensaje se tratan como escapes de texto; no introducirlas en el bloque del juego.

## Retirada y caducidad confirmadas: etapa cerrada

El usuario confirmó que, conservando tiempo_telarana, las redes existentes desaparecen después de retirar el poder al jugador. Autorizó conservar únicamente la retirada del tag y excluir la eliminación del objetivo. La ficha ya cumple esa secuencia: solo tag NOMBRE_JUGADOR remove spider_man. Se verificó que no contiene scoreboard objectives remove tiempo_telarana como comando vigente y se aclaró que tiempo_telarana es un objetivo de tipo dummy, distinto de los marcadores de las redes.

Se cierran las etapas de movilidad en redes, trayectoria, objeto marcado/nombre, exclusividad por tipo de bola y limpieza/retirada según los resultados reportados. No se amplían las pruebas a dimensiones, servidor, concurrencia ni controles no ejecutados. Las redes existentes siguen su contador; los circuitos de seguimiento y limpieza permanecen cargados y activos.

La única etapa funcional acordada pendiente es revisar la escalada por levitación: activación indeseada al mirar al suelo y comportamiento en paredes, con el antecedente de diferencias entre solitario y servidor. No se cambia todavía ese circuito ni se afecta a las partes ya aprobadas. Los estados pendientes de secciones anteriores reflejan momentos históricos y deben leerse junto a este cierre.

## Limpieza confirmada; redes persistentes al borrar el objetivo

El usuario confirmó retirada de los objetos marcados, limpieza del suelo y eliminación al recoger una copia guardada en un cofre. No se registra limpieza directa del interior del cofre: actúa cuando la copia entra al inventario de un no portador. No se especificaron dimensiones ni se añade validación de otras pruebas por inferencia.

Reportó además que, al borrar tiempo_telarana durante la retirada, las redes existentes quedan en el mundo y vuelven a poder caducar tras reasignar el poder/recrear el objetivo. Este reporte concuerda con la dependencia del contador, ya corregida en la ficha en la etapa anterior. No se considera que el montaje del juego ya haya recibido esa corrección documental: se debe retirar del montaje la orden antigua scoreboard objectives remove tiempo_telarana y usar solo la retirada del tag para un jugador.

### Solución operativa y recuperación

Conservar permanentemente el objetivo compartido mientras exista la instalación. Retirar únicamente spider_man del jugador; no borrar el objetivo ni apagar el circuito de duración. Las cadenas de incremento y retirada son incondicionales y deben seguir funcionando sin portadores. No hace falta forzar el tiempo antes de retirar el tag: las redes terminan de forma independiente mediante sus marcadores.

Si ya se borró el objetivo, después de impedir que el bloque viejo lo siga borrando, ejecutar una vez desde chat:

<pre>/scoreboard objectives add tiempo_telarana dummy</pre>

Si informa que ya existe, no eliminarlo ni reinicializarlo. Con el circuito alimentado, los marcadores que sigan vivos y cargados podrán volver a incrementar su contador; al alcanzar 100 se retirarán las redes de sus posiciones y después los marcadores. Borrar el objetivo eliminó las puntuaciones previas, de modo que la duración se reinicia para esos marcadores al volver a añadirles puntos. Esto no crea marcadores que ya se hayan eliminado ni limpia cobweb que haya quedado sin marcador.

La retirada normal desde el chat del jugador es:

<pre>/tag @s remove spider_man</pre>

**Pendiente de prueba:** retirar tag conservando objetivo y comprobar que las redes existentes caducan sin reasignar el poder. Probar recuperación tras recrear objetivo si quedan redes con sus marcadores. No forzar limpieza global de cobweb ni borrar marcadores antes de sus redes. La ficha se aclaró sin cambiar ningún comando vigente; la eliminación antigua del objetivo queda solo en historial.

## Retirada individual y limpieza listas para prueba

El usuario autorizó desarrollar retirada/limpieza cuando el jugador pierda spider_man y realizará la prueba de quitar el tag. Se revisaron los cuatro comandos de limpieza existentes: su predicado ya coincide con poder:spider_man del objeto Telarañas. Se conservan idénticos. Primer bloque repetición, siempre activo, incondicional; tres cadenas siempre activas e incondicionales. Inventarios de jugadores conectados sin tag y objetos marcados tirados en zonas cargadas de las tres dimensiones. Las bolas normales se conservan.

### Corrección necesaria de la retirada documentada

La ficha antigua retiraba spider_man de todos los portadores conectados y eliminaba tiempo_telarana. Eso deja sin contador compartido a los marcadores vivos y puede impedir que completen su retirada, además de afectar otros portadores. Se sustituye por retirada individual con tag NOMBRE_JUGADOR remove spider_man, sin eliminar el objetivo. Los comandos antiguos se conservan aquí como registro de migración, no como secuencia vigente:

- tag @a[tag=spider_man] remove spider_man
- scoreboard objectives remove tiempo_telarana

No ejecutar la eliminación de tiempo_telarana durante esta prueba. Se conserva el objetivo compartido para que las redes existentes caduquen y otros portadores sigan funcionando. No se cambia su duración ni el circuito de levitación. Si el objetivo ya se borró en el mundo, habrá que reponerlo antes de atribuir un fallo a la limpieza de objetos.

### Prueba del usuario, todavía pendiente

Con limpieza y movilidad cargadas y activas, retirar el propio tag desde el chat:

<pre>/tag @s remove spider_man</pre>

Comprobar que desaparecen las Telarañas marcadas del inventario y no se reponen, mientras las bolas normales permanecen. La limpieza solo compara custom_data, no el nombre visible. Los modificadores propios de movimiento y gravedad deben desaparecer al siguiente ciclo; Weaving conserva el residual de hasta cinco segundos ya aprobado.

La limpieza del suelo borra copias marcadas incluso si el portador conserva el tag, para evitar acumular recursos. Las bolas normales tiradas se conservan. Cofres y contenedores portátiles no se inspeccionan: la copia guardada se limpia al entrar al inventario de alguien sin tag. Solo entidades cargadas y jugadores conectados. No se borran proyectiles lanzados; una bola marcada cuyo lanzador ya no tenga tag deja de cumplir el filtro de generación, pero las redes existentes terminan por su contador.

Esta retirada no prueba por sí sola el filtro de proyectil de un no portador: el clear puede eliminarle las bolas antes de lanzarlas. Distinguir observaciones. La prueba de limpieza Spider-Man sigue pendiente; no heredar resultados de otros poderes.

## Objeto exclusivo confirmado e incorporado

El usuario confirmó que sustituyó el comando en el circuito real: la bola marcada genera telarañas y las bolas normales y antiguas utilizadas en su prueba no las generan. Se registra como validación positiva y negativa del filtro de custom_data en el proyectil, conservando la trayectoria aprobada. No se infiere una prueba independiente de un lanzador sin tag, ni de varios portadores o limpieza.

Se incorporaron a la ficha los dos comandos preparados: reposición por marca con nombre Telarañas rojo/azul y generación filtrada por Item.components.custom_data más on origin/tag. Solo esos dos comandos cambian; los 21 restantes se conservan idénticos. La marca sigue siendo poder:spider_man para mantener la relación con la limpieza existente. Se confirmó funcionalmente el predicado sobre el stack del proyectil mediante esta prueba; la primera captura sin componentes no invalida el resultado posterior.

Las bolas antiguas que el usuario probó quedan registradas como no activadoras en esa prueba. No se concluye que toda bola antigua sea rechazada: cualquier copia que conserve la misma marca es válida para el filtro, aunque su nombre visible o antigüedad sean distintos. El nombre no es una contraseña de activación.

Pendiente de revisión por etapas: retirada/exclusividad del objeto y prueba del lanzador sin tag, distinguiendo que la limpieza puede impedir conservar el objeto antes de lanzarlo. Levitación queda al final por instrucción expresa. Los bloques temporales de captura de datos ya no son necesarios para usar el circuito; pueden mantenerse apagados. No borrar bloques de trabajo ni archivos históricos automáticamente.

## Marca del objeto sostenido confirmada; prueba dirigida del filtro

La segunda imagen muestra que la consulta de SelectedItem devuelve {poder:"spider_man"}. Se confirma la marca en el objeto que el usuario sostiene. No se atribuye a esa imagen una confirmación del nombre/color ni de la transferencia de componentes a la bola lanzada. La primera captura confirmó Item, pero el stack capturado no mostró components.

Para avanzar con una prueba observable se prepara el filtro completo como candidato, sin incorporarlo a la ficha: el predicado comprueba Item.components del proyectil y luego el tag del lanzador mediante on origin. La forma Item.components es la estructura a verificar con el resultado de esta prueba, no un dato ya observado en la primera captura. Esto sustituye el paso de captura adicional propuesto antes; no declara resuelta la incertidumbre ni inventa una transferencia confirmada.

Conservar el bloque de repetición previo execute if entity @a[tag=spider_man]. Sustituir solo su cadena de creación de marcadores, manteniendo cadena, siempre activo, condicional:

<pre>execute as @e[type=minecraft:snowball,nbt={Item:{components:{"minecraft:custom_data":{poder:"spider_man"}}}}] at @s on origin if entity @s[type=minecraft:player,tag=spider_man] if block ~ ~ ~ minecraft:air run summon minecraft:interaction ~ ~ ~ {Tags:["reloj_telarana"],Passengers:[{text:""}]}</pre>

At @s fija la posición de la bola antes de cambiar al lanzador; no añadir at @s después de on origin. Se conserva la posición aprobada, summon, Passengers y el resto de los circuitos. No comprobar la mano actual ni el nombre visible como condición final.

Pruebas iniciales: bola marcada de la pila consultada lanzada por el jugador con spider_man debe crear redes; bola normal lanzada por el mismo jugador no debe crearlas. Desactivar y sustituir la generación antigua, no mantener ambas activas, para que la prueba negativa tenga valor. Si la marcada tampoco genera, registrar si hubo error de sintaxis o simplemente no apareció red y volver a capturar esa bola; no atribuir automáticamente el resultado al tag ni dar por probado que Minecraft elimina la marca.

**Estado: candidato pendiente de prueba.** Después de un resultado positivo y negativo, completar control de lanzador sin tag en una prueba que no quede impedida por limpieza de inventario. La ficha pública local conserva por ahora la generación probada anterior. La marca de limpieza existente y los cinco comandos de movilidad no se modifican.

## Captura recibida: campo Item confirmado, marca aún no acreditada

La imagen aportada por el usuario muestra la consulta de pruebas:spider_man bola y el campo Item con count:1 e id:"minecraft:snowball". No aparecen components ni minecraft:custom_data dentro de ese Item en la captura. No se interpreta como prueba de que la bola lanzada conserve la marca ni como prueba de que el juego la elimine: pudo capturarse una bola normal o datos anteriores. El filtro definitivo sigue pendiente.

La barra de título muestra Minecraft 26.3 - Multiplayer (3rd-party Server): se identifica la versión del cliente en esta prueba. No acredita la versión ni el software del servidor, una instalación vanilla de servidor ni las versiones de las pruebas históricas. No se copian coordenadas ni identificadores personales de la imagen.

### Siguiente comprobación única

Con la bola nueva llamada Telarañas seleccionada en la mano principal, ejecutar desde el chat:

<pre>/data get entity @s SelectedItem.components."minecraft:custom_data"</pre>

Resultado esperado de la marca del objeto sostenido: {poder:"spider_man"}. Si no existe esa ruta, no está acreditada la marca en el objeto seleccionado. Si la marca sí está, el siguiente paso será capturar una bola lanzada de esa pila sin otros proyectiles cercanos y descartar una captura vieja. No cambiar todavía generación para filtrar por una marca que no se ha observado en el proyectil. Esta comprobación del objeto sostenido es diagnóstico, no se usará como condición final de propiedad del proyectil.

La ruta externa del stack del proyectil es Item, confirmada directamente por la evidencia actual. No suponer contents ni item minúscula. La ficha principal no se modifica en esta etapa.

## Nombre Telarañas y filtro de objeto: preparación de prueba

Se conserva custom_data={poder:"spider_man"}, ya presente en entrega y limpieza. El usuario autoriza nombre Telarañas rojo/azul y exclusividad de generación por marca del objeto y tag del portador. La identidad no debe depender del nombre visible ni de qué lleva en la mano después de lanzar. El nombre se prepara con dos segmentos sin cursiva.

### Sustituir entrega para la prueba

Conservar repetición, necesita redstone, incondicional, y la señal permanente del bloque actual. Reposición de dos bolas si no hay una marcada en la barra rápida; una bola normal ya no bloquea recibir la del poder.

<pre>execute as @a[tag=spider_man] unless items entity @s hotbar.* minecraft:snowball[minecraft:custom_data~{poder:"spider_man"}] run give @s minecraft:snowball[minecraft:custom_data={poder:"spider_man"},minecraft:custom_name=[{text:"Tela",color:"red",italic:false},{text:"rañas",color:"blue",italic:false}]] 2</pre>

Sacar de la barra rápida las bolas antiguas marcadas para que el sistema entregue las que tienen nombre nuevo. Las marcas antiguas no se eliminan ni se migran automáticamente; si comparten custom_data siguen siendo copias del poder. No exigir nombre como condición de identidad.

### Verificar marca en el proyectil antes de cerrar el filtro

La documentación oficial consultada no acredita de forma suficiente para la instalación actual si el stack lanzado se guarda bajo Item o item ni si expone contents. No inventar esa ruta ni usar el slot de ítem tirado sin prueba. El chat de comandos coincide en capturar primero los datos del proyectil. La versión exacta del usuario no fue indicada; Java 26.3 es la referencia estable según el índice oficial consultado el 17 de noviembre.

Bloque temporal de repetición, necesita redstone, incondicional. Activarlo, lanzar una bola marcada cerca sin otros proyectiles de prueba en vuelo, apagarlo y consultar el storage desde chat. El bloque conserva la última entidad capturada aunque desaparezca:

<pre>execute as @e[type=minecraft:snowball,limit=1,sort=nearest] run data modify storage pruebas:spider_man bola set from entity @s</pre>

<pre>/data get storage pruebas:spider_man bola</pre>

El namespace de storage es un identificador vanilla, no requiere datapack ni archivos del juego. La captura solo lee la bola y escribe sus datos en almacenamiento de diagnóstico del mundo. No altera el proyectil ni el circuito de redes. Si indica que no hay datos, no se capturó la bola; no inferir ausencia de marca por ese fallo. Compartir el resultado para fijar el campo real. No dejar el bloque de captura activo después de la prueba.

El filtro definitivo comprobará la marca antes de `on origin if entity @s[type=minecraft:player,tag=spider_man]`. Fijar posición con at @s mientras el ejecutor todavía es la bola; no volver a fijarla a la posición del portador después de origin. No se integra un filtro incompleto que solo compruebe tag del jugador.

Pruebas finales del filtro, una vez preparado: marcada+tag genera red; normal+tag no; marcada sin tag no; normal renombrada como Telarañas no. La limpieza vigente puede retirar una marcada de un no portador antes de que la lance; si eso ocurre es prueba de limpieza, no de comprobación del proyectil.

Fuentes oficiales: [Java 1.19.4: origin del proyectil](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-19-4), [Java 1.21.5: componentes de texto directos](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-5) e [índice de estables](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs). Propuestas pendientes de prueba. La ficha incorpora solo la trayectoria confirmada; entrega nueva y filtro se cierran después de comprobarlos. Levitación queda para el final por instrucción expresa.

## 17 de noviembre: trayectoria confirmada e incorporada

El usuario confirmó el comando sin positioned ^ ^1 ^: las redes salen desde el portador en las direcciones probadas, incluido hacia arriba; conserva las mejoras de movilidad y le gusta el funcionamiento actual. Se integró en la ficha únicamente esa eliminación, sin cambiar filtros, duración, marcadores, movilidad ni escalada.

El usuario pide ahora nombre Telarañas rojo/azul, identificación por custom_data y generación exclusiva por bolas marcadas de un portador con spider_man. La marca poder:spider_man ya estaba en la entrega y limpieza; se conservará para no romperlas. El filtro de marca debe comprobar el objeto representado por el proyectil, no el objeto actual de la mano. La levitación queda expresamente para el final.

## 17 de noviembre: movilidad aprobada e incorporada a la ficha

El usuario confirmó que le gusta el sistema actual y autorizó incorporar esta parte del funcionamiento. Se añadieron a la ficha los cinco comandos exactos del último circuito: movimiento 0.8, Weaving 5 segundos nivel I, gravedad x4, todos con la misma proximidad de radio 2 a reloj_telarana. La retirada de los dos modificadores se mantiene en cada ciclo. Se conserva su aprobación del comportamiento observado sin inferir pruebas nuevas de versiones, multijugador, retirada del tag o desmontaje.

Los cinco comandos anteriores de prueba pasan a ser implementación vigente. No ejecutar variantes antiguas además del circuito final. Se verificó que ningún comando anterior de la ficha fue sustituido en esta integración; únicamente se añadieron los cinco de movilidad y su explicación. Los demás módulos permanecen pendientes de revisión según su alcance.

## Siguiente prueba: generar la red en la posición real de la bola

El usuario pidió que las redes dejen de salir por encima y sigan una trayectoria más fiel al lanzamiento. Se propone quitar solamente positioned ^ ^1 ^ del comando de creación de marcadores. La referencia pasa a ser la posición real de la bola, no una altura fija respecto al jugador: el rastro seguirá la curva del proyectil y puede subir o bajar según el lanzamiento.

Sustituir solo el comando de la cadena de generación de marcadores; conservar cadena, siempre activo, condicional y el resto de la secuencia. No cambiar todavía filtro de lanzador, Passengers, duración de redes, movilidad o escalada.

<pre>execute as @e[type=minecraft:snowball] at @s if block ~ ~ ~ minecraft:air run summon minecraft:interaction ~ ~ ~ {Tags:["reloj_telarana"],Passengers:[{text:""}]}</pre>

**Estado:** preparado para probar, no integrado en la ficha. Probar un tiro horizontal, uno hacia arriba y uno hacia abajo. Observar tanto colocación como movilidad cerca del rastro, pues los mismos marcadores activan los bonos. La muestra por ejecuciones puede dejar huecos entre posiciones; quitar el desplazamiento no garantiza una estela completamente continua ni genera un hilo desde la mano del jugador.

### Puntos restantes mencionados por el usuario

- Posición del rastro: siguiente prioridad, según la prueba anterior.
- Identificación del lanzador: el selector actual todavía permite procesar bolas de otros jugadores cuando existe un portador; ajustar y probar por separado.
- Nombre del objeto: Telarañas con colores rojo y azul, conservando minecraft:snowball.
- Escalada mediante levitación: revisar activación al mirar al suelo y diferencias observadas entre solitario y servidor.
- Revisión final de exclusividad y limpieza del objeto marcado: el usuario la dejó para después de resolver las habilidades. No atribuir a la prueba de movilidad una validación de esa limpieza.

## 17 de noviembre: movimiento más fluido y ajuste de intensidad

El usuario probó la última variante de gravedad por radio y reportó un movimiento más cómodo y fluido. Pide alargar Weaving, acepta expresamente su residual al salir y solicita un aumento moderado de velocidad, manteniendo exactamente la retirada rápida actual. No se acredita una prueba nueva de desmontaje, varios portadores ni la versión exacta del juego.

### Ajustes solicitados para la siguiente prueba

- Bloque 2: bono de velocidad de 0.6 a 0.8. En ausencia de otras diferencias, pasa de factor 1.6 a 1.8, un incremento del 12.5 % respecto al valor anterior. Conservar la operación y el identificador.
- Bloque 3: Weaving de 1 a 5 segundos, mismo nivel I y partículas ocultas. Se renueva cerca de los marcadores; puede durar hasta cinco segundos después de dejar esa cobertura. Weaving conserva además su comportamiento vanilla de generar redes al morir; el cambio solo aumenta duración.

Los bloques 1, 4 y 5 no cambian; el sexto anterior permanece desactivado. La gravedad se conserva en x4 y el radio sigue siendo 2, centrado 0.9 bloques sobre los pies. La velocidad se retira en cada ciclo y solo se reañade con tag y cercanía: no adquiere una duración de cinco segundos. Al salir del radio o perder el tag, deja de reañadirse en la siguiente ejecución. Solo afecta jugadores conectados con el circuito cargado y activo.

### Circuito vigente de prueba completo

Primero: repetición, siempre activo, incondicional. Segundo a quinto: cadena, siempre activo, incondicional, en orden. Un comando por bloque. Esta secuencia reúne los comandos vigentes para evitar mezclar etapas anteriores; no implica que los dos valores nuevos estén probados.

1.

<pre>execute as @a run attribute @s minecraft:movement_speed modifier remove poderes:spider_red</pre>

2.

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..2] run attribute @s minecraft:movement_speed modifier add poderes:spider_red 0.8 add_multiplied_total</pre>

3.

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..2] run effect give @s minecraft:weaving 5 0 true</pre>

4.

<pre>execute as @a run attribute @s minecraft:gravity modifier remove poderes:spider_caida</pre>

5.

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..2] run attribute @s minecraft:gravity modifier add poderes:spider_caida 3 add_multiplied_total</pre>

**Estado:** mayor fluidez con la variante anterior confirmada por el usuario; Weaving 5 segundos y velocidad 0.8 pendientes de prueba. No usar el Weaving manual de 30 segundos para evaluar la duración nueva: esperar a que termine primero. La detección sigue siendo cercanía a marcadores de redes del poder, no todo cobweb ni contacto exclusivo con el bloque.

La ficha principal permanece sin cambios mientras continúa el pulido. No cambiar trayectoria, escalada, objetos ni limpieza en esta etapa. Mantener las instrucciones de retirada explícita de los modificadores si se desmonta o apaga el circuito mientras están aplicados.

## 17 de noviembre: aclaración del resultado y continuidad entre redes

La aclaración más reciente del usuario prevalece sobre su primera impresión: con Weaving mantenido manualmente sí sintió una caída más rápida. Notó tramos más lentos al pasar de una telaraña a otra y más rapidez en el centro que en los bordes. Se registra como percepción reportada; no demuestra qué efecto o atributo se interrumpe. No registrar como conclusión que Weaving no influye en su prueba. No se cambian fuerza de gravedad ni compensación horizontal.

### Prueba de continuidad por el radio ya aprobado

Propuesta diagnóstica, pendiente de prueba y aceptación como funcionamiento final. Las celdas usadas por la gravedad podrían dejar huecos en bordes mientras el jugador sigue tocando cobweb. Para comparar se usa para gravedad el mismo radio 2 de los marcadores que para velocidad y Weaving. Esto cambia expresamente el alcance: también modifica salto y caída en aire cercano a la red; no es contacto exclusivo, no detecta redes manuales y no debe incorporarse como solución final sin observar y aceptar ese efecto.

Conservar bloques 1–4 del circuito actual (movilidad, Weaving y retirada de gravedad), sustituir solo el comando 5 por el siguiente y desactivar el bloque 6 anterior. El bloque 5 mantiene cadena, siempre activo, incondicional. Al ser el sexto el último bloque, desactivarlo no corta otros bloques posteriores de esta prueba. Si el montaje real incluye más cadenas después, conservar la continuidad del circuito al apartar la orden antigua.

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..2] run attribute @s minecraft:gravity modifier add poderes:spider_caida 3 add_multiplied_total</pre>

Para comparar una sola diferencia de cobertura, mantener Weaving manualmente durante la misma duración de la comparación anterior: `/effect give @s minecraft:weaving 30 0 true`. No añadir un modificador manual de gravedad. Comparar en redes generadas por el poder mientras sus marcadores permanezcan, cruzando bordes y uniones. Registrar si desaparecen los cortes y si el cambio del salto fuera de la telaraña resulta aceptable. La desaparición de los propios marcadores sigue retirando la mejora.

El circuito de prueba queda en cinco comandos activos. El bloque 4 retira poderes:spider_caida en cada ciclo, por lo que al salir del radio o perder el tag se deja de reañadir. La limpieza explícita al desmontar sigue siendo `/attribute @s minecraft:gravity modifier remove poderes:spider_caida` desde el chat del portador. No probar apagar y dejar el modificador permanente.

La ficha principal no se modifica. Si la proximidad no es aceptable para gravedad, habrá que mejorar la detección de bloques sin convertir esta prueba en una implementación final.

## Diagnóstico confirmado: modificador presente en red y ausente fuera

El usuario consultó el modificador: obtuvo 3 dentro de una telaraña lanzada y ausencia fuera. También comprobó que se aplica a telarañas manuales. Se confirma la presencia/retirada en los instantes consultados y la selección por bloques de cualquier cobweb; no demuestra continuidad durante todo el movimiento ni confirma que ya perciba el descenso temporal como adecuado.

La gravedad usa celdas de bloque; velocidad y Weaving conservan radio 2 de reloj_telarana. Esta diferencia de detecciones podría afectar la consistencia, pero no se declara causa demostrada. En la prueba manual x4 se mantuvo Weaving temporalmente mediante un comando, mientras que la prueba automática solo lo renueva cerca del marcador.

### Siguiente comparación aislada, pendiente

Sin modificar los seis bloques, aplicar desde el chat del jugador:

<pre>/effect give @s minecraft:weaving 30 0 true</pre>

Durante esos 30 segundos, repetir la misma caída en la misma disposición de redes con la gravedad automática activa; no añadir el modificador manual de gravedad ni cambiar su valor. El efecto manual estabiliza Weaving durante la comparación y caduca solo. Evitar levitación durante la prueba como en la comparación manual anterior. Si se aprecia mejora consistente, revisar la cobertura de Weaving; si no, no atribuir la causa a esa hipótesis y revisar la continuidad/gravedad efectiva. No integrar ni ampliar aún los circuitos.

La gravedad se mantiene en amount 3 add_multiplied_total. La aplicación a cualquier telaraña es el comportamiento de sus comprobaciones actuales; no se convierte silenciosamente en una selección exclusiva de redes del poder. Ficha principal sin cambios.

## Aplicación temporal por dos celdas: sin mejora perceptible

El usuario no sintió que se aplicara la caída acelerada durante la prueba temporal en telarañas lanzadas. Se conserva como resultado negativo de percepción: no demuestra por sí solo que el modificador nunca exista ni invalida la prueba manual x4 confirmada. La comprobación de dos celdas puede omitir contacto lateral, pero la causa no está confirmada. No aumentar la fuerza ni cambiar alcance antes de comprobar activación.

### Diagnóstico mínimo pendiente

Mantener el circuito de seis bloques activo y, estando atrapado dentro de una telaraña del poder, consultar desde el chat del jugador:

<pre>/attribute @s minecraft:gravity modifier value get poderes:spider_caida</pre>

Un valor 3 confirma que el modificador está presente en ese instante. Un error de modificador inexistente indica que en ese instante no se está manteniendo. El comando consulta el valor del modificador, no la gravedad total. Una sola consulta no demuestra continuidad durante todo el movimiento. No pedir todavía una secuencia de pruebas larga ni cambiar la gravedad.

Según el resultado se revisará la detección/orden de ejecución o la diferencia entre la prueba manual y la aplicación temporal. La ficha principal se conserva y no se instala otra variante automáticamente.

## Gravedad x4 confirmada; aplicación temporal por contacto propuesta

El usuario confirmó descenso más rápido y salida más rápida de telarañas con gravedad x4; también probó telarañas verticales y sintió que no quedaba atrapado. Es prueba reportada, sin medición ni versión exacta. Solicitó que el atributo se aplique temporalmente durante interacción con telarañas.

Se conservan los tres bloques de velocidad/Weaving por cercanía al marcador en radio 2, ya aprobados. Para gravedad se elige una condición distinta: presencia de cobweb en las celdas de los pies o un bloque por encima. No ampliar gravedad a todo el radio 2, porque alteraría saltos y caídas cercanos sin estar en redes. No es una comprobación completa de toda la caja de colisión: un contacto exclusivamente por un borde puede no detectarse. Esta diferencia de alcance se explica en la entrega y queda pendiente de prueba. La gravedad se aplica durante todo contacto detectado, no únicamente al descender.

### Añadir después de los tres bloques de movilidad

Los tres nuevos son cadena, siempre activo, incondicional, con flechas en orden. El circuito completo queda en seis bloques; conserva su primera repetición siempre activa. La retirada se ejecuta primero para todos los jugadores conectados, incluidos quienes ya no tengan spider_man, y se reaplica solo a portadores en contacto detectado. Los modificadores ajenos y el valor base no se cambian.

4.

<pre>execute as @a run attribute @s minecraft:gravity modifier remove poderes:spider_caida</pre>

5.

<pre>execute as @a[tag=spider_man] at @s if block ~ ~ ~ minecraft:cobweb run attribute @s minecraft:gravity modifier add poderes:spider_caida 3 add_multiplied_total</pre>

6.

<pre>execute as @a[tag=spider_man] at @s if block ~ ~1 ~ minecraft:cobweb run attribute @s minecraft:gravity modifier add poderes:spider_caida 3 add_multiplied_total</pre>

Los bloques 5 y 6 añaden el mismo identificador: si ambas celdas contienen cobweb, el segundo add puede informar que ya existe, pero no añade otra copia ni multiplica por 4 de nuevo. Todas las cadenas son incondicionales para que esos fallos esperados no detengan las comprobaciones. La retirada del bloque 4 también puede informar ausencia cuando no existe el modificador.

**Pendiente de prueba:** entrar en redes generadas por el poder, caer y saltar dentro, salir y comprobar salto/caída normales fuera de las redes. También probar perder spider_man con el circuito activo. El modificador debe desaparecer al siguiente ciclo si ninguna celda cumple contacto o si pierde el tag. No se declara probado hasta recibir resultado. La movilidad horizontal sigue teniendo radio 2 y Weaving puede quedar un segundo residual; la gravedad no depende de duración de efecto.

Mantener circuito cargado y activo. Si se apaga mientras un jugador conserva el modificador, ejecutar desde su chat `/attribute @s minecraft:gravity modifier remove poderes:spider_caida`; el modificador no caduca solo. Para retirar toda la instalación, limpiar de jugadores conectados los dos modificadores propios spider_red (movement_speed) y spider_caida (gravity); los desconectados requieren limpieza al volver. Esta instalación de prueba no introduce automatización para usuarios desconectados.

La ficha principal sigue sin cambios. No se alteran trayectoria, levitación, daño por caída, objetos ni limpieza. Las fuentes de atributos y la referencia estable de esta revisión están documentadas en la prueba manual siguiente.

## Descenso con gravedad x2: resultado inconcluso

El usuario probó redes lanzadas con bola de nieve hacia abajo desde unos 3–4 bloques. Sin el modificador las redes desaparecían antes de tocar el suelo. Con el modificador x2 ocurrió lo mismo dos veces y en una tercera percibió un descenso más rápido. Se registra como percepción inconsistente, no como mejora confirmada ni medición. La desaparición de la red y la cobertura variable de marcadores pueden interferir en la comparación.

### Siguiente prueba manual: redes fijas y gravedad x4

Propuesta pendiente de prueba, sin modificar los bloques del poder. Colocar cobweb manualmente para que no caduque, lejos de marcadores que puedan borrarlo. Comparar desde el mismo punto, aproximadamente 3 bloques sobre esa red, dejándose caer en vez de saltar. Evitar levitación activa. Mantener Weaving constante en ambas comparaciones de forma manual, porque las redes manuales no reciben la renovación desde los marcadores.

1. Retirar primero el modificador anterior:

<pre>/attribute @s minecraft:gravity modifier remove poderes:spider_caida</pre>

Si ya se había retirado, el aviso de modificador ausente es esperado. No sustituir esto por un reset del atributo base.

2. Aplicar Weaving I durante 60 segundos para mantener igual esta variable en ambas caídas:

<pre>/effect give @s minecraft:weaving 60 0 true</pre>

Realizar la caída de referencia sin el modificador y volver al mismo punto. Si el efecto termina antes de completar ambas comparaciones, repetirlo con la misma duración y nivel.

3. Aplicar el nuevo valor al mismo identificador, ya retirado:

<pre>/attribute @s minecraft:gravity modifier add poderes:spider_caida 3 add_multiplied_total</pre>

El valor 3 implica factor 1+3=4; no significa gravedad x3. Repetir la misma caída. La gravedad sigue actuando fuera de las redes y sobre el salto mientras exista este modificador; todavía no está limitada al descenso ni al tag. La prueba compara comportamiento, no demuestra inmunidad al frenado vertical.

4. Al terminar, volver a ejecutar el comando de retirada del paso 1. Weaving caduca por sí solo tras sus 60 segundos. No dejar permanente el modificador de gravedad ni sumar otros identificadores para aumentar su efecto.

Si esta prueba no produce una mejora clara, revisar la hipótesis antes de aumentar más el valor. La ficha principal, daño por caída, levitación y los circuitos horizontales permanecen sin cambios. Limitar cualquier compensación al descenso requiere una etapa posterior; no se da por implementada ni suficiente por sí misma.

Fuente de gravedad: [Mojang, Java 1.20.5](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-20-5). Referencia estable Java 26.3 reconsultada el 16 de noviembre de 2026 en el [índice oficial](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs). No se conoce la versión exacta usada por el usuario.

## Radio 2 confirmado; descenso pendiente

El usuario confirmó que el circuito con radio 2 funciona y le gusta la movilidad mayor del portador cerca de las redes. Reportó que al saltar cae lentamente dentro de las telarañas y quiere mejorar el descenso. No se atribuye a ese reporte una medición de velocidad, una prueba específica de retirada del tag ni inmunidad completa. Se mantienen las diferencias conocidas entre cercanía al marcador y contacto con cualquier bloque cobweb.

### Prueba manual aislada de gravedad

**Propuesta, todavía no probada.** Conservar los tres bloques de movilidad horizontal y no añadir un circuito automático de gravedad. Comparar el descenso en el mismo grupo de redes antes y después de aplicar este comando desde el chat del propio jugador:

<pre>/attribute @s minecraft:gravity modifier add poderes:spider_caida 1 add_multiplied_total</pre>

El modificador multiplica por 2 la gravedad calculada previa al modificador, dentro de los límites del atributo. No fija ni sustituye el valor base. Puede cambiar la altura del salto y acelera la caída también fuera de las redes mientras exista; no está limitado al radio, al tag ni exclusivamente a la fase descendente en esta prueba manual. No representa inmunidad a cobweb ni garantía de reproducir una caída normal. Realizar una comparación desde poca altura con las mismas condiciones; si la levitación existente está actuando, su efecto puede interferir y debe registrarse antes de atribuir el resultado a gravedad.

Retirar el modificador al terminar desde el mismo chat:

<pre>/attribute @s minecraft:gravity modifier remove poderes:spider_caida</pre>

El modificador no caduca por tiempo ni por apagar los tres bloques existentes: su retirada es explícita. Conservar el comando de retirada para terminar la comparación. No cambiar daño por caída, jump_strength ni levitación como parte de esta prueba. Si la gravedad no mejora de manera apreciable el descenso, no aumentar valores indiscriminadamente ni dar la hipótesis por válida.

Fuente oficial: [Java 1.20.5, Attributes](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-20-5), gravedad como aceleración descendente; [Java 1.21, Attributes](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21), modificadores identificados y operaciones. Java 26.3 sigue siendo la referencia estable del [índice oficial](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs), consultado el 16 de noviembre de 2026. La versión exacta de las pruebas del usuario no se conoce.

La ficha principal no se modifica. Antes de integrar cualquier ajuste automático se debe confirmar su utilidad y acordar el alcance, ya que usar todo el radio 2 podría alterar saltos fuera de las telarañas.

## Prueba de cobertura: ampliar el radio del marcador a 2

El usuario reportó que la mejora no se activa en algunos puntos de las redes del poder, tampoco al saltar, y que no actúa en telarañas individuales colocadas manualmente. Eso confirma límites de cobertura de la aproximación por marcador; no se considera una prueba satisfactoria de inmunidad ni de toda la salida sin residual. No se cambian los valores de compensación ni la altura de referencia.

Por solicitud del usuario se prepara una ampliación de radio 1 a 2. Solo sustituir los comandos 2 y 3 del circuito independiente de tres bloques por los siguientes; conservar el primero de retirada del modificador y todas las cadenas incondicionales:

2.

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..2] run attribute @s minecraft:movement_speed modifier add poderes:spider_red 0.6 add_multiplied_total</pre>

3.

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..2] run effect give @s minecraft:weaving 1 0 true</pre>

**Estado: pendiente de prueba.** Comparar caminar y saltar dentro de las redes generadas por el poder. Es una esfera de 2 bloques alrededor de un punto 0.9 sobre los pies, referida a posiciones de reloj_telarana. Puede mejorar cobertura, pero el bono también se concede fuera de la telaraña hasta abandonar esa cercanía. No garantiza cubrir toda interacción con bloques de redes, y no resuelve redes manuales ni redes cuyo marcador desapareció. No aumentar el radio indefinidamente como sustituto del contacto real.

Si se requiere que el beneficio funcione en cualquier cobweb, la detección debe basarse en los bloques y necesita otra prueba. La preferencia por pocos bloques de comandos no prevalece sobre una detección correcta. La ficha principal sigue sin cambios.

## Segunda prueba: retirar la velocidad sin duración residual

El usuario confirmó que los cuatro comandos mejoran la movilidad y que la movilidad dentro de telarañas le parece adecuada. Rechazó la sensación de velocidad residual al salir: reporta que dura demasiado, sin medir segundos. No atribuir una duración exacta observada ni descartar interferencia de otros efectos. Solicitó detectar cercanía a un bloque en cualquier dirección y reducir bloques.

### Propuesta de tres bloques, pendiente de prueba

Se sustituye Velocidad III por un modificador propio de movement_speed de 0.6, operación add_multiplied_total. Es una compensación de partida comparable al bono de Velocidad III en ausencia de otras fuentes, no garantiza idéntico comportamiento con otras bonificaciones. No cambia el valor base del jugador ni elimina modificadores ajenos. Cada ciclo retira el modificador de todos los jugadores conectados y lo vuelve a añadir solo al portador que cumpla la cercanía; no acumula copias y no depende de una duración de poción. Todas las cadenas deben ser incondicionales: retirar un modificador ausente puede fallar y no debe impedir las siguientes órdenes.

Se reutilizan los auxiliares reloj_telarana del circuito original. La comprobación es una esfera de radio 1 alrededor de un punto 0.9 bloques sobre los pies del jugador. Mide cercanía a la posición del marcador, no contacto exacto con el bloque ni distancia a sus caras. No detecta telarañas vanilla colocadas manualmente. Se debe aceptar y probar esta diferencia antes de considerarla implementación definitiva. El usuario pidió distancia en cualquier dirección; no existe un selector de bloques equivalente a distance para detectar cualquier cobweb con un único if block.

Desactivar el circuito anterior de cuatro bloques y esperar a que sus efectos terminen antes de comparar; no mantener el efecto speed a la vez que el nuevo modificador. Mantener activos los circuitos que generan y retiran las telarañas. Primero: repetición, siempre activo, incondicional. Segundo y tercero: cadena, siempre activo, incondicional, orientados en orden. Mantener la zona cargada.

1.

<pre>execute as @a run attribute @s minecraft:movement_speed modifier remove poderes:spider_red</pre>

2.

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..1] run attribute @s minecraft:movement_speed modifier add poderes:spider_red 0.6 add_multiplied_total</pre>

3.

<pre>execute as @a[tag=spider_man] at @s positioned ~ ~0.9 ~ if entity @e[tag=reloj_telarana,distance=..1] run effect give @s minecraft:weaving 1 0 true</pre>

Probar atravesando las telarañas generadas por el poder mientras sus marcadores siguen vivos: aproximarse, pasar por dentro y alejarse más de un bloque del marcador. El bono de movimiento debe cesar en el siguiente ciclo activo fuera de la cercanía; weaving puede conservar su segundo residual. Probar también quitar spider_man: el primer bloque sigue retirando el modificador aunque el jugador ya no tenga el tag. No se ha ejecutado esa prueba aquí.

Si se detiene este circuito mientras un jugador conserva el modificador, este no se retira automáticamente. Para finalizar la prueba, desactivar primero el circuito y ejecutar desde el chat: `/execute as @a run attribute @s minecraft:movement_speed modifier remove poderes:spider_red`. No borra efectos externos. Solo actúa sobre jugadores conectados; un jugador desconectado al retirar la instalación deberá recibir la limpieza cuando vuelva.

Fuentes: [cambios oficiales de atributos y modificadores en Java 1.21](https://feedback.minecraft.net/hc/en-us/articles/27547857163917-Minecraft-Java-Edition-1-21-Tricky-Trials). Referencia estable: Java 26.3 según el [índice oficial](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs), revisado el 16 de noviembre de 2026. La versión exacta de las pruebas del usuario sigue sin identificarse.

No se modifica la ficha principal ni la trayectoria, levitación, nombre o limpieza de objetos. La detección de cualquier telaraña en un volumen tendría que usar otras comprobaciones y se estudiaría por separado si la aproximación con marcadores no sirve.

## Prueba de movilidad: weaving confirmado y compensación propuesta

El usuario confirmó que weaving mejora el desplazamiento dentro de telarañas, pero no permite un movimiento suficientemente normal. Autorizó conservarlo y probar una compensación de velocidad al contacto. Weaving es un efecto, no un atributo. No se conoce la versión exacta ejecutada. La ficha principal todavía no incorpora estos cambios; no se modifica trayectoria, levitación, recursos ni limpieza.

Referencia estable de esta revisión: Java 26.3 según el [índice oficial de versiones estables](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs), consultado el 16 de noviembre de 2026. [Mojang documenta weaving](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21): mejora el movimiento en redes y también genera telarañas al morir. La confirmación del usuario solo corresponde a la mejora de desplazamiento, no a inmunidad ni a una prueba de muerte.

### Circuito independiente de prueba

Cuatro bloques en el orden siguiente. Primero: repetición, siempre activo, incondicional. Los otros tres: cadena, siempre activo, incondicional. Mantener la zona cargada y las flechas siguiendo el orden. Un comando por bloque; los jugadores de prueba necesitan spider_man.

1. Weaving en pies:

<pre>execute as @a[tag=spider_man] at @s if block ~ ~ ~ minecraft:cobweb run effect give @s minecraft:weaving 1 0 true</pre>

2. Weaving en cabeza:

<pre>execute as @a[tag=spider_man] at @s if block ~ ~1 ~ minecraft:cobweb run effect give @s minecraft:weaving 1 0 true</pre>

3. Velocidad III en pies:

<pre>execute as @a[tag=spider_man] at @s if block ~ ~ ~ minecraft:cobweb run effect give @s minecraft:speed 1 2 true</pre>

4. Velocidad III en cabeza:

<pre>execute as @a[tag=spider_man] at @s if block ~ ~1 ~ minecraft:cobweb run effect give @s minecraft:speed 1 2 true</pre>

Velocidad III es un punto inicial para comparar, no una promesa de inmunidad o velocidad normal. Se renuevan efectos de un segundo al detectar cobweb en la celda de los pies o un bloque por encima; al salir puede quedar ese segundo residual. La detección no cubre toda la caja de colisión, por lo que el roce por un borde puede no activarla. No usar ese caso como prueba de que la velocidad no ayuda estando completamente dentro.

Probar caminando por varias telarañas contiguas, salir y comprobar la transición. Comparar con weaving solo, sin otras fuentes de Velocidad durante esta prueba para poder interpretar el resultado. Una fuente previa más potente o duradera puede interferir; el circuito no guarda ni restaura efectos externos. La prueba no garantiza eliminar el frenado vertical ni estabilizar saltos. Para detenerla, desactivar el circuito y esperar un segundo; efectos preexistentes no se eliminan expresamente.

**Pendiente:** resultado de la combinación con Velocidad III, comodidad del movimiento y transición al salir. No borrar bloques ni marcadores para esta prueba.

## Resultados y decisiones

- Implementación original presentada como terminada según las pruebas históricas del autor.
- La limpieza de levitación dirigida a todos los jugadores se conserva deliberadamente según la experiencia reportada.
- Pendiente: limpieza nueva de bolas marcadas en inventario y suelo; las pruebas de perlas y cohetes no equivalen a probar este poder.
- Pendiente: alcance multijugador de los proyectiles y riesgo de que el portador quede atrapado en sus telarañas.

La versión exacta ejecutada, el número de jugadores y otras condiciones no indicadas por el autor permanecen sin registrar. Una comprobación documental o una prueba de otro poder no acredita estas condiciones.

<details>
<summary>Notas anteriores y fuentes</summary>

Archivo de las explicaciones anteriores, conservadas para consultar el origen de los cambios. Sus menciones de pruebas pendientes reflejan el momento en que se escribieron; los resultados actualizados figuran arriba.

Estado de desarrollo: terminado según las pruebas históricas del autor. La versión exacta de esas pruebas no está registrada en esta ficha; la compatibilidad con una versión estable posterior se revisa por separado.

Estado: limpieza de inventario de perlas confirmada por el autor al mantener la señal permanente, incluidas perlas recogidas de cofres y del suelo. Esa prueba no valida calaveras, bolas de nieve ni la nueva eliminación directa de entidades, que siguen pendientes de prueba.

Referencia documental: Java 26.3, estable consultada el 16 de noviembre de 2026 en el [índice oficial](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs). [Sintaxis oficial de custom_data, predicados y slot contents](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-20-5).

La entrega por tag y la selección posterior de proyectiles son pasos distintos: el selector de snowballs no contiene un filtro de propietario. Se conserva el comportamiento probado por el autor; cualquier ajuste de alcance o multijugador se discutirá por separado. La secuencia no define un contador específico de recarga para lanzar bolas.

Las cadenas deben ser incondicionales: que no haya objetos en un inventario o dimensión no debe impedir la limpieza siguiente. Como alternativa, el bloque de repetición puede usar **necesita redstone** si recibe una señal permanente, sin depender de un pulso breve. No sirve un pulso breve. Mantener cargada la zona de los bloques.

El primer comando limpia inventarios de jugadores conectados sin `spider_man`, incluso después de retirar el poder al último portador. Los siguientes eliminan todos los ítems marcados tirados en las tres dimensiones vanilla, aunque su dueño conserve el poder. No seleccionan proyectiles lanzados. Solo alcanzan entidades cargadas; las descargadas se revisarán al cargar su zona mientras el circuito siga activo.

Los objetos normales y las copias antiguas sin marca se conservan. No se inspeccionan cofres ni el contenido de contenedores portátiles; una copia marcada tomada de un cofre o del suelo se limpia cuando entra en el inventario de un jugador sin el tag. Los productos fabricados a partir de esos recursos quedan fuera. La marca identifica el poder, no un dueño individual.

</details>
