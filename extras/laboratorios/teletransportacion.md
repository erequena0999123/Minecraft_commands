# Laboratorio: Teletransportación

[Ficha y comandos](../../examples/superpowers/teletransportacion.md) · [Volver a laboratorios](../laboratorios.md)

## Resultados y decisiones

- Confirmado: en un lanzamiento lejano, la regeneración de dos segundos terminó antes de llegar la perla.
- Decisión: conservar los dos segundos de regeneración al usar la perla. El autor considera suficiente poder lanzar otra perla para activar otro periodo.
- Confirmado: limpieza de perlas marcadas en el inventario al alimentar permanentemente el bloque de repetición; también al recogerlas de cofres o del suelo.
- Pendiente: la nueva eliminación directa de perlas tiradas en las tres dimensiones. La prueba de Volar no valida este circuito de Teletransportación.
- Se investigó la detección de llegada. Se conservó la implementación por uso para evitar un seguimiento de desapariciones que no garantizaba impacto real.

La versión exacta ejecutada, el número de jugadores y otras condiciones no indicadas por el autor permanecen sin registrar. Una comprobación documental o una prueba de otro poder no acredita estas condiciones.

<details>
<summary>Notas anteriores y fuentes</summary>

Archivo de las explicaciones anteriores, conservadas para consultar el origen de los cambios. Sus menciones de pruebas pendientes reflejan el momento en que se escribieron; los resultados actualizados figuran arriba.

Estado de desarrollo: implementación recuperada y compartida por el autor el 14 de noviembre de 2026. El autor la presenta como un poder desarrollado previamente. La versión exacta y las condiciones originales de prueba no se han indicado; las observaciones de sincronización anteriores no se presentan como resultados de una prueba nueva.

Estado: limpieza de inventario de perlas confirmada por el autor al mantener la señal permanente, incluidas perlas recogidas de cofres y del suelo. Esa prueba no valida calaveras, bolas de nieve ni la nueva eliminación directa de entidades, que siguen pendientes de prueba.

Referencia documental: Java 26.3, estable consultada el 16 de noviembre de 2026 en el [índice oficial](https://feedback.minecraft.net/hc/en-us/sections/360001186971-Release-Changelogs). [Sintaxis oficial de custom_data, predicados y slot contents](https://www.minecraft.net/en-us/article/minecraft-java-edition-1-20-5).

Tras esa prueba, el autor decidió conservar la regeneración de dos segundos por uso: puede volver a lanzar una perla para activar otro periodo de regeneración. No se añadió detección de impacto ni se aumentó la duración.

La intención del autor es compensar el daño de la teletransportación. El criterio registra el uso de la perla, no su llegada ni la pérdida de vida. Por ello, la regeneración puede comenzar durante el viaje y agotarse antes de una llegada tardía. El autor confirmó que en un lanzamiento lejano la regeneración se agotó antes de llegar. La secuencia no garantiza inmunidad ni una curación posterior a cada llegada.

Las cadenas deben ser incondicionales: que no haya objetos en un inventario o dimensión no debe impedir la limpieza siguiente. Como alternativa, el bloque de repetición puede usar **necesita redstone** si recibe una señal permanente, sin depender de un pulso breve. No sirve un pulso breve. Mantener cargada la zona de los bloques.

El primer comando limpia inventarios de jugadores conectados sin `teletransportar`, incluso después de retirar el poder al último portador. Los siguientes eliminan todos los ítems marcados tirados en las tres dimensiones vanilla, aunque su dueño conserve el poder. No seleccionan proyectiles lanzados. Solo alcanzan entidades cargadas; las descargadas se revisarán al cargar su zona mientras el circuito siga activo.

Los objetos normales y las copias antiguas sin marca se conservan. No se inspeccionan cofres ni el contenido de contenedores portátiles; una copia marcada tomada de un cofre o del suelo se limpia cuando entra en el inventario de un jugador sin el tag. Los productos fabricados a partir de esos recursos quedan fuera. La marca identifica el poder, no un dueño individual.

</details>
