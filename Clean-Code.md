## ¿Qué es Clean Code?

> **"Code is clean if it can be understood easily – by everyone on the team."**

El código es limpio cuando cualquier persona del equipo puede **entenderlo con facilidad**, **sin necesidad de que el autor original lo explique**. Esto implica que el código:

* Es **legible**.
* Se puede **modificar** sin temor a romper otras partes.
* Es **extensible**, es decir, se le pueden agregar nuevas funcionalidades fácilmente.
* Es **mantenible** a lo largo del tiempo.

---

## 1. Reglas Generales

| Regla                               | Significado                                                     |
| ----------------------------------- | --------------------------------------------------------------- |
| **1. Seguir convenciones estándar** | Utilizar normas de estilo del lenguaje o del equipo.            |
| **2. Mantenerlo simple (KISS)**     | Preferir soluciones simples. Evitar complejidades innecesarias. |
| **3. Regla del Boy Scout**          | Siempre dejar el código un poco mejor que como lo encontraste.  |
| **4. Encontrar la causa raíz**      | No tapar errores. Investigar y resolver el problema de fondo.   |

---

## 2. Reglas de Diseño

| Regla                                                | Significado                                                        |
| ---------------------------------------------------- | ------------------------------------------------------------------ |
| **1. Mantener datos configurables en niveles altos** | Las configuraciones deben estar visibles y accesibles.             |
| **2. Preferir polimorfismo a condicionales**         | Evitar `if/else` o `switch` extensos usando herencia o interfaces. |
| **3. Separar el código multi-hilo**                  | Mantenerlo aislado para evitar errores de concurrencia.            |
| **4. Evitar sobreconfiguración**                     | No dar demasiadas opciones innecesarias.                           |
| **5. Usar inyección de dependencias**                | Las clases no deben crear sus dependencias, sino recibirlas.       |
| **6. Seguir la Ley de Deméter**                      | Una clase solo debe conocer sus dependencias directas.             |

---

## 3. Consejos de Comprensibilidad

| Consejo                                                | Significado                                                               |
| ------------------------------------------------------ | ------------------------------------------------------------------------- |
| **1. Ser consistente**                                 | Aplicar el mismo estilo y estructura en todo el código.                   |
| **2. Usar variables explicativas**                     | Nombrar variables que expliquen su propósito.                             |
| **3. Encapsular condiciones límite**                   | Agrupar y aislar lógicas como validaciones de límites o valores extremos. |
| **4. Usar objetos valor en lugar de tipos primitivos** | Ejemplo: en vez de `String fecha`, usar `Fecha fecha`.                    |
| **5. Evitar dependencias lógicas internas**            | No hacer que un método dependa del orden de ejecución de otros.           |
| **6. Evitar condicionales negativas**                  | Mejor `if (esActivo)` que `if (!esInactivo)`                              |

---

## 4. Reglas de Nombres

| Regla                                     | Significado                                                                     |
| ----------------------------------------- | ------------------------------------------------------------------------------- |
| **1. Nombres descriptivos y no ambiguos** | El nombre debe decir exactamente qué hace o representa.                         |
| **2. Distinciones significativas**        | Evitar nombres como `user1`, `user2`. Mejor `adminUser`, `guestUser`.           |
| **3. Nombres pronunciables**              | Facilita el trabajo en equipo y la lectura.                                     |
| **4. Nombres buscables**                  | Que se puedan encontrar fácilmente en el código.                                |
| **5. Reemplazar números mágicos**         | Usar constantes con nombres (`MAX_REINTENTOS = 3`) en lugar de números sueltos. |
| **6. Evitar codificaciones**              | No incluir tipo o prefijos (`strNombre`, `intEdad`).                            |

---

## 5. Reglas para Funciones

| Regla                                | Significado                                                                                              |
| ------------------------------------ | -------------------------------------------------------------------------------------------------------- |
| **1. Pequeñas**                      | Deben ser concisas y directas.                                                                           |
| **2. Hacer solo una cosa**           | Una función debe tener una única responsabilidad.                                                        |
| **3. Nombres descriptivos**          | El nombre debe decir claramente qué hace.                                                                |
| **4. Menos argumentos**              | Idealmente 0-2 parámetros.                                                                               |
| **5. Sin efectos secundarios**       | No deben modificar estados externos inesperadamente.                                                     |
| **6. No usar argumentos de bandera** | Mejor dividir en múltiples funciones. Ej.: `enviar(true)` => `enviarComoCorreo()`, `enviarComoMensaje()` |

---

## 6. Reglas para Comentarios

| Regla                               | Significado                                                  |
| ----------------------------------- | ------------------------------------------------------------ |
| **1. Explicarse con el código**     | Hacer que el código sea autoexplicativo.                     |
| **2. Evitar redundancia**           | No explicar lo obvio.                                        |
| **3. No añadir ruido innecesario**  | Comentarios innecesarios sólo estorban.                      |
| **4. No comentar llaves de cierre** | `// fin if` es innecesario con buena indentación.            |
| **5. No comentar código muerto**    | Si no sirve, elimínalo.                                      |
| **6. Explicar intención**           | Usar comentarios para explicar decisiones de diseño.         |
| **7. Aclarar el código complejo**   | Solo cuando el código no puede ser más claro por sí solo.    |
| **8. Advertir sobre consecuencias** | Por ejemplo, “Este método es costoso, úsese con precaución.” |

---

## 7. Estructura del Código Fuente

| Regla                                         | Significado                                                  |
| --------------------------------------------- | ------------------------------------------------------------ |
| **1. Separar conceptos verticalmente**        | Cada bloque debe estar bien definido y separado visualmente. |
| **2. Agrupar código relacionado**             | Código que trabaja junto debe estar físicamente cerca.       |
| **3. Declarar variables cerca de su uso**     | Facilita la lectura.                                         |
| **4. Agrupar funciones dependientes**         | Las funciones que se llaman entre sí deben estar cerca.      |
| **5. Mantener líneas cortas**                 | Evita que el código se desborde visualmente.                 |
| **6. No usar alineación horizontal excesiva** | Puede ser más confuso que útil.                              |
| **7. Usar espacios en blanco con intención**  | Para agrupar o separar bloques de lógica.                    |
| **8. Respetar la indentación**                | Refleja la estructura lógica del programa.                   |

---

## 8. Objetos y Estructuras de Datos

| Regla                                                                 | Significado                                                                   |
| --------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **1. Ocultar estructura interna**                                     | No exponer los detalles de implementación.                                    |
| **2. Preferir estructuras de datos simples**                          | Cuando sea apropiado, usar mapas, listas, etc. en lugar de objetos complejos. |
| **3. Evitar estructuras híbridas**                                    | No combinar objeto y estructura de datos en una sola clase.                   |
| **4. Ser pequeños y tener una única responsabilidad**                 | Igual que con las funciones.                                                  |
| **5. Reducir número de atributos**                                    | Solo lo esencial.                                                             |
| **6. Las clases base no deben conocer sus derivadas**                 | Mantener la abstracción limpia.                                               |
| **7. Preferir múltiples funciones que recibir código como parámetro** | Aumenta la claridad.                                                          |
| **8. Preferir métodos de instancia a métodos estáticos**              | Permite mayor flexibilidad y testeo.                                          |

---

## 9. Pruebas (Tests)

| Regla                     | Significado                                               |
| ------------------------- | --------------------------------------------------------- |
| **1. Un assert por test** | Cada prueba debe verificar una sola condición específica. |
| **2. Legibles**           | Cualquier persona debe entender qué está validando.       |
| **3. Rápidas**            | Para poder ejecutarlas frecuentemente.                    |
| **4. Independientes**     | No deben depender entre sí.                               |
| **5. Repetibles**         | Siempre deben dar el mismo resultado.                     |

---

## 10. Code Smells (Malos olores de código)

| Smell                       | Descripción                                              |
| --------------------------- | -------------------------------------------------------- |
| **Rigidez**                 | Dificultad para hacer cambios sin afectar todo lo demás. |
| **Fragilidad**              | Un cambio rompe muchas partes del sistema.               |
| **Inmovilidad**             | Código difícil de reutilizar en otro proyecto.           |
| **Complejidad innecesaria** | Uso de patrones o estructuras no requeridas.             |
| **Repetición innecesaria**  | Lógica duplicada en múltiples lugares.                   |
| **Opacidad**                | Código difícil de entender, incluso para su autor.       |

---
