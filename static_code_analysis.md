### ¿Qué es el análisis de código estático?

El **análisis de código estático** es el proceso de examinar el código fuente de un programa sin ejecutarlo. Su objetivo es detectar errores, vulnerabilidades, malas prácticas, problemas de estilo o inconsistencias antes de que el código corra, para mejorar la calidad y seguridad del software.

Este análisis se hace sobre el código fuente (o a veces sobre el código intermedio) y permite identificar:

* Errores de sintaxis o semántica.
* Violaciones a reglas de estilo y convenciones.
* Posibles bugs, como variables no inicializadas o condiciones imposibles.
* Vulnerabilidades de seguridad.
* Complejidad y mantenibilidad del código.
* Problemas de rendimiento potenciales.

### ¿Qué ventajas tiene?

* Detectar errores temprano en el ciclo de desarrollo.
* Aumentar la calidad y seguridad del código.
* Facilitar la revisión de código.
* Mejorar la mantenibilidad y legibilidad.
* Cumplir con estándares de codificación y normativas.

---

### Herramientas comunes para análisis de código estático

Dependiendo del lenguaje de programación, hay muchas herramientas. Aquí algunas muy usadas en diferentes ecosistemas:

#### Para varios lenguajes:

* **SonarQube**: Plataforma que soporta muchos lenguajes y da reportes detallados de calidad y seguridad.
* **Checkmarx**: Enfocada en seguridad.
* **Coverity**: Para análisis profundo y detección de vulnerabilidades.

#### Para Java:

* **FindBugs / SpotBugs**
* **PMD**
* **Checkstyle**

#### Para C#/.NET:

* **FxCop / Microsoft Code Analysis**
* **StyleCop**
* **ReSharper** (también ayuda a mejorar código)

#### Para JavaScript/TypeScript:

* **ESLint**
* **TSLint** (obsoleto, ahora ESLint con plugins)
* **JSHint**

#### Para Python:

* **Pylint**
* **Flake8**
* **mypy** (análisis de tipos)

#### Para C/C++:

* **Cppcheck**
* **Clang-Tidy**
* **PVS-Studio**
