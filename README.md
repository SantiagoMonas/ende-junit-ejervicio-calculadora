# Testing con Junit

Este es un ejemplo sencillo de pruebas unitarias usando Junit 5

Observa que este proyecto no tiene ninguna clase con el método `main`, no nos hace fatal. Además, tampoco tiene ningún `scanner` ni ningún `print`.

Haz un fork de este proyecto en tu repositorio de Github y contesta a las siguientes preguntas:

1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?
2. Revisa las pruebas de la suma y comenta lo que te parezca de interés
3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.



## Instrucciones

El alumno deberá hacer un fork de este proyecto e implementar la solución solicitada (preguntas y código).

>Se deberá utilizar este fichero, y los artefactos de código del proyecto, para resolver el ejercicio.

## Santiago Monasterio 1DAW

### 1. ¿Qué sentido puede tener este proyecto y para que lo podrías usar?

- El proyecto es un entorno diseñado para aprender y practicar pruebas unitarias usando la libreria JUnit. Lo podemos ver ya que si miramos el codigo no tenemos un main, Scanner ni un print, no es interactivo. Pues creo que se podria usar para la logica matematica de alguna aplicacion.

### 2. Revisa las pruebas de la suma y comenta lo que te parezca de interés

- Despues de hacer el test podemos ver que los metodos dividir, sumar y sumar positivos no dan error, pero sumarpositivosmal nos da un error poniendo "Expected [4] but was [5]. Segun he leido esto es el corazon de JUnit, avisarme cuando el codigo no hace lo que esperaba.
  
### 3. Realiza un estudio de caja negra de la división e implementa las pruebas en junit: Se realizará en markdown.

Para probar el método de la división primero hacemos el estudio de cada entrada individualmente.
Para la variable a sus limites son (-∞, ∞).

| Variable | Valores | Tipo de Caso | Valor de Prueba Seleccionado |
| :------- | :------ | :----------- | :--------------------------- |
| **a**    | (-∞, ∞) | Válido       | 7                            |
| **b**    | (-∞, 0) | Válido       | -7                           |
| **b**    | (0, ∞)  | Válido       | 10                           |
| **b**    | 0       | No válido    | 0 (Provoca error)            |


| Caso de Prueba | Entrada (a, b) | Resultado Esperado | Descripción |
| :------------- | :------------- | :----------------- | :---------- |
| **1**          | a = 7, b = -7  | -1                 |
| **2**          | a = 7, b = 10  | 0                  |
| **3**          | a = 7, b = 0   | Error              |

### Codigo en JUnit
- Esto es el codigo que se deberia poner en la parte de calculadoratest.java

```java
    @Test
    public void testDivisionNumeroNegativo() {
        // Caso de Prueba 1: a = 7, b = -7 | Esperado: -1
        int resultado = calc.dividir(7, -7);
        assertEquals(-1, resultado, "La división de 7 entre -7 debería ser -1");
    }

    @Test
    public void testDivisionDivisorMayor() {
        // Caso de Prueba 2: a = 7, b = 10 | Esperado: 0
        int resultado = calc.dividir(7, 10);
        assertEquals(0, resultado, "La división entera de 7 entre 10 debería ser 0");
    }

    @Test
    public void testDivisionPorCero() {
        // Caso de Prueba 3: a = 7, b = 0 | Esperado: Error (Exception)
        assertThrows(ArithmeticException.class, () -> {
            calc.dividir(7, 0);
        }, "Intentar dividir entre 0 debería lanzar ArithmeticException");
    }
    ```