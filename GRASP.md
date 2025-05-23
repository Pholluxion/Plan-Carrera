# Patrones GRASP

GRASP es el acrónimo de General Responsibility Assignment Software Patterns o, traducido al español, patrones de asignación de responsabilidad general. Estos patrones pertenecen a una metodología denominada OOAD (Object-Oriented Analysis and Design) que utiliza una orientación a objetos para modelar y diseñar sistemas.

Los patrones GRASP (aunque muchos son más principios que patrones) nos indican reglas o técnicas para asignar responsabilidades en nuestro software con el fin de mantener bajo acoplamiento, conseguir alta cohesión y hacer nuestro software más escalable y mantenible.

---

## 1. Information Expert (Experto en Información)

**Definición:**
Asigna una responsabilidad a la clase que tiene la información necesaria para cumplirla de forma lógica y natural.

**Por qué existe:**
Evita código disperso. Si una clase ya tiene los datos, también debe tener la lógica que los manipula.

**Para qué sirve:**
Maximiza la cohesión y reduce el acoplamiento entre objetos.

**Ejemplo:**

```csharp
public class Producto {
    public decimal PrecioUnitario { get; set; }
    public int Cantidad { get; set; }

    public decimal CalcularSubtotal() {
        return PrecioUnitario * Cantidad;
    }
}
```

**Implementación:**
Ubica los métodos directamente en la clase que posee los datos requeridos.

---

## 2. Creator (Creador)

**Definición:**
Una clase debe ser responsable de crear instancias de otra clase si la contiene, la utiliza, o tiene la información para inicializarla.

**Por qué existe:**
Permite que la creación de objetos esté a cargo de las clases que tienen una relación natural con ellos.

**Para qué sirve:**
Evita acoplamientos innecesarios y promueve la cohesión.

**Ejemplo:**

```csharp
public class Pedido {
    private List<Producto> productos = new List<Producto>();

    public void AgregarProducto(string nombre, decimal precio, int cantidad) {
        var producto = new Producto { PrecioUnitario = precio, Cantidad = cantidad };
        productos.Add(producto);
    }
}
```

**Implementación:**
Cuando una clase contiene o utiliza objetos de otra clase, es responsable de su creación.

---

## 3. Controller (Controlador)

**Definición:**
Clase que maneja los eventos del sistema y coordina las operaciones necesarias en respuesta a estos.

**Por qué existe:**
Separa la lógica de negocio de la interfaz de usuario y proporciona un punto centralizado para manejar solicitudes.

**Para qué sirve:**
Promueve la separación de responsabilidades y mejora la mantenibilidad del sistema.

**Ejemplo:**

```csharp
public class VentaController {
    private readonly ServicioVenta servicio;

    public VentaController(ServicioVenta servicio) {
        this.servicio = servicio;
    }

    public void IniciarVenta(List<Producto> productos) {
        servicio.RealizarVenta(productos);
    }
}
```

**Implementación:**
Define una clase que actúe como intermediaria entre la UI y el modelo.

---

## 4. Low Coupling (Bajo Acoplamiento)

**Definición:**
Diseñar clases con el mínimo de dependencias posibles entre ellas.

**Por qué existe:**
Reduce el impacto de los cambios en el sistema y facilita la reutilización y pruebas.

**Para qué sirve:**
Mejorar la flexibilidad del sistema y su mantenibilidad.

**Ejemplo:**

```csharp
public interface IRepositorioClientes {
    Cliente ObtenerPorId(int id);
}

public class ClienteService {
    private readonly IRepositorioClientes repo;

    public ClienteService(IRepositorioClientes repo) {
        this.repo = repo;
    }

    public Cliente Buscar(int id) {
        return repo.ObtenerPorId(id);
    }
}
```

**Implementación:**
Usar interfaces, inyección de dependencias y diseño basado en contratos para desacoplar clases.

---

## 5. High Cohesion (Alta Cohesión)

**Definición:**
Mantener juntas las responsabilidades que están estrechamente relacionadas.

**Por qué existe:**
Clases cohesionadas son más claras, fáciles de mantener y de reutilizar.

**Para qué sirve:**
Ayuda a que cada clase tenga una sola responsabilidad claramente definida.

**Ejemplo:**

```csharp
public class GeneradorFacturas {
    public void GenerarPDF(Factura factura) {
        // Generación de PDF
    }

    public void GenerarEmail(Factura factura) {
        // Envío por email
    }
}
```

**Implementación:**
Diseñar clases enfocadas en una única responsabilidad o grupo de tareas relacionadas.

---

## 6. Polymorphism (Polimorfismo)

**Definición:**
Permite tratar distintos tipos de objetos de manera uniforme mediante interfaces o clases base.

**Por qué existe:**
Evita estructuras condicionales extensas y facilita la extensión del sistema.

**Para qué sirve:**
Permitir el uso flexible de distintos comportamientos que comparten una misma interfaz.

**Ejemplo:**

```csharp
public interface IMetodoPago {
    void ProcesarPago();
}

public class PagoTarjeta : IMetodoPago {
    public void ProcesarPago() {
        Console.WriteLine("Procesando pago con tarjeta");
    }
}

public class Caja {
    public void RealizarPago(IMetodoPago metodo) {
        metodo.ProcesarPago();
    }
}
```

**Implementación:**
Utilizar interfaces o clases abstractas y herencia para representar comportamientos intercambiables.

---

## 7. Pure Fabrication (Fabricación Pura)

**Definición:**
Clase que no representa una entidad del dominio, creada para cumplir una necesidad técnica o de diseño.

**Por qué existe:**
Permite mejorar la cohesión y reducir el acoplamiento técnico.

**Para qué sirve:**
Separar lógica técnica o de infraestructura del dominio de negocio.

**Ejemplo:**

```csharp
public class EmailService {
    public void Enviar(string destino, string mensaje) {
        Console.WriteLine($"Enviando email a {destino}: {mensaje}");
    }
}
```

**Implementación:**
Crear clases auxiliares para responsabilidades técnicas (como logging, acceso a datos, validación, etc.).

---

## 8. Indirection (Indirección)

**Definición:**
Usar un objeto intermediario para desacoplar dos clases que no deben comunicarse directamente.

**Por qué existe:**
Permite cambiar una parte del sistema sin afectar directamente al resto.

**Para qué sirve:**
Facilita la flexibilidad, el mantenimiento y el testeo del sistema.

**Ejemplo:**

```csharp
public interface IDB {
    void Guardar(object entidad);
}

public class DBSQL : IDB {
    public void Guardar(object entidad) {
        Console.WriteLine("Guardado en SQL.");
    }
}

public class ServicioNegocio {
    private IDB db;

    public ServicioNegocio(IDB db) {
        this.db = db;
    }

    public void Ejecutar() {
        db.Guardar(new { });
    }
}
```

**Implementación:**
Utiliza intermediarios como interfaces, controladores o adaptadores para reducir dependencias directas.

---

## 9. Protected Variations (Variaciones Protegidas)

**Definición:**
Proteger partes del sistema que son susceptibles al cambio mediante interfaces o clases abstractas.

**Por qué existe:**
Permite modificar una parte del sistema sin afectar el resto.

**Para qué sirve:**
Aislar los puntos de cambio y proteger el sistema contra inestabilidad.

**Ejemplo:**

```csharp
public interface INotificador {
    void Enviar(string mensaje);
}

public class NotificadorEmail : INotificador {
    public void Enviar(string mensaje) {
        Console.WriteLine("Email enviado: " + mensaje);
    }
}

public class Alerta {
    private readonly INotificador notificador;

    public Alerta(INotificador notificador) {
        this.notificador = notificador;
    }

    public void EnviarAlerta(string mensaje) {
        notificador.Enviar(mensaje);
    }
}
```

**Implementación:**
Encapsular elementos susceptibles a cambio detrás de una interfaz.

---