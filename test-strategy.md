# Estrategia de Pruebas para el Juego "Adivina tu Número"

## Objetivo
El objetivo de este documento es detallar la estrategia de pruebas implementada para el juego "Adivina tu Número", así como los cambios realizados en el código para cumplir con los requisitos especificados.

## Estrategia de Pruebas

### Casos de Prueba

1. **Validación de entrada no numérica**
   - **Descripción**: Ingresar un valor no numérico y verificar que se muestre una alerta.
   - **Resultado esperado**: Se debe mostrar un mensaje de alerta que indique que se debe ingresar un número entero y no se debe incrementar el contador de intentos.

2. **Número mayor que el número aleatorio**
   - **Descripción**: Ingresar un número mayor que el número aleatorio.
   - **Resultado esperado**: Se debe mostrar el mensaje "Incorrecto! El número es menor!" y el color de fondo debe ser negro.

3. **Número menor que el número aleatorio**
   - **Descripción**: Ingresar un número menor que el número aleatorio.
   - **Resultado esperado**: Se debe mostrar el mensaje "Incorrecto! El número es mayor!" y el color de fondo debe ser negro.

4. **Adivinanza correcta**
   - **Descripción**: Ingresar el número aleatorio.
   - **Resultado esperado**: Se debe mostrar el mensaje "Felicitaciones! adivinaste el número!" y el color de fondo debe ser verde.

5. **Número de intentos excedido**
   - **Descripción**: Realizar 10 intentos sin adivinar el número.
   - **Resultado esperado**: Se debe mostrar el mensaje "!!!Pérdistes!!!" y el color de fondo debe ser rojo.

6. **Reinicio del juego**
   - **Descripción**: Hacer clic en el botón para reiniciar el juego después de finalizar.
   - **Resultado esperado**: El juego debe reiniciarse y permitir una nueva serie de intentos.

## Cambios Realizados en el Código

1. **Validación de Entrada**
   - Se agregó una validación para comprobar si el valor ingresado por el usuario es un número entero.
   - Se utilizó `isNaN()` y `Number.isInteger()` para verificar la validez de la entrada.
   - **Código**:
     ```javascript
     if (isNaN(userGuess) || !Number.isInteger(userGuess)) {
       alert('Por favor, ingresa un número entero.');
       guessField.value = '';
       guessField.focus();
       return;
     }
     ```

2. **Manejo de Mensajes de Retroalimentación**
   - Se ajustaron los mensajes de retroalimentación para mostrar el texto correcto basado en la entrada del usuario.
   - Se estableció el color de fondo correspondiente para los mensajes de error (negro), victoria (verde) y pérdida (rojo).
   - **Código**:
     ```javascript
     lastResult.textContent = 'Incorrecto!';
     lastResult.style.backgroundColor = 'black'; // Para respuestas incorrectas
     ```

3. **Corrección del Número Aleatorio**
   - Se corrigió la lógica para generar un número aleatorio entre 1 y 100 utilizando `Math.floor(Math.random() * 100) + 1`.
   - **Código**:
     ```javascript
     let randomNumber = Math.floor(Math.random() * 100) + 1; // Número aleatorio entre 1 y 100
     ```

4. **Control de Intentos**
   - Se implementó un contador de intentos que detiene el juego después de 10 intentos o al acertar el número.
   - Se modificaron los mensajes de finalización del juego según el estado del juego (ganar o perder).
   - **Código**:
     ```javascript
     if (guessCount === ATTEMPTS) {
       lastResult.textContent = '!!!Pérdistes!!!';
       lastResult.style.backgroundColor = 'red';
       setGameOver();
     }
     ```

5. **Reinicio del Juego**
   - Se implementó la lógica para reiniciar el juego, eliminando los mensajes previos y reactivando los campos de entrada.
   - Se creó un botón para reiniciar el juego y se le asignó una función que restablece todos los parámetros.
   - **Código**:
     ```javascript
     resetButton.addEventListener('click', resetGame);
     ```

## Conclusión
Los cambios realizados aseguran que el juego "Adivina tu Número" cumpla con todos los requisitos funcionales y no funcionales. Se han implementado las validaciones necesarias y se ha mejorado la experiencia del usuario mediante mensajes claros y un control efectivo del flujo del juego.