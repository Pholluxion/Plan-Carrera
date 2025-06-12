### 1. **DRIVERS de arquitectura**

**Definición formal:**
Los *architecture drivers* son los factores clave que influyen directamente en el diseño arquitectónico de un sistema de software. Estos factores representan consideraciones fundamentales que deben ser abordadas y guiadas por las decisiones arquitectónicas.

Los *drivers* se clasifican en:

#### a) **Restricciones técnicas**

Limitaciones impuestas por el entorno técnico o tecnológico del sistema.

> *Ejemplo:* "El sistema debe estar implementado en Java y ejecutarse sobre Kubernetes."

#### b) **Restricciones de negocio**

Condiciones no técnicas impuestas por objetivos comerciales, políticas organizacionales o regulatorias.

> *Ejemplo:* "El producto debe lanzarse al mercado en un plazo de 3 meses."

#### c) **Atributos de calidad del negocio**

Propiedades deseadas del sistema relacionadas con la percepción del valor de negocio, como disponibilidad o escalabilidad.

> *Ejemplo:* "El sistema debe soportar hasta un millón de usuarios activos mensuales."

#### d) **Atributos de calidad técnicos**

Requisitos no funcionales relacionados con el comportamiento interno del sistema, que afectan su estructura o desempeño.

> *Ejemplo:* "El sistema debe responder en menos de 2 segundos en el 95% de los casos."

#### e) **Requerimientos funcionales**

Funciones o capacidades que el sistema debe ofrecer a los usuarios o integraciones externas.

> *Ejemplo:* "El sistema debe permitir registrar nuevos usuarios mediante correo electrónico."

---

### 2. **Trade-off**

**Definición formal:**
Un *trade-off* arquitectónico es una decisión en la que se optimiza un conjunto de propiedades del sistema a expensas de otras. Surge debido a la imposibilidad de maximizar simultáneamente todos los atributos de calidad.

> *Ejemplo:* "Mejorar la seguridad mediante cifrado puede reducir el rendimiento del sistema."

---

### 3. **Ejemplo de driver de arquitectura**

**Ejemplo concreto:**

> Proyecto: Plataforma de pagos móviles.
>
> * **Restricción técnica:** Debe desarrollarse en Flutter.
> * **Restricción de negocio:** Tiempo máximo de desarrollo: 4 meses.
> * **Atributo de calidad técnico:** Alta disponibilidad (99.95%).
> * **Requerimiento funcional:** El usuario debe poder realizar pagos con QR.

Estos *drivers* influirán en decisiones como el tipo de arquitectura (por ejemplo, basada en microservicios), la selección de tecnologías en la nube y el diseño de pruebas de carga.

---

### 4. **ADD – Attribute-Driven Design**

**Definición formal:**
*Attribute-Driven Design (ADD)* es un método de diseño arquitectónico basado en la priorización de atributos de calidad. ADD parte de los *drivers* de arquitectura y los traduce en decisiones estructurales utilizando patrones y tácticas que permiten satisfacer dichos atributos.

> Referencia: Clements, Kazman, Klein – *"Documenting Software Architectures"*

---

### 5. **Modelo 4+1 de vistas arquitectónicas**

**Definición formal:**
El modelo 4+1 de vistas de arquitectura, propuesto por Philippe Kruchten, organiza la descripción de la arquitectura de software en cinco vistas interrelacionadas que abordan diferentes intereses de los stakeholders:

1. **Vista lógica:** modela la funcionalidad del sistema mediante diagramas de clases y objetos.
2. **Vista de desarrollo (implementación):** muestra la organización del software desde la perspectiva del programador.
3. **Vista de procesos:** captura la concurrencia, sincronización y comunicación entre procesos.
4. **Vista física (infraestructura):** representa la topología de hardware y la distribución del software.
5. **Vista de casos de uso (+1):** describe los escenarios principales que guían las otras vistas.

> *Objetivo:* Asegurar que la arquitectura sea comprensible y verificable desde múltiples perspectivas.

---

### 6. **DDD – Domain-Driven Design**

**Definición formal:**
*Domain-Driven Design (DDD)* es un enfoque de modelado de software centrado en el dominio del problema, que promueve la alineación entre los modelos de negocio y el diseño del software. DDD utiliza un modelo de dominio rico expresado en un *lenguaje ubicuo* compartido entre desarrolladores y expertos del negocio.

> Términos clave: entidad, valor, agregado, repositorio, servicio de dominio, contexto delimitado (*bounded context*).

> Fuente: Eric Evans – *"Domain-Driven Design: Tackling Complexity in the Heart of Software"*

---

### 7. **TDD – Test-Driven Development**

**Definición formal:**
*Test-Driven Development (TDD)* es una metodología de desarrollo donde las pruebas automatizadas se escriben antes del código funcional. El ciclo de trabajo incluye tres fases:

1. **Red:** escribir una prueba que falla.
2. **Green:** escribir el código mínimo para que la prueba pase.
3. **Refactor:** mejorar el código sin alterar su comportamiento externo.

> Beneficio: asegura que el código está continuamente verificado mediante pruebas, mejorando la calidad y facilitando el mantenimiento.

---

### 8. **BDD – Behavior-Driven Development**

**Definición formal:**
*Behavior-Driven Development (BDD)* es una metodología de desarrollo ágil centrada en el comportamiento del sistema descrito en lenguaje natural. Busca la colaboración activa entre desarrolladores, QA y negocio mediante ejemplos y escenarios que definen el comportamiento esperado.

> Utiliza herramientas como Cucumber o SpecFlow para expresar pruebas con lenguaje estructurado tipo Gherkin.

> Ejemplo (en Gherkin):

```gherkin
Escenario: Inicio de sesión exitoso
Dado que el usuario tiene una cuenta válida
Cuando ingresa su usuario y contraseña correctamente
Entonces debería acceder al panel principal
```

---