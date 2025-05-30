# Microservicios

Los **microservicios** son un estilo de arquitectura de software que consiste en desarrollar una aplicación como un conjunto de **servicios pequeños, independientes y desacoplados**, que se comunican entre sí a través de **interfaces bien definidas** (por ejemplo, APIs HTTP/REST, gRPC, mensajería, etc.).

### Características clave de los microservicios:

1. **Independencia**:
   Cada microservicio se puede desarrollar, desplegar, escalar y actualizar de forma independiente.

2. **Responsabilidad única**:
   Cada microservicio está enfocado en una función o dominio específico (por ejemplo, gestión de usuarios, pagos, inventario).

3. **Despliegue autónomo**:
   No es necesario desplegar toda la aplicación para actualizar un servicio.

4. **Escalabilidad**:
   Puedes escalar solo los servicios que lo necesiten, en lugar de toda la aplicación.

5. **Tecnologías diversas**:
   Cada microservicio puede estar programado en un lenguaje diferente y usar su propia base de datos (si se desea).

6. **Tolerancia a fallos**:
   Si un microservicio falla, no necesariamente afecta a toda la aplicación (si se maneja correctamente).

---

### Comparación con arquitectura monolítica:

| Característica   | Monolito                | Microservicios                        |
| ---------------- | ----------------------- | ------------------------------------- |
| Tamaño de la app | Una sola unidad grande  | Muchas unidades pequeñas              |
| Escalado         | Escalado de toda la app | Escalado por servicio                 |
| Mantenimiento    | Difícil conforme crece  | Más fácil, pero complejo de orquestar |
| Tecnologías      | Uniformes               | Diversas                              |
| Despliegue       | Toda la app a la vez    | Independiente por servicio            |

---

### Ejemplo simple:

Supongamos una app de e-commerce con microservicios como:

* **Servicio de Usuarios**: Maneja registros y autenticación.
* **Servicio de Productos**: Administra el catálogo.
* **Servicio de Pagos**: Procesa transacciones.
* **Servicio de Envíos**: Coordina la logística.

Cada uno puede estar en un contenedor diferente, con su propia base de datos y tecnología.