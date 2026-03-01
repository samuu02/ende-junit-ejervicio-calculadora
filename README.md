# Testing con Junit

Este es un ejemplo sencillo de pruebas unitarias usando Junit 5

Observa que este proyecto no tiene ninguna clase con el método `main`, no nos hace fatal. Además, tampoco tiene ningún `scanner` ni ningún `print`.

Haz un fork de este proyecto en tu repositorio de Github y contesta a las siguientes preguntas:

## 1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?


Llevar a cabo pruebas unitarias sobre una parte concreta del sistema, en este caso, el funcionamiento de una calculadora. La finalidad de esto es asegurarse de que la unidad lógica más básica (los propios métodos de cálculo) opere correctamente por sí sola, sin depender de otros componentes.

Dentro de la empresa, este módulo podría incorporarse como una librería dentro de un sistema de información más amplio, por ejemplo, en una aplicación móvil de calculadora.


## 2. Revisa las pruebas de la suma y comenta lo que te parezca de interés

El método sumarPositivosMal() está diseñado intencionadamente para que dé error, ya que se configura para esperar un resultado de 4 en vez de 5. De este modo, se puede comprobar que el sistema de pruebas es capaz de identificar fallos correctamente.


## 3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.

Hay dos entradas (dividendo y divisor) y una salida (el resultado de la división).
   
Clases equivalentes:
    Dividendo: son válidos todos los números.
    Divisor: son válidos todos los números menos el cero.
   
Valores límites: (depende de cada entrada):
    Dividendo (D1): 
      - Valor mínimo: -infinito
      - Valor máximo: +infinito
      - Válidas: D1 < 0 | D1 > 0 | D1 = 0
   
    Divisor (D2):
      - Valor mínimo: -infinito
      - El cero no es válido.
      - Valor máximo: +infinito
      - Válidas: D2 < 0 | D2 > 0
      - No Válidas: D2 = 0 
   
Conjetura de errores: se comprobará que cuando el divisor sea cero dará error.

Casos de pruebas: (aplicando los limites para cubrir todos los casos)
    | Caso de Prueba | Dividendo | Divisor | Salida |
    | CP1 | 2 | 2 | 1 |  
    | CP2 | -4 | -2 | 2 | 
    | CP3 | 5 | -5 | -1 |
    | CP4 | -10 | 5 | -2 |
    | CP5 | 0 | 3 | 0 |
    | CP6 | 0 | -1 | 0 |
    | CP7 | 7 | 0 | ERROR |
    | CP8 | -3 | 0 | ERROR |
    | CP9 | 0 | 0 | ERROR |

@Test
public void dividirTest() {

    // Pruebas de caja negra aplicando clases equivalentes y valores límite

    assertAll("Division",

        // Casos válidos
        () -> assertEquals(1, calculadora.dividir(2, 2), "2 / 2 = 1"),          
        () -> assertEquals(2, calculadora.dividir(-4, -2), "-4 / -2 = 2"),      
        () -> assertEquals(-1, calculadora.dividir(5, -5), "5 / -5 = -1"),      
        () -> assertEquals(-2, calculadora.dividir(-10, 5), "-10 / 5 = -2"),    
        () -> assertEquals(0, calculadora.dividir(0, 3), "0 / 3 = 0"),         
        () -> assertEquals(0, calculadora.dividir(0, -1), "0 / -1 = 0"),        

        // Casos no válidos (divisor = 0)
        () -> assertThrows(OperacionNoValidaException.class,
                () -> calculadora.dividir(7, 0), "7 / 0 = ERROR"),
        () -> assertThrows(OperacionNoValidaException.class,
                () -> calculadora.dividir(-3, 0), "-3 / 0 = ERROR"),
        () -> assertThrows(OperacionNoValidaException.class,
                () -> calculadora.dividir(0, 0), "0 / 0 = ERROR")
    );
}