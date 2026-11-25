# Laboratorio: Kill aura

[Ficha y comandos](../../examples/superpowers/kill-aura.md) · [Volver a laboratorios](../laboratorios.md)

## Resultados y decisiones

### Ampliación a 35 tipos hostiles y resultado del filtro

**Resultado confirmado por el autor.** El aura atacó a esqueletos, zombis, creepers y al Warden. Los cerdos y aldeanos quedaron ilesos. El autor da por cerrado el filtro con esta muestra. Las demás especies de la lista comparten el mismo criterio de selección por identificador y carecen de una prueba individual registrada.

El 16 de noviembre de 2026 el autor confirmó que el circuito funciona con radio 5 y que lo probó con criaturas pacíficas sin afectarlas. Mencionó corregir 15 a 5 en su montaje; la ficha local ya indicaba 5 y se conserva ese valor. La versión exacta y el número de jugadores de la prueba no se especificaron.

Después pidió incluir todos los tipos hostiles, superando la lista inicial limitada. Se consultó al chat Comandos Minecraft Java y se amplió únicamente el array del comando 2 a 35 tipos. No cambian los otros comandos, el radio, el daño, el temporizador, los cuatro bloques ni el aviso estático.

Lista vigente: `blaze`, `bogged`, `breeze`, `creaking`, `creeper`, `drowned`, `elder_guardian`, `ender_dragon`, `endermite`, `evoker`, `ghast`, `guardian`, `hoglin`, `husk`, `illusioner`, `magma_cube`, `parched`, `phantom`, `piglin_brute`, `pillager`, `ravager`, `shulker`, `silverfish`, `skeleton`, `slime`, `stray`, `vex`, `vindicator`, `warden`, `witch`, `wither`, `wither_skeleton`, `zoglin`, `zombie`, `zombie_villager`.

La revisión documental no encontró otro tipo hostil que añadir conforme al criterio de excluir tipos neutrales y monturas situacionales. No se afirma haber auditado directamente el registro binario completo de Minecraft.

#### Clasificación y casos especiales

- Se incluyen Parched de Java 1.21.11 y Hoglin, reclasificado como hostil en 26.2, además de los bosses vanilla y el ilusionista invocable mediante comandos.
- Arañas, arañas de cueva, endermen, piglins y piglins zombificados quedan fuera por ser tipos neutrales/situacionales. No es un filtro de agresividad actual.
- Zombie Horse es no hostil. Zombie Nautilus y Camel Husk dependen de sus jinetes; no se incluyen sus tipos completos para no atacar monturas pasivas o domesticadas. Sulfur Cube es pasivo y no se añade.
- Slime queda incluido por tipo, aunque sus variantes pequeñas sean inofensivas. Giant no se incluye como enemigo funcional por su falta de IA de ataque. El conejo asesino es una variante de rabbit: no se añade rabbit completo porque dañaría conejos normales. Esta lista de tipos no añade una detección específica de esa variante excepcional.
- Creaking vinculado a un corazón reacciona de forma especial al daño. Wither y dragón tienen reglas propias. Pertenecer a la lista no garantiza recibir indirect_magic; un objetivo inmune puede ocupar la selección de cercanía. No se cambió el daño para sortear esas reglas.

#### Fuentes de actualización

- [Java 1.21.11: Parched y comportamiento de las monturas](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-11)
- [Java 26.1: novedades](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-1)
- [Java 26.2: Hoglin y Sulfur Cube](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-2)
- [Java 26.3: versión estable de referencia](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-3)
- [Java 1.21.4: daño del Creaking vinculado y del generado con huevo](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-4)

Las entradas de selección anteriores se conservan como historial. La lista vigente es la de 35 tipos.


### Selección de objetivos: 16 de noviembre de 2026

El usuario delegó elegir entre excluir entidades o permitir tipos y solicitó los comandos del chat Comandos Minecraft Java. Se incorporó la lista conservadora de ese generador: `zombie`, `husk`, `drowned`, `skeleton`, `stray`, `bogged`, `creeper`, `witch`, `pillager`, `vindicator`, `evoker`, `ravager`, `blaze`, `wither_skeleton`. No es la lista completa de mobs hostiles. No contiene ghast, guardianes, breeze, vex, slimes, magma cubes, endermites, silverfish, shulkers, phantom, piglin brute, hoglin, zoglin ni bosses vanilla como Wither o dragón; su ausencia no implica clasificarlos como pacíficos. Se pueden añadir tras acordarlo, editando únicamente la lista del predicado.

Se excluyen por defecto todos los tipos no enumerados, incluidas entidades decorativas y criaturas neutrales incluso enfadadas. Arañas y endermen quedan fuera para evitar daño a criaturas que puedan estar tranquilas. No es una detección de quién está atacando en ese instante. Los cuatro bosses del manual usan zombie, husk, stray y evoker y, por tanto, siguen siendo seleccionables por su tipo; no hay una inmunidad de bosses.

La cadena limpia marcas, marca candidatos, aplica una sola búsqueda de cercanía por portador y limpia marcas al final. No se usa un comando de daño por especie. La unión de candidatos sirve para todos los portadores porque comparten la misma lista; cada búsqueda conserva su propio radio y dimensión. Las cadenas son incondicionales para continuar incluso si un paso no encuentra candidatos. Solo un circuito completo y reservado utiliza aura_objetivo.

Se conservaron intactos todos los demás comandos: aviso estático, temporizador, umbral 1200, daño 2, radio 5, entrega y limpieza de calaveras. El autor confirmó la presentación estática y descartó la animación. No se ejecutó Minecraft desde este chat.

#### Referencia de versión y sintaxis

