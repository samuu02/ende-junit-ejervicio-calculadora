# Testing con Junit

Este es un ejemplo sencillo de pruebas unitarias usando Junit 5

Observa que este proyecto no tiene ninguna clase con el método `main`, no nos hace fatal. Además, tampoco tiene ningún `scanner` ni ningún `print`.

Haz un fork de este proyecto en tu repositorio de Github y contesta a las siguientes preguntas:

1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?
Es una calculadora básica y puede servir como base para una calculadora más completa, como una calculadora científica.
2. Revisa las pruebas de la suma y comenta lo que te parezca de interés
Están los métodos bien excepto el método sumarPositivosMal.
3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.

He hecho cuatro casos: con dos números positivos (4/2) para que de otro número positivo, involucrando un número negativo (3/-1) para obtener un resultado negativo, con un cero como numerador para obtener un cero como resultado (0/2) y con dos números negativos para obtener un resultado positivo.

@Test
   void dividir() {
      Assertions.assertAll("División", new Executable[]{() -> {
         Assertions.assertEquals(2, Calculadora.dividir(4, 2), "4 / 2 = 2");
      }, () -> {
         Assertions.assertEquals(-3, Calculadora.dividir(3, -1), "3 / 1 = -3");
      }, () -> {
         Assertions.assertEquals(0, Calculadora.dividir(0, 1), "0 / 1 = 0");
      }, () -> {
         Assertions.assertEquals(1, Calculadora.dividir(-1, -1), "-1 / -1 = 1");
      }});
   }



## Instrucciones

El alumno deberá hacer un fork de este proyecto, poner el repositorio como **privado**, agregar al profesor como colaborador (julparper) e implementar la solución solicitada (preguntas y código).

>Se deberá utilizar este fichero, y los artefactos de código del proyecto, para resolver el ejercicio.


**Si no se puede acceder al repositorio la evaluación del ejercicio será de 0. No se evaluarán entregas modificadas/entregadas fuera del plazo establecido en la tarea**