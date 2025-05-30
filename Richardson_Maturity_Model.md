# Richardson Maturity Model

El **Modelo de Madurez de Richardson** (Richardson Maturity Model) es un modelo propuesto por **Leonard Richardson** para evaluar el nivel de adherencia de una API web a los principios de **REST** (Representational State Transfer). Este modelo clasifica una API en **cuatro niveles de madurez (del 0 al 3)**, dependiendo de cómo usa los recursos HTTP, las URIs y los métodos.

### Niveles del modelo:

---

#### **Nivel 0 – "Swamp of POX" (Pantano de XML plano)**

* Todo se hace mediante una única URI.
* Usa únicamente el método HTTP POST.
* Normalmente se envía un único bloque de datos (como XML o JSON) para indicar la acción y los datos.
* No hay una verdadera separación de recursos.
* **Ejemplo**: `POST /api` con body `{"action": "getUser", "id": 123}`

---

#### **Nivel 1 – Recursos**

* Introduce el concepto de **recursos identificables** mediante URIs.
* Cada recurso tiene su propia URI.
* Pero aún se utiliza solo un método HTTP, generalmente POST.
* **Ejemplo**:

  * `GET /users`
  * `POST /users/123/delete`

---

#### **Nivel 2 – Verbos HTTP**

* Se empieza a usar correctamente los **métodos HTTP**: GET, POST, PUT, DELETE, etc.
* El uso de estos métodos mejora la semántica y la interoperabilidad.
* **Ejemplo**:

  * `GET /users/123` → obtener usuario
  * `PUT /users/123` → actualizar usuario
  * `DELETE /users/123` → eliminar usuario

---

#### **Nivel 3 – Hipermedios (HATEOAS)**

* El nivel más alto. La API usa **hipermedios como el motor del estado de la aplicación** (HATEOAS: Hypermedia As The Engine Of Application State).
* Las respuestas incluyen enlaces que guían al cliente sobre qué puede hacer después.
* Ayuda a la **descubribilidad** y hace a la API más auto-descriptiva.
* **Ejemplo**:

  ```json
  {
    "id": 123,
    "name": "Juan",
    "links": [
      {"rel": "self", "href": "/users/123"},
      {"rel": "delete", "href": "/users/123"},
      {"rel": "update", "href": "/users/123"}
    ]
  }
  ```

---

### ¿Para qué sirve?

El modelo ayuda a:

* Evaluar qué tan RESTful es una API.
* Guiar el desarrollo hacia buenas prácticas REST.
* Mejorar la interoperabilidad y mantenibilidad de APIs.