# Juego de Memoria

Juego de memoria hecho con JavaScript vanilla para la evaluacion de DOM y eventos.

Repositorio: https://github.com/lorarsam/Juego-de-memoria

GitHub Pages: https://lorarsam.github.io/Juego-de-memoria/

## Defensa del proyecto

La IA ayudo a ordenar la logica del juego, detectar errores tipicos del codigo original y mejorar la estructura general. El archivo `parte2_codigo_para_auditar.html` muestra una version inicial con problemas: usaba varias variables sueltas, agregaba un listener por cada carta, comparaba leyendo el DOM y permitia errores con clicks rapidos o doble click sobre la misma carta.

En la version final (`index.html` + `app.js`) decidi usar un objeto `state` como fuente unica de verdad. Ahi viven las cartas, cartas volteadas, movimientos, nombre, nivel y bloqueo del tablero. Esto evita depender del texto visible en el DOM para decidir si dos cartas coinciden. La interfaz se actualiza desde `render()`, por lo que el DOM solo muestra el estado actual.

Otra decision fue usar delegacion de eventos en `#tablero`. En el codigo original se creaba un `addEventListener` por cada carta cada vez que se renderizaba. En la version final hay un solo listener que detecta que carta fue presionada con `closest('.card')`. Esto reduce repeticion, mejora el rendimiento y cumple la restriccion de no usar un listener por elemento.

Tambien se corrigio el bloqueo del turno. El codigo original permitia hacer click en una tercera carta durante el `setTimeout` o hacer doble click sobre la misma carta. En `app.js`, `state.bloqueado` impide jugar mientras se resuelve una pareja incorrecta, y `state.volteadas.includes(indice)` evita comparar una carta consigo misma.

Para seguridad, la version original mostraba el mensaje de victoria con `innerHTML`, mezclando texto del usuario con HTML. En la version final se usa `textContent`, por lo que el nombre del jugador se muestra como texto normal y no como codigo interpretable.

Con mas tiempo mejoraria la accesibilidad del tablero con navegacion completa por teclado entre cartas, no solo Enter para iniciar y R para reiniciar.