Java 26.3, estable verificada por el chat de comandos el 16 de noviembre de 2026. La fuente oficial de [1.20.5](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-20-5) documenta predicados inline sin archivo y listas de tipos. [Java 26.2](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-2) cambia el campo de tipo de entidad a minecraft:entity_type. [Java 26.3](https://www.minecraft.net/en-us/article/minecraft-java-edition-26-3) cambia condition a type para los predicados. La secuencia usa los nombres actuales, no la combinación antigua condition/predicate.type. La verificación documental no sustituye la prueba del circuito.

#### Plan de pruebas del filtro inicial (histórico)

- Colocar un objeto tirado y un animal más cerca que un zombi: comprobar que el daño sigue seleccionando al zombi.
- Comprobar un marco, un aldeano, un caballo y un jugador sin criaturas permitidas cerca: ninguno debe ser elegido.
- Colocar dos especies permitidas a distinta distancia: solo debe seleccionarse la más cercana en cada ejecución por portador.
- Repetir con dos portadores, después en otra dimensión, y comprobar que aura_objetivo no queda asignada tras el ciclo.
- Comprobar que el aviso y el cooldown conservan su comportamiento.

Registrar versión exacta, configuración y resultados del usuario. Si el comando no acepta la sintaxis o selecciona mal, conservar el mensaje exacto para corregir una variable por vez.


- Presentación del aviso cambiada de verde a un arcoíris estático por letra mediante una lista de componentes de texto con colores hexadecimales. Mantiene el texto, destinatario, detección y frecuencia del aviso confirmado. El autor probó la presentación multicolor y confirmó que le gusta; el 16 de noviembre de 2026 decidió conservarla estática y descartar la animación.
- Para migrar desde el temporizador anterior, sustituir su circuito de activación y descuento por la secuencia actual; no mantener un segundo bloque descontando el mismo contador.

- Aviso individual añadido mediante actionbar al pasar de 1 a 0: marca temporal `aura_aviso_listo`, descuento, mensaje a `@s` y retirada de marca en una cadena ordenada. No añade objetivos ni cambia los umbrales del poder. El autor confirmó que el aviso aparece correctamente al llegar a cero y no observó fallos. No indicó una prueba concreta de cada condición multijugador; esos casos conservan su alcance documental.
- Revisión del código: `tiempo_aura` guarda puntuaciones por jugador. La inicialización actual reinicia a todos los portadores conectados y la retirada elimina el objetivo compartido; no son operaciones de asignación o baja aisladas. Los contadores se pausan al desconectar.
- Referencia documental: Java 26.3, estable consultada el 16 de noviembre de 2026. [Formato oficial de texto para title](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-21-5).

- Activación y reposición ajustadas para exigir `minecraft:skeleton_skull[minecraft:custom_data~{poder:"kill_aura"}]`. La marca ya se asignaba al entregar; antes la activación solo comprobaba el tipo de ítem. El autor confirmó que funciona la identificación de la calavera mediante custom_data. No indicó una prueba multijugador específica. La duración y el daño conservan su funcionamiento. Verificación documental para Java 26.3 el 16 de noviembre de 2026; sintaxis de predicados en la fuente oficial de componentes enlazada abajo.

- Implementación original presentada como terminada según las pruebas históricas del autor.
- El objeto del código es `minecraft:skeleton_skull`; el recuerdo verbal de una calavera de Wither Skeleton no autoriza a cambiarlo.
- **Limpieza confirmada en Minecraft.** El autor ratificó la prueba del circuito. Al retirar el poder, la calavera marcada desaparece del inventario y las calaveras ajenas al poder se conservan.
- Filtro inicial de 14 tipos: el autor confirmó posteriormente que funciona a 5 bloques y no afecta a las criaturas pacíficas de su prueba. Lista ampliada después a 35; el resultado por especie figura al principio del laboratorio.
- **Presentación aprobada en Minecraft.** El autor verificó el nombre legible con los adornos ofuscados, las instrucciones de uso y la historia propia de la calavera. [Ficha de Kill Aura](../../examples/superpowers/kill-aura.md)

La versión exacta ejecutada, el número de jugadores y otras condiciones no indicadas por el autor permanecen sin registrar. Una comprobación documental o una prueba de otro poder no acredita estas condiciones.

<details>
<summary>Notas anteriores y fuentes</summary>

Archivo de las explicaciones anteriores, conservadas para consultar el origen de los cambios. Sus menciones de pruebas pendientes reflejan el momento en que se escribieron; los resultados actualizados figuran arriba.

Estado de desarrollo: terminado según las pruebas históricas del autor. La versión exacta de esas pruebas no está registrada en esta ficha; la compatibilidad con una versión estable posterior se revisa por separado.

En esa etapa se había comprobado la limpieza de perlas al mantener la señal permanente. El resultado vigente de la calavera figura en «Resultados y decisiones».

Referencia documental: Java 26.3, estable consultada el 16 de noviembre de 2026 en el [índice oficial](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs). [Sintaxis oficial de custom_data, predicados y slot contents](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-20-5).

En un montaje anterior, el comando de entrega de Kill Aura todavía incluía una descripción tomada del reloj de Doctor Strange. La ficha vigente contiene el nombre y el lore aprobados para la calavera.

- La ficha histórica describe 3 minutos y 20 segundos de actividad y 1 minuto de recarga. La duración real depende de la frecuencia y orden de los bloques.

Las cadenas deben ser incondicionales: que no haya objetos en un inventario o dimensión no debe impedir la limpieza siguiente. Como alternativa, el bloque de repetición puede usar **necesita redstone** si recibe una señal permanente, sin depender de un pulso breve. No sirve un pulso breve. Mantener cargada la zona de los bloques.

El primer comando limpia inventarios de jugadores conectados sin `aura_dmg`, incluso después de retirar el poder al último portador. Los siguientes eliminan todos los ítems marcados tirados en las tres dimensiones vanilla, aunque su dueño conserve el poder. No seleccionan proyectiles lanzados. Solo alcanzan entidades cargadas; las descargadas se revisarán al cargar su zona mientras el circuito siga activo.

Los objetos normales y las copias antiguas sin marca se conservan. No se inspeccionan cofres ni el contenido de contenedores portátiles; una copia marcada tomada de un cofre o del suelo se limpia cuando entra en el inventario de un jugador sin el tag. Los productos fabricados a partir de esos recursos quedan fuera. La marca identifica el poder, no un dueño individual.

</details>
