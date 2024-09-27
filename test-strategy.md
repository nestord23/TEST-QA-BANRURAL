1. Test Strategy
Objetivo del Test:
El propósito del test es asegurar que el juego "Adivina tu número" se comporta según lo especificado en las restricciones del caso, manejando entradas no válidas, mostrando los mensajes correctos, y finalizando el juego en las condiciones estipuladas (adivinanza correcta o número máximo de intentos).

Alcance:
El test abarca las siguientes funcionalidades:

Validación de que el número ingresado es un entero.
Verificación de mensajes de éxito, error y fin de juego en los colores adecuados.
Control adecuado de los intentos (máximo de 10).
Comportamiento del juego cuando el número ingresado es mayor o menor al número aleatorio.
Criterios de aceptación:
Validación del input:

Si el jugador ingresa un número no entero, se debe mostrar una alerta sin contar el intento.
El juego debe continuar con el siguiente intento sin registrar un incremento.
Mensajes:

Si el jugador ingresa un número mayor al número a adivinar, el mensaje debe ser: "Incorrecto! El número es mayor!" en color negro.
Si el número es menor, el mensaje debe ser: "Incorrecto! El número es menor!" en color negro.
Si el jugador adivina el número, se debe mostrar: "Felicitaciones! adivinaste el número!" en color verde.
Si el jugador no adivina después de 10 intentos, el mensaje debe ser: "!!!Pérdistes!!!" en color rojo.
Control de intentos:

El número máximo de intentos es 10. Si se supera esta cantidad sin adivinar, el juego debe terminar.
Al adivinar antes de los 10 intentos, el juego debe finalizar y mostrar un mensaje de victoria.
Se debe habilitar un botón para reiniciar el juego una vez terminado.
Criterios de éxito del test:
El juego muestra las alertas correctas para entradas no válidas sin contar el intento.
Los mensajes de error, victoria y derrota se muestran correctamente con el color de fondo adecuado.
El número de intentos se controla y no supera el límite de 10.
El juego permite reiniciar de manera correcta tras finalizar.
Tipos de pruebas:
Pruebas de validación de entrada:

Caso 1: Ingresar un número entero (válido).
Caso 2: Ingresar un valor no entero (cadena de texto, decimal, etc.).
Caso 3: Ingresar un valor vacío o no numérico.
Pruebas de mensajes y resultados:

Caso 1: Ingresar un número mayor que el número a adivinar (debe mostrar "Incorrecto! El número es mayor!").
Caso 2: Ingresar un número menor que el número a adivinar (debe mostrar "Incorrecto! El número es menor!").
Caso 3: Adivinar el número antes del décimo intento (debe mostrar "Felicitaciones! adivinaste el número!" y finalizar).
Caso 4: No adivinar el número tras 10 intentos (debe mostrar "!!!Pérdistes!!!" y finalizar).
Pruebas de funcionalidad general:

Caso 1: Adivinar el número en menos de 10 intentos.
Caso 2: Agotar todos los intentos sin adivinar.
Caso 3: Verificar que se puede reiniciar el juego correctamente tras terminar.
2. Detalle de los Cambios Realizados
Validación del input como entero:

Problema: El código original no validaba si el número ingresado era un entero.
Solución: Se agregó una verificación usando Number.isInteger() para asegurarse de que el valor ingresado sea un entero, y una alerta para manejar los casos donde el jugador ingrese un valor inválido. Además, se previene el incremento del contador de intentos si la entrada es inválida:
javascript
Copiar código
if (isNaN(userGuess) || !Number.isInteger(userGuess)) {
  alert('Por favor, ingresa un número entero.');
  guessField.value = '';
  guessField.focus();
  return;
}
Generación correcta del número aleatorio:

Problema: El código original generaba un número aleatorio incorrecto (0 a 1).
Solución: Se corrigió la generación de números aleatorios para que sean enteros entre 1 y 100 usando Math.floor(Math.random() * 100) + 1.
Mensajes de retroalimentación y colores:

Problema: Los mensajes de error, victoria y derrota no tenían los textos ni colores adecuados.
Solución: Se implementaron los mensajes correctos y se ajustaron los colores:
Mensaje de victoria: "Felicitaciones! adivinaste el número!" en color verde.
Mensaje de derrota: "!!!Pérdistes!!!" en color rojo.
Mensajes de error cuando el número es mayor o menor: "Incorrecto! El número es mayor/menor!" en color negro.
javascript
Copiar código
lastResult.textContent = 'Felicitaciones! adivinaste el número!';
lastResult.style.backgroundColor = 'green';
...
lastResult.textContent = '!!!Pérdistes!!!';
lastResult.style.backgroundColor = 'red';
Corrección de la cantidad de intentos:

Problema: El código original permitía 5 intentos en lugar de los 10 requeridos.
Solución: Se cambió la constante ATTEMPS a ATTEMPTS = 10 para ajustar el número máximo de intentos:
javascript
Copiar código
const ATTEMPTS = 10;
Corrección de eventos y métodos:

Problema: Algunos eventos estaban mal escritos (addeventListener).
Solución: Se corrigió la sintaxis de los eventos a addEventListener:
javascript
Copiar código
guessSubmit.addEventListener('click', checkGuess);
Reinicio del juego:

Problema: El reinicio del juego no funcionaba correctamente y no se generaba un nuevo número.
Solución: Se implementó correctamente la lógica para reiniciar el juego, habilitando los campos y generando un nuevo número aleatorio:
javascript
Copiar código
function resetGame() {
  guessCount = 1;
  const resetParas = document.querySelectorAll('.resultParas p');
  for (let i = 0; i < resetParas.length; i++) {
    resetParas[i].textContent = '';
  }
  resetButton.parentNode.removeChild(resetButton);
  guessField.disabled = false;
  guessSubmit.disabled = false;
  guessField.value = '';
  guessField.focus();
  lastResult.style.backgroundColor = 'white';
  randomNumber = Math.floor(Math.random() * 100) + 1;
}