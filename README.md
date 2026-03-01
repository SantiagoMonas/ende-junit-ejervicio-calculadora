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

Para probar el método de la división, hemos analizado las clases de equivalencia (combinaciones de números positivos, negativos y el cero) y los valores límite (como la división por cero).

| Caso de Prueba | Entrada (a, b)  | Resultado Esperado         | Descripción                         |
| :------------- | :-------------- | :------------------------- | :---------------------------------- |
| **1**          | a = 10, b = 2   | 5                          | Positivo entre positivo             |
| **2**          | a = -10, b = -2 | 5                          | Negativo entre negativo             |
| **3**          | a = 10, b = -2  | -5                         | Positivo entre negativo             |
| **4**          | a = -10, b = 2  | -5                         | Negativo entre positivo             |
| **5**          | a = 0, b = 5    | 0                          | Cero entre cualquier número da cero |
| **6**          | a = 10, b = 0   | OperacionNoValidaException | División por cero (Valor Límite)    |
| **7**          | a = 1, b = 2    | 0                          | División con truncamiento decimal   |


### Codigo
- Esto es el codigo que se deberia poner en la parte de calculadoratest.java

// Pruebas.
    @Test
    @DisplayName("Probar divisiones válidas")
    void dividir() {
        assertAll("División",
                () -> assertEquals(5, Calculadora.dividir(10, 2), "10 / 2 = 5"),
                () -> assertEquals(5, Calculadora.dividir(-10, -2), "-10 / -2 = 5"),
                () -> assertEquals(-5, Calculadora.dividir(10, -2), "10 / -2 = -5"),
                () -> assertEquals(-5, Calculadora.dividir(-10, 2), "-10 / 2 = -5"),
                () -> assertEquals(0, Calculadora.dividir(0, 5), "0 / 5 = 0"),
                () -> assertEquals(0, Calculadora.dividir(1, 2), "1 / 2 = 0 (truncamiento)"));
    }

    @Test
    @DisplayName("Probar división por cero (Excepción)")
    void dividirPorCero() {
        assertThrows(OperacionNoValidaException.class, () -> {
            Calculadora.dividir(10, 0);
        },);
    }