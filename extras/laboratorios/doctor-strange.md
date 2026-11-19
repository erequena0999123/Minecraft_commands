# Laboratorio: Doctor Strange

[Ficha y comandos](../../examples/superpowers/doctor-strange.md) · [Volver a laboratorios](../laboratorios.md)






## Cierre de las cuatro mejoras acordadas

El usuario confirmó que el aviso de disponibilidad aparece en pantalla, desaparece correctamente y permite volver a activar la habilidad. Reafirmó también que los relojes marcados se retiran al quitar el tag. El cuarto punto queda probado dentro de las condiciones que reportó; no se modifican los comandos tras esta confirmación.

| Punto | Resultado reportado |
| --- | --- |
| Área y restauración | Paralización y recuperación al salir del radio de 50 bloques o terminar la fase activa, probadas en Overworld, Nether y End |
| Reloj marcado y acceso | Solo el reloj con custom_data y un jugador con doctor_strange activan el poder |
| Limpieza | Funcionamiento confirmado; el usuario reiteró la retirada del reloj al quitar el tag |
| Aviso y reutilización | Mensaje visible y transitorio; nueva activación correcta después de la recarga |

La ficha principal queda cerrada para reutilizar su secuencia actual. Mantiene 23 comandos en bloques copiables y las especificaciones de montaje. Las cadenas de instalación y retirada se explicitan como incondicionales sin cambiar su orden. Las mejoras futuras se tratarán como una revisión nueva.

### Alcance de la confirmación

La versión exacta ejecutada no fue indicada. No se dispone de prueba simultánea de dos portadores ni de una comprobación específica de una criatura creada con NoAI:true. Tampoco se precisaron las dimensiones de prueba de la limpieza de objetos. Se conservan estos límites sin exigir nuevas pruebas para cerrar los cuatro puntos acordados. La revisión documental del lore no forma parte de este cierre.

<details>
<summary>Historial de propuestas, instalación y pruebas anteriores</summary>

Los estados pendientes que aparecen a continuación corresponden a cada etapa histórica. El estado actual está en el cierre anterior; consultar la ficha principal para copiar los comandos vigentes.

## Punto 4 incorporado: aviso individual de recarga

El usuario autorizó incorporar el mismo aviso estático de Kill aura. Se sustituyó la secuencia de dos bloques del temporizador por cinco: activación original, marca ds_aviso_listo cuando el contador vale 1, descuento original, actionbar para el portador marcado que llega a 0 y retirada de la marca. No cambia 5200, el umbral 2400, el radio 50 ni los circuitos ya probados. Se reutilizan los colores hexadecimales de Kill aura distribuidos por las letras de «Doctor Strange listo para usar».

**Estado:** incorporado en la ficha; pendiente de prueba en Minecraft. El aviso corresponde al final de la recarga completa. No se añade un segundo mensaje al terminar la fase de paralización.

### Instalación sobre el circuito existente

Sustituir únicamente el circuito anterior de activación y descuento por los cinco bloques de la ficha. No dejar otro bloque descontando tiempo_parado. Conservar la entrega, limpieza y seguimiento de criaturas. Mantener alimentado y cargado el circuito; las cuatro cadenas deben ser incondicionales. No volver a ejecutar la inicialización para instalar el aviso, pues pone a cero los contadores de todos los portadores conectados.

### Prueba pendiente

1. Activar normalmente y apartar el reloj de la mano principal para observar la disponibilidad sin reactivación inmediata.
2. Al terminar el efecto, las criaturas se liberan como antes. El aviso de disponibilidad debe esperar al final de toda la recarga.
3. Al llegar el contador a cero, comprobar que aparece brevemente «Doctor Strange listo para usar» en arcoíris sobre la barra rápida y no se repite mientras permanezca en cero.
4. Volver a sostener el reloj marcado para comprobar que se puede activar de nuevo.

La selección se hace por puntuación y tag de cada jugador; no se acredita una prueba simultánea de varios portadores. Si se mantiene el reloj en la mano, la reactivación automática existente sucede al ciclo siguiente del aviso; el mensaje no introduce una pausa ni requiere confirmación.

## Estado vigente: limpieza confirmada y prueba en End

El 16 de noviembre de 2026 el usuario confirmó que la limpieza del reloj funciona según lo descrito en el punto 3: conservación del reloj marcado con el tag, retirada sin el tag, eliminación del marcado en el suelo y conservación de relojes normales. No precisó en qué dimensiones hizo estas pruebas de limpieza; no extender su resultado automáticamente a las tres.

También confirmó la prueba del poder en el End, con el mismo comportamiento ya observado en Overworld y Nether: las criaturas se paralizan dentro del área durante el efecto y recuperan movimiento al salir del radio de 50 bloques o al terminar la fase activa. La mención del cooldown se registra como fin del efecto y recuperación del movimiento, conforme a la descripción del resultado; no acredita una prueba distinta del fin de toda la recarga.

Los puntos 1, 2 y 3 quedan confirmados dentro del alcance reportado. No cambia ningún comando. En este momento de la revisión, el aviso individual todavía estaba sin integrar; su incorporación posterior figura al principio de esta página. La prueba con dos portadores sigue sin realizarse por falta de medios; tampoco hay confirmación específica de conservación de NoAI:true previo. No se conoce la versión exacta ejecutada en estas pruebas.

## Antecedente: punto 2 confirmado y punto 3 incorporado

El 16 de noviembre de 2026 el usuario confirmó que probó el reloj normal y el marcado: solo activa el poder el que contiene custom_data, y solo si el jugador tiene doctor_strange. Sin el tag, el reloj marcado no activa la habilidad. Se conserva ese comportamiento en la ficha sin modificar los comandos ya probados.

El usuario pidió pasar al tercer punto. Se incorporó el circuito de limpieza de cuatro bloques preparado previamente por el generador: clear de relojes marcados en no portadores y eliminación de entidades item marcadas en zonas cargadas de Overworld, Nether y End. Todos los bloques son incondicionales y permanecen activos sin depender de portadores. Es una etapa independiente; no cambia el seguimiento de criaturas, la activación ni el contador.

### Estado y límites de las pruebas

- Reloj marcado y control de acceso por tag: confirmados por el usuario. No se infiere de ese reporte una prueba específica de todos los casos de reposición en la barra rápida.
- Limpieza de relojes: incorporada, pendiente de prueba del usuario.
- End: el usuario todavía no lo ha probado y pidió tiempo para hacerlo. Se conserva pendiente sin bloquear el avance por etapas.
- Dos portadores simultáneos: no realizado por falta de medios del usuario; se mantiene como límite de validación y no se exige como requisito para continuar con los puntos restantes.
- Conservación de una criatura creada con NoAI:true: aún sin resultado explícito.

### Prueba del punto 3

1. Con doctor_strange, comprobar que el reloj marcado permanece en el inventario.
2. Quitar el tag y comprobar que el reloj marcado desaparece, mientras un reloj normal permanece.
3. Volver a asignar el tag, recibir un reloj marcado y tirarlo al suelo: debe desaparecer incluso si su portador conserva el poder.
4. Tirar un reloj normal al suelo: debe conservarse. Mantener los circuitos cargados y activos; comprobar primero donde se esté probando y registrar las dimensiones adicionales realmente ejecutadas.

La limpieza no entra en cofres ni contenedores portátiles, no alcanza entidades descargadas y no reconoce copias antiguas sin la marca. No se presenta como protección completa frente a fabricación o almacenamiento de recursos. El aviso de recarga sigue preparado, todavía sin integrar, hasta completar esta prueba.

## Antecedente: confirmación del circuito de ocho bloques y avance al reloj marcado

El 16 de noviembre de 2026 el usuario confirmó el funcionamiento del circuito de ocho bloques en Overworld y Nether, con criaturas hostiles y no hostiles:

- Dentro del área se paralizan; al alejarse fuera de aproximadamente 50 bloques recuperan movimiento.
- Al terminar la fase activa y comenzar la recarga, las criaturas afectadas vuelven a moverse normalmente.
- No reportó fallos en esas pruebas. No indicó la versión exacta ejecutada.

El reporte no menciona una prueba en End, una criatura creada con NoAI:true, varios portadores simultáneos ni retirada del tag o cambio de dimensión en mitad del efecto. Estos casos permanecen pendientes; no se convierten en resultados confirmados por inferencia.

Se aceptó la secuencia de ocho bloques como implementación actual. La ficha se limpió de instrucciones de migración; el circuito de NoAI no cambió. Para migrar desde versiones anteriores, desactivar los circuitos viejos y conservar un único seguimiento; no borrar ds_restaurar en criaturas aún congeladas. ds_cubierto es una marca obsoleta sin efecto en la versión actual.

### Punto 2: reloj con custom_data

Se incorporaron los dos comandos preparados por el generador: activación y reposición. El objeto entregado lleva custom_data={poder:"doctor_strange"}, y ambas comprobaciones exigen esa marca. No se cambió el nombre/lore heredado ni el temporizador. El formato heredado del lore no se revisó en esta etapa.

**Estado en la preparación inicial: reloj marcado pendiente de prueba; confirmado posteriormente, según el resultado al principio de esta página.** El reloj viejo carece de marca y no debe activar tras sustituir el comando. Retirarlo manualmente de la barra rápida y dejar que el circuito entregue el nuevo; no se añadió todavía la limpieza automática de relojes.

Prueba con el tag doctor_strange y tiempo_parado en cero, sin una fase anterior en curso:

1. Tener un reloj normal en la mano: no debe iniciar el contador. La presencia de ese reloj normal en la barra no debe impedir recibir uno marcado.
2. Sostener el reloj marcado en la mano principal: debe iniciar 5200 y la fase activa según la frecuencia y orden del circuito.
3. Mantener un reloj marcado en un jugador sin doctor_strange: no debe activar el poder. La eliminación de ese objeto se incorporará y probará en el punto 3; todavía no se promete que desaparezca.

No volver a ejecutar la inicialización que pone a cero a todos los portadores durante cooldowns ajenos. Para una prueba controlada en un mundo de pruebas, se puede poner solo el contador propio a cero desde el chat si es necesario, sin reiniciar los demás.

La siguiente etapa será la limpieza dirigida de relojes marcados y, después, el aviso de recarga. No se añadieron aún para aislar las pruebas.

## Antecedente: simplificación y normalización de booleanos

El 16 de noviembre de 2026 el usuario pidió reducir los 16 bloques y aplicar la convención ya acordada de true/false para booleanos. Se consultó al chat Comandos Minecraft Java y se sustituyó la secuencia de seguimiento por ocho bloques. Reloj, temporizador, radio 50, umbral 2400.. y selección de entidades permanecen iguales.

La versión reducida ya no recalcula ni almacena ds_cubierto. Registra en ds_restaurar solo a las criaturas que encuentra dentro de un área activa sin NoAI:true. Mantiene NoAI:true en las registradas cercanas y, al procesar cada entidad registrada en su propia posición, comprueba directamente si tiene algún portador activo a 50 bloques. Si no lo tiene, restaura NoAI:false y retira su registro.

**Alcance dimensional:** @e sin cambio de contexto no recorre todas las dimensiones. execute at cambia a la dimensión y posición de la entidad elegida; por eso basta para los dos primeros comandos, que parten de portadores activos. No basta para recuperar criaturas de una dimensión sin jugadores. Los seis comandos finales visitan explícitamente Overworld, Nether y End: tres de restauración y tres de retirada del registro. No se encontró un comodín de dimensión utilizable en lugar de estos nombres.

La marca ds_restaurar de las versiones anteriores sigue siendo válida y se conserva durante la sustitución. ds_cubierto queda sin uso y no interviene en la nueva selección. Solo un circuito de seguimiento debe estar activo; no mantener en paralelo los circuitos de seis, 16 y ocho.

**Booleanos:** NoAI:true y NoAI:false se usan tanto en comprobaciones NBT como en escrituras. Son representaciones booleanas SNBT del dato almacenado como byte; no se cambiaron enteros, cantidades ni otros tipos numéricos. Los ejemplos históricos de NoAI en este laboratorio también se normalizaron para no ofrecer formatos contradictorios, sin atribuir una prueba nueva a ese cambio de escritura.

**Estado de pruebas:** la confirmación del usuario sigue correspondiendo a los seis bloques en Overworld. La versión de ocho bloques, Nether/End, NoAI previo y varios portadores requieren sus pruebas específicas. No se declara probado el circuito reducido a partir del resultado anterior.

Probar de nuevo paralización y recuperación al salir de 50 bloques en Overworld, después Nether y End. Comprobar también un cambio de dimensión con una criatura registrada que permanece cargada en la dimensión anterior. El seguimiento debe continuar sin portadores para restaurarla cuando no quede cobertura.

Referencias: [execute at e in y contexto de ejecución](https://www.minecraft.net/en-us/article/minecraft-snapshot-18w02a), [SNBT y datos de entidades en Java 1.21.5](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-5). Las referencias históricas de sintaxis no certifican una prueba actual. La revisión del generador mantiene Java 26.3 como versión estable de referencia.

## Antecedente: ampliación dimensional de 16 bloques

El 16 de noviembre de 2026 el usuario confirmó que los seis bloques funcionan en el Overworld: se paralizan criaturas hostiles y no hostiles dentro del área y recuperan el movimiento al alejarse fuera de ella. Esta confirmación no identifica la versión exacta ni acredita pruebas específicas de NoAI:true previo, dos portadores, retirada del tag o fin natural del contador.

El usuario pidió extender el mismo comportamiento a las otras dimensiones. El chat Comandos Minecraft Java revisó una secuencia de 16 bloques: 3 de limpieza de cobertura, 1 de detección en la dimensión de cada portador, 3 de registro, 3 de paralización, 3 de restauración y 3 de retirada de marcas. Se incorporó a la ficha principal sustituyendo los dos comandos originales. El resto de comandos de instalación, retirada, reloj y temporizador se comparó y conservó idéntico.

**Estado en la revisión de 16 bloques:** funcionamiento de área y recuperación por distancia confirmado en Overworld; ampliación a Nether y End pendiente de prueba. No se declara toda la secuencia de 16 bloques probada por la confirmación de la de seis.

### Prueba siguiente

1. Sustituir el circuito de seis bloques por los 16 de la ficha. No mantener los dos bloques antiguos ni otro seguimiento paralelo. No quitar ds_restaurar de criaturas que aún estén congeladas: esa marca permite recuperarlas.
2. Con el mismo circuito cargado, probar en Nether y en End que una criatura se paraliza al acercarse y recupera movimiento al quedar fuera de 50 bloques. Mantener cargada la zona de la criatura durante la observación.
3. Probar finalizar el efecto en cada dimensión y cambiar de dimensión mientras esté activo. Una criatura de la dimensión anterior debe restaurarse si ya no queda cubierta por otro portador; si se descargó su zona, comprobarla al volver a cargar sin entrar aún en una cobertura activa.
4. Registrar el resultado y la versión real. No hace falta cambiar a un filtro de hostiles: la selección general se mantiene por indicación del usuario.

Los dos portadores, la conservación del NoAI previo y la retirada del poder siguen siendo casos por comprobar de forma específica. La reactivación automática al mantener el reloj y los contadores originales no se han modificado.

La ampliación usa `execute at` para situar el área en el jugador y `execute in` explícito para seleccionar entidades en cada dimensión. Referencia estable consultada el 16 de noviembre de 2026: [Java 26.3](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs). Las notas oficiales describen el cambio dimensional de [execute](https://www.minecraft.net/en-us/article/minecraft-snapshot-18w02a); es una referencia histórica, no una versión de prueba.

## Antecedente: revisión del 16 de noviembre de 2026

El usuario pidió revisar primero la recuperación de las criaturas, conservar la selección general si se restaura correctamente y preparar por etapas el reloj marcado, su exclusividad y el aviso individual. No pidió trasladar automáticamente el filtro hostil de Kill aura. En esta primera revisión se conservaron la ficha y sus comandos mientras se probaba la restauración; la integración posterior figura al principio del laboratorio.

### Diagnóstico del circuito actual

| Condición | Lo que indica el código |
| --- | --- |
| La criatura sigue cerca al terminar | La rama de restauración intenta escribir NoAI:false |
| El jugador se aleja y deja la criatura a más de 50 bloques | La rama ya no la selecciona; puede conservar NoAI:true |
| El contador vale exactamente 2400 | Las dos ramas coinciden y dependen de su orden |
| Un portador está activo y otro en recarga cerca de la misma criatura | Las ramas pueden escribir valores opuestos |
| La criatura ya tenía NoAI:true antes del poder | La restauración general puede activar su IA sin conservar su estado original |
| Se retira el tag o el objetivo durante el efecto | El portador deja de seleccionarse; la secuencia no asegura la recuperación de sus criaturas |

Son observaciones de los selectores, no pruebas nuevas de Minecraft. NoAI afecta a la IA; no representa congelación completa de física, gravedad, proyectiles, daño o tiempo del mundo. El alcance es una esfera de 50 bloques medida desde el jugador, siguiendo su posición, no desde el bloque de comandos ni desde un punto fijado al activar.

## Punto 1: prueba de restauración con seguimiento

**Antecedente de seis bloques para Overworld:** el usuario confirmó posteriormente la paralización y la recuperación al alejarse. Esta secuencia se conserva como historial de la prueba y se sustituye por la de 16 bloques en la ficha vigente. Los demás casos específicos mantienen el estado indicado al principio del laboratorio.

Regla propuesta: una criatura permanece paralizada mientras esté cubierta por el radio de al menos un portador activo. Al salir de todos esos radios, o al finalizar el último efecto que la cubra, recupera IA. Esto cambia el comportamiento de las entidades que abandonan el área: no quedan congeladas fuera de ella.

Se mantiene el umbral activo 2400.. y el radio 50. La restauración depende de perder cobertura y deja de tener una rama de contador que se solape en 2400. Solo se registra a quien no tenía NoAI:true; las criaturas originalmente sin IA permanecen así. Una criatura congelada por este sistema no se restaura mientras otro portador activo la siga cubriendo.

### Instalación de la prueba

1. Conserva la asignación del poder, el reloj y el temporizador actuales. Mantén su circuito activo.
2. **Desactiva los dos bloques anteriores de paralización y restauración** antes de crear las criaturas de control. No deben funcionar al mismo tiempo que esta propuesta.
3. Instala la secuencia siguiente en el Overworld, con la zona cargada. Cada comando va en un bloque independiente. El primero es **repetición, siempre activo, incondicional**; los otros cinco son **cadena, siempre activo, incondicional**, orientados en orden.
4. Mantén este circuito de seguimiento activo también durante la recarga y después de retirar el tag del jugador: es quien recupera las entidades registradas.

### Bloque 1: Recalcular cobertura

<pre>execute in minecraft:overworld run tag @e[tag=ds_cubierto] remove ds_cubierto</pre>

### Bloque 2: Marcar entidades con vida dentro de la cobertura

<pre>execute at @a[tag=doctor_strange,scores={tiempo_parado=2400..}] if dimension minecraft:overworld as @e[type=!minecraft:player,distance=..50] if data entity @s Health run tag @s add ds_cubierto</pre>

### Bloque 3: Registrar únicamente entidades que no estaban ya sin IA

<pre>execute in minecraft:overworld as @e[tag=ds_cubierto,tag=!ds_restaurar] unless data entity @s {NoAI:true} run tag @s add ds_restaurar</pre>

### Bloque 4: Paralizar las registradas que siguen cubiertas

<pre>execute in minecraft:overworld as @e[tag=ds_cubierto,tag=ds_restaurar] run data merge entity @s {NoAI:true}</pre>

### Bloque 5: Restaurar las registradas fuera de toda cobertura

<pre>execute in minecraft:overworld as @e[tag=ds_restaurar,tag=!ds_cubierto] run data merge entity @s {NoAI:false}</pre>

### Bloque 6: Retirar la marca de restauración

<pre>execute in minecraft:overworld run tag @e[tag=ds_restaurar,tag=!ds_cubierto] remove ds_restaurar</pre>

### Comprobaciones por separado

Realizar en una zona de pruebas del Overworld con un portador conectado y criaturas nuevas. No reutilizar criaturas congeladas por el circuito antiguo: no tienen registro de procedencia y no se puede distinguir ese estado de un NoAI:true deliberado.

Preparación opcional **desde el chat del juego**, con las barras iniciales correspondientes:

```mcfunction
/summon minecraft:pig ~2 ~ ~ {Tags:["ds_prueba_normal"],PersistenceRequired:true}
```

```mcfunction
/summon minecraft:pig ~4 ~ ~ {Tags:["ds_prueba_sin_ia"],PersistenceRequired:true,NoAI:true}
```

El jugador debe tener instalado doctor_strange y tiempo_parado. Para reducir la espera de esta prueba se puede usar desde el chat:

```mcfunction
/scoreboard players set @s tiempo_parado 2600
```

Con el descuento normal de una unidad por tick a 20 TPS, la fase activa restante será de unos diez segundos; el resultado depende de la frecuencia real. Este valor es solo para la prueba y no modifica los valores 5200/2400 de los bloques. Apartar el reloj de la mano para no reactivar automáticamente el poder al volver a cero.

| Prueba | Resultado esperado |
| --- | --- |
| Activar cerca del cerdo normal y esperar sin alejarse | Se paraliza y luego recupera IA |
| Repetir y desplazarse a más de 50 bloques, manteniendo cargada la zona del animal | Recupera IA al quedar fuera de toda cobertura, aunque el contador siga activo |
| Mantener el cerdo que nació con NoAI:true en la misma área | Conserva NoAI:true durante y después de la prueba |
| Retirar el tag del portador durante la fase activa, sin apagar el seguimiento | Se recuperan las criaturas registradas que ya no estén cubiertas por otro portador |

Para comprobar NoAI en el cerdo normal desde el chat:

```mcfunction
/execute if data entity @e[type=minecraft:pig,tag=ds_prueba_normal,limit=1,sort=nearest] {NoAI:true}
```

La condición pasa cuando conserva NoAI:true y falla cuando no lo tiene. Cambiar ds_prueba_normal por ds_prueba_sin_ia permite comprobar el control. No tomar que el animal se quede quieto un instante como prueba suficiente: también puede estar parado por su comportamiento normal.

Prueba multijugador posterior: con dos portadores y contadores distintos, una criatura dentro de una cobertura activa debe seguir paralizada aunque el otro esté en recarga. No se acredita esa prueba hasta que el usuario la ejecute.

### Límites de esta propuesta

- Solo selecciona entidades cargadas del Overworld. No extender la confirmación de esta prueba a Nether o End. La restauración de una entidad descargada espera a que vuelva a cargarse.
- No puede reparar de forma selectiva las entidades congeladas por el circuito antiguo sin registro. No restaurar globalmente todos los NoAI:true del mundo.
- No protege contra otro sistema que cambie NoAI simultáneamente. Las etiquetas ds_cubierto y ds_restaurar quedan reservadas al poder.
- Si se apaga el circuito cuando hay entidades paralizadas, no podrán recuperarse mediante él hasta que vuelva a ejecutarse.
- La comprobación de Health evita procesar objetos y otras entidades sin ese dato; no es un filtro de hostiles ni una promesa de compatibilidad de NoAI con cada tipo de entidad con Health.

## Puntos siguientes preparados para revisión

1. Reloj con custom_data={poder:"doctor_strange"}; reposición y activación deben exigir esa marca, no solo minecraft:clock.
2. Limpieza continua de relojes marcados en jugadores sin doctor_strange y en objetos tirados cargados de las tres dimensiones. Conservar relojes vanilla normales. Cofres y objetos fabricados requieren el mismo tratamiento y límites ya descritos para los demás poderes.
3. Aviso individual arcoíris estático cuando tiempo_parado pasa de 1 a 0, mediante una marca temporal y title @s actionbar. No crear un objetivo por jugador ni alterar la duración del poder.

Las mejoras del reloj, limpieza y aviso se integrarán por separado después de comprobar la restauración. No mezclar etapas sin registrar sus resultados.

## Fuentes de la revisión

- [Java 26.3, versión estable de referencia consultada](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-3)
- [Datos de objetos y predicados custom_data](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-20-5)
- [Formato de texto para title](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-5)

Las fuentes oficiales mencionan NoAI en notas históricas, pero no proporcionan una prueba de este circuito completo. La validez funcional y multijugador de la propuesta se comprueba con los resultados del usuario, sin atribuir al asistente ejecución de Minecraft.

## Resultados y decisiones históricas

- Implementación original presentada como terminada según las pruebas históricas del autor.
- Las condiciones de paralización y restauración incluyen ambas el contador 2400. Se conserva el código; su revisión requiere una prueba específica.
- Las duraciones históricas descritas son 2 minutos y 20 segundos de actividad y 2 minutos de recarga; dependen de frecuencia y orden del circuito.

La versión exacta ejecutada, el número de jugadores y otras condiciones no indicadas por el autor permanecen sin registrar. Una comprobación documental o una prueba de otro poder no acredita estas condiciones.

<details>
<summary>Notas anteriores y fuentes</summary>

Archivo de las explicaciones anteriores, conservadas para consultar el origen de los cambios. Sus menciones de pruebas pendientes reflejan el momento en que se escribieron; los resultados actualizados figuran arriba.

Estado de desarrollo: terminado según las pruebas históricas del autor. La versión exacta de esas pruebas no está registrada en esta ficha; la compatibilidad con una versión estable posterior se revisa por separado.

- La ficha histórica describe 2 minutos y 20 segundos de actividad y 2 minutos de recarga. El contador se interpreta según la frecuencia y orden del circuito; conservar esa configuración al reproducirlo.

</details>

</details>
