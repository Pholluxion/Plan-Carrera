**GoF** significa **Gang of Four** (en español, *la Banda de los Cuatro*), un término ampliamente conocido en el mundo del desarrollo de software.

## ¿Quiénes son los GoF?

Se refiere a los autores del libro **"Design Patterns: Elements of Reusable Object-Oriented Software"**, publicado en 1994:

* **Erich Gamma**
* **Richard Helm**
* **Ralph Johnson**
* **John Vlissides**

Juntos, propusieron un catálogo de **23 patrones de diseño** que ayudan a **resolver problemas comunes** en el desarrollo de software orientado a objetos, especialmente con lenguajes como C++, Java y C#. Estos patrones han sido tan influyentes que el término "GoF patterns" es sinónimo de "patrones de diseño clásicos".

---

## ¿Qué son los patrones de diseño GoF?

Son **soluciones reutilizables a problemas de diseño comunes**. No son código específico, sino **plantillas conceptuales** que se pueden aplicar a muchos contextos.

Se dividen en tres categorías:

1. **Patrones Creacionales** – Cómo se crean los objetos.
2. **Patrones Estructurales** – Cómo se componen los objetos.
3. **Patrones de Comportamiento** – Cómo interactúan los objetos.

---

## ¿Por qué son importantes?

* Fomentan **reutilización** de soluciones probadas.
* Ayudan a **comunicar ideas** con un lenguaje común.
* Mejoran el diseño y **mantenibilidad** del software.
* Favorecen el **principio de responsabilidad única** y el **principio abierto/cerrado**.

---

# Patrones Creacionales

Los **patrones creacionales** se encargan de **crear objetos** de manera que el código sea más flexible, reutilizable y fácil de mantener.

---

## 1. Singleton

### ¿Qué hace?

Se asegura de que **solo exista una instancia** de una clase y proporciona un punto global para acceder a ella.

### ¿Cuándo usarlo?

Cuando necesitas **una sola instancia** compartida, por ejemplo: una clase de configuración, un logger o conexión a base de datos.

### Ejemplo:

```csharp
public class Logger
{
    private static Logger _instance;

    private Logger() { } // Constructor privado

    public static Logger GetInstance()
    {
        if (_instance == null)
        {
            _instance = new Logger();
        }
        return _instance;
    }

    public void Log(string message)
    {
        Console.WriteLine($"Log: {message}");
    }
}
```

**Uso:**

```csharp
Logger logger = Logger.GetInstance();
logger.Log("Hola mundo");
```

---

## 2. Factory Method

### ¿Qué hace?

Permite crear objetos sin decir explícitamente **la clase exacta** que se debe instanciar.

### ¿Cuándo usarlo?

Cuando el **tipo de objeto que se necesita puede variar** dependiendo del contexto o configuración.

### Ejemplo:

```csharp
public interface IAnimal
{
    void Hablar();
}

public class Perro : IAnimal
{
    public void Hablar() => Console.WriteLine("Guau");
}

public class Gato : IAnimal
{
    public void Hablar() => Console.WriteLine("Miau");
}

public class AnimalFactory
{
    public static IAnimal CrearAnimal(string tipo)
    {
        if (tipo == "perro") return new Perro();
        if (tipo == "gato") return new Gato();
        return null;
    }
}
```

**Uso:**

```csharp
IAnimal animal = AnimalFactory.CrearAnimal("gato");
animal.Hablar(); // Miau
```

---

## 3. Abstract Factory

### ¿Qué hace?

Crea **familias de objetos relacionados** (como botones y menús para Windows o Mac) sin especificar sus clases concretas.

### ¿Cuándo usarlo?

Cuando tu sistema debe ser **independiente del sistema operativo, entorno o estilo de objetos** que usa.

### Ejemplo:

```csharp
// Productos
public interface IBoton { void Dibujar(); }
public interface IMenu { void Mostrar(); }

public class BotonWindows : IBoton
{
    public void Dibujar() => Console.WriteLine("Botón estilo Windows");
}

public class MenuWindows : IMenu
{
    public void Mostrar() => Console.WriteLine("Menú estilo Windows");
}

// Fábrica abstracta
public interface IGUIFactory
{
    IBoton CrearBoton();
    IMenu CrearMenu();
}

// Fábrica concreta
public class WindowsFactory : IGUIFactory
{
    public IBoton CrearBoton() => new BotonWindows();
    public IMenu CrearMenu() => new MenuWindows();
}
```

**Uso:**

```csharp
IGUIFactory factory = new WindowsFactory();
IBoton boton = factory.CrearBoton();
IMenu menu = factory.CrearMenu();

boton.Dibujar();
menu.Mostrar();
```

---

## 4. Builder

### ¿Qué hace?

Permite construir objetos **complejos paso a paso** y con diferentes representaciones.

### ¿Cuándo usarlo?

Cuando tienes que construir objetos con **muchas partes opcionales o configurables**.

### Ejemplo:

```csharp
public class Hamburguesa
{
    public string Pan { get; set; }
    public string Carne { get; set; }
    public string Salsa { get; set; }

    public void Mostrar() =>
        Console.WriteLine($"Hamburguesa: {Pan}, {Carne}, {Salsa}");
}

public class HamburguesaBuilder
{
    private Hamburguesa _hamburguesa = new Hamburguesa();

    public HamburguesaBuilder ConPan(string pan)
    {
        _hamburguesa.Pan = pan;
        return this;
    }

    public HamburguesaBuilder ConCarne(string carne)
    {
        _hamburguesa.Carne = carne;
        return this;
    }

    public HamburguesaBuilder ConSalsa(string salsa)
    {
        _hamburguesa.Salsa = salsa;
        return this;
    }

    public Hamburguesa Construir() => _hamburguesa;
}
```

**Uso:**

```csharp
var builder = new HamburguesaBuilder();
var miHamburguesa = builder
    .ConPan("Integral")
    .ConCarne("Res")
    .ConSalsa("BBQ")
    .Construir();

miHamburguesa.Mostrar();
```

---

## 5. Prototype

### ¿Qué hace?

Crea nuevos objetos **copiando otros existentes** (clonarlos).

### ¿Cuándo usarlo?

Cuando necesitas **copiar un objeto** muchas veces y su construcción es costosa.

### Ejemplo:

```csharp
public class Persona
{
    public string Nombre { get; set; }

    public Persona Clonar()
    {
        return (Persona)this.MemberwiseClone(); // Copia superficial
    }
}
```

**Uso:**

```csharp
Persona original = new Persona { Nombre = "Ana" };
Persona copia = original.Clonar();
copia.Nombre = "Luis";

Console.WriteLine(original.Nombre); // Ana
Console.WriteLine(copia.Nombre);    // Luis
```


--- 


# Patrones Estructurales

Los **patrones estructurales** se enfocan en **cómo se relacionan y organizan las clases y objetos** para formar estructuras más grandes y flexibles.

---

## 1. Adapter

### ¿Qué hace?

Permite que dos clases incompatibles trabajen juntas adaptando una interfaz a otra.

### ¿Cuándo usarlo?

Cuando necesitas usar una clase existente, pero su interfaz no es compatible con lo que necesitas.

### Ejemplo:

```csharp
// Clase que ya existe
public class MotorAntiguo
{
    public void Encender() => Console.WriteLine("Motor antiguo encendido");
}

// Interfaz que necesita el nuevo sistema
public interface IMotor
{
    void Activar();
}

// Adaptador
public class AdaptadorMotor : IMotor
{
    private MotorAntiguo _motorAntiguo = new MotorAntiguo();

    public void Activar()
    {
        _motorAntiguo.Encender();
    }
}
```

**Uso:**

```csharp
IMotor motor = new AdaptadorMotor();
motor.Activar();
```

---

## 2. Bridge

### ¿Qué hace?

Separa una abstracción de su implementación para que puedan variar independientemente.

### ¿Cuándo usarlo?

Cuando quieres separar lo que hace un objeto (abstracción) de cómo lo hace (implementación).

### Ejemplo:

```csharp
public interface IDispositivo
{
    void Encender();
}

public class TV : IDispositivo
{
    public void Encender() => Console.WriteLine("TV encendida");
}

public class ControlRemoto
{
    protected IDispositivo _dispositivo;

    public ControlRemoto(IDispositivo dispositivo)
    {
        _dispositivo = dispositivo;
    }

    public void BotonEncender()
    {
        _dispositivo.Encender();
    }
}
```

**Uso:**

```csharp
IDispositivo tv = new TV();
var control = new ControlRemoto(tv);
control.BotonEncender();
```

---

## 3. Composite

### ¿Qué hace?

Permite tratar objetos individuales y composiciones de objetos de manera uniforme.

### ¿Cuándo usarlo?

Cuando tienes una estructura en árbol (como menús, carpetas, jerarquías).

### Ejemplo:

```csharp
public abstract class Componente
{
    public abstract void Mostrar();
}

public class Hoja : Componente
{
    private string _nombre;
    public Hoja(string nombre) => _nombre = nombre;
    public override void Mostrar() => Console.WriteLine(_nombre);
}

public class Compuesto : Componente
{
    private List<Componente> _hijos = new List<Componente>();
    private string _nombre;

    public Compuesto(string nombre) => _nombre = nombre;

    public void Agregar(Componente componente) => _hijos.Add(componente);

    public override void Mostrar()
    {
        Console.WriteLine(_nombre);
        foreach (var hijo in _hijos)
        {
            hijo.Mostrar();
        }
    }
}
```

**Uso:**

```csharp
var raiz = new Compuesto("Carpeta Raíz");
raiz.Agregar(new Hoja("Archivo 1"));
raiz.Agregar(new Hoja("Archivo 2"));

var subcarpeta = new Compuesto("Subcarpeta");
subcarpeta.Agregar(new Hoja("Archivo 3"));

raiz.Agregar(subcarpeta);
raiz.Mostrar();
```

---

## 4. Decorator

### ¿Qué hace?

Agrega funcionalidad adicional a un objeto en tiempo de ejecución sin modificar su estructura.

### ¿Cuándo usarlo?

Cuando quieres extender el comportamiento de una clase sin herencia.

### Ejemplo:

```csharp
public interface ICafe
{
    string Descripcion();
}

public class CafeSimple : ICafe
{
    public string Descripcion() => "Café";
}

public class ConLeche : ICafe
{
    private ICafe _cafe;

    public ConLeche(ICafe cafe) => _cafe = cafe;

    public string Descripcion() => _cafe.Descripcion() + " con leche";
}
```

**Uso:**

```csharp
ICafe cafe = new CafeSimple();
ICafe cafeConLeche = new ConLeche(cafe);
Console.WriteLine(cafeConLeche.Descripcion()); // Café con leche
```

---

## 5. Facade

### ¿Qué hace?

Proporciona una interfaz simple para un conjunto complejo de clases o subsistemas.

### ¿Cuándo usarlo?

Cuando quieres simplificar el uso de un sistema complejo.

### Ejemplo:

```csharp
public class CPU
{
    public void Encender() => Console.WriteLine("CPU encendida");
}

public class Disco
{
    public void Leer() => Console.WriteLine("Leyendo disco");
}

public class Computadora
{
    private CPU _cpu = new CPU();
    private Disco _disco = new Disco();

    public void Iniciar()
    {
        _cpu.Encender();
        _disco.Leer();
    }
}
```

**Uso:**

```csharp
var pc = new Computadora();
pc.Iniciar();
```

---

## 6. Flyweight

### ¿Qué hace?

Reduce el uso de memoria compartiendo objetos que son iguales.

### ¿Cuándo usarlo?

Cuando tienes una gran cantidad de objetos similares.

### Ejemplo:

```csharp
public class Letra
{
    private char _caracter;

    public Letra(char caracter) => _caracter = caracter;

    public void Mostrar() => Console.WriteLine($"Letra: {_caracter}");
}

public class FabricaLetras
{
    private Dictionary<char, Letra> _letras = new();

    public Letra ObtenerLetra(char c)
    {
        if (!_letras.ContainsKey(c))
            _letras[c] = new Letra(c);
        return _letras[c];
    }
}
```

**Uso:**

```csharp
var fabrica = new FabricaLetras();
var letraA1 = fabrica.ObtenerLetra('A');
var letraA2 = fabrica.ObtenerLetra('A');

Console.WriteLine(object.ReferenceEquals(letraA1, letraA2)); // True
```

---

## 7. Proxy

### ¿Qué hace?

Proporciona un sustituto para otro objeto para controlar el acceso.

### ¿Cuándo usarlo?

Cuando necesitas control, seguridad, o carga diferida antes de acceder al objeto real.

### Ejemplo:

```csharp
public interface IServicio
{
    void Acceder();
}

public class ServicioReal : IServicio
{
    public void Acceder() => Console.WriteLine("Accediendo al servicio real");
}

public class ProxyServicio : IServicio
{
    private ServicioReal _servicioReal;

    public void Acceder()
    {
        if (_servicioReal == null)
        {
            _servicioReal = new ServicioReal();
        }
        Console.WriteLine("Acceso a través del proxy");
        _servicioReal.Acceder();
    }
}
```

**Uso:**

```csharp
IServicio servicio = new ProxyServicio();
servicio.Acceder();
```

---

# Patrones de Comportamiento

Los **patrones de comportamiento** se enfocan en **cómo interactúan los objetos entre sí** y cómo se comunican para lograr un comportamiento dinámico y flexible.

---

## 1. Chain of Responsibility

### ¿Qué hace?

Permite pasar una petición a lo largo de una cadena de objetos hasta que alguien la maneje.

### ¿Cuándo usarlo?

Cuando varios objetos pueden manejar una petición, y no quieres acoplar el emisor con el receptor.

### Ejemplo:

```csharp
public abstract class Manejador
{
    protected Manejador siguiente;

    public void EstablecerSiguiente(Manejador siguiente)
    {
        this.siguiente = siguiente;
    }

    public abstract void Manejar(string solicitud);
}

public class ManejadorConcretoA : Manejador
{
    public override void Manejar(string solicitud)
    {
        if (solicitud == "A")
            Console.WriteLine("A manejado");
        else if (siguiente != null)
            siguiente.Manejar(solicitud);
    }
}

public class ManejadorConcretoB : Manejador
{
    public override void Manejar(string solicitud)
    {
        if (solicitud == "B")
            Console.WriteLine("B manejado");
        else if (siguiente != null)
            siguiente.Manejar(solicitud);
    }
}
```

**Uso:**

```csharp
var a = new ManejadorConcretoA();
var b = new ManejadorConcretoB();
a.EstablecerSiguiente(b);

a.Manejar("B");  // B manejado
```

---

## 2. Command

### ¿Qué hace?

Encapsula una solicitud como un objeto, permitiendo parametrizar acciones, deshacerlas o almacenarlas.

### ¿Cuándo usarlo?

Cuando necesitas acciones que puedan ser **almacenadas, deshacer, o ejecutarse en otro momento**.

### Ejemplo:

```csharp
public interface ICommand
{
    void Ejecutar();
}

public class Luz
{
    public void Encender() => Console.WriteLine("Luz encendida");
}

public class EncenderLuzCommand : ICommand
{
    private Luz _luz;
    public EncenderLuzCommand(Luz luz) => _luz = luz;
    public void Ejecutar() => _luz.Encender();
}

public class ControlRemoto
{
    private ICommand _comando;
    public ControlRemoto(ICommand comando) => _comando = comando;
    public void PresionarBoton() => _comando.Ejecutar();
}
```

**Uso:**

```csharp
var luz = new Luz();
var comando = new EncenderLuzCommand(luz);
var control = new ControlRemoto(comando);
control.PresionarBoton();  // Luz encendida
```

---

## 3. Interpreter

### ¿Qué hace?

Interpreta sentencias en un lenguaje específico.

### ¿Cuándo usarlo?

Cuando tienes un lenguaje de reglas, expresiones o comandos simples.

### Ejemplo (simplificado):

```csharp
public interface IExpresion
{
    int Interpretar();
}

public class Numero : IExpresion
{
    private int _valor;
    public Numero(int valor) => _valor = valor;
    public int Interpretar() => _valor;
}

public class Suma : IExpresion
{
    private IExpresion _izq, _der;
    public Suma(IExpresion izq, IExpresion der)
    {
        _izq = izq;
        _der = der;
    }
    public int Interpretar() => _izq.Interpretar() + _der.Interpretar();
}
```

**Uso:**

```csharp
IExpresion expresion = new Suma(new Numero(2), new Numero(3));
Console.WriteLine(expresion.Interpretar());  // 5
```

---

## 4. Iterator

### ¿Qué hace?

Permite acceder secuencialmente a los elementos de una colección sin exponer su estructura interna.

### ¿Cuándo usarlo?

Cuando necesitas recorrer una colección sin depender de cómo está implementada.

### Ejemplo:

```csharp
public class Coleccion
{
    private List<string> _elementos = new();

    public void Agregar(string item) => _elementos.Add(item);
    public IEnumerable<string> ObtenerElementos() => _elementos;
}
```

**Uso:**

```csharp
var col = new Coleccion();
col.Agregar("Uno");
col.Agregar("Dos");

foreach (var e in col.ObtenerElementos())
{
    Console.WriteLine(e);
}
```

---

## 5. Mediator

### ¿Qué hace?

Define un objeto que centraliza la comunicación entre otros objetos.

### ¿Cuándo usarlo?

Cuando tienes múltiples objetos intercomunicados y deseas **desacoplarlos**.

### Ejemplo:

```csharp
public class Chat
{
    public void Enviar(string mensaje, Usuario usuario)
    {
        Console.WriteLine($"{usuario.Nombre} dice: {mensaje}");
    }
}

public class Usuario
{
    public string Nombre { get; }
    private Chat _chat;

    public Usuario(string nombre, Chat chat)
    {
        Nombre = nombre;
        _chat = chat;
    }

    public void EnviarMensaje(string mensaje)
    {
        _chat.Enviar(mensaje, this);
    }
}
```

**Uso:**

```csharp
var chat = new Chat();
var u1 = new Usuario("Ana", chat);
var u2 = new Usuario("Luis", chat);

u1.EnviarMensaje("Hola");
```

---

## 6. Memento

### ¿Qué hace?

Permite guardar y restaurar el estado anterior de un objeto sin violar su encapsulación.

### ¿Cuándo usarlo?

Cuando necesitas soporte para **deshacer cambios**.

### Ejemplo:

```csharp
public class Memento
{
    public string Estado { get; }
    public Memento(string estado) => Estado = estado;
}

public class Editor
{
    public string Texto { get; set; }

    public Memento Guardar() => new Memento(Texto);
    public void Restaurar(Memento memento) => Texto = memento.Estado;
}
```

**Uso:**

```csharp
var editor = new Editor();
editor.Texto = "Versión 1";
var respaldo = editor.Guardar();

editor.Texto = "Versión 2";
editor.Restaurar(respaldo);
Console.WriteLine(editor.Texto);  // Versión 1
```

---

## 7. Observer

### ¿Qué hace?

Notifica a múltiples objetos cuando cambia el estado de otro.

### ¿Cuándo usarlo?

Cuando necesitas que varios objetos reaccionen a un cambio en otro objeto.

### Ejemplo:

```csharp
public class Sujeto
{
    private List<IObservador> _observadores = new();
    private int _estado;

    public int Estado
    {
        get => _estado;
        set
        {
            _estado = value;
            Notificar();
        }
    }

    public void Agregar(IObservador o) => _observadores.Add(o);
    public void Notificar()
    {
        foreach (var o in _observadores)
            o.Actualizar(_estado);
    }
}

public interface IObservador
{
    void Actualizar(int estado);
}

public class ObservadorConcreto : IObservador
{
    public void Actualizar(int estado)
    {
        Console.WriteLine($"Estado actualizado a: {estado}");
    }
}
```

**Uso:**

```csharp
var sujeto = new Sujeto();
sujeto.Agregar(new ObservadorConcreto());
sujeto.Estado = 42;
```

---

## 8. State

### ¿Qué hace?

Permite cambiar el comportamiento de un objeto cuando cambia su estado interno.

### ¿Cuándo usarlo?

Cuando un objeto debe comportarse diferente según su estado.

### Ejemplo:

```csharp
public interface IEstado
{
    void Manejar();
}

public class EstadoActivo : IEstado
{
    public void Manejar() => Console.WriteLine("Modo Activo");
}

public class EstadoInactivo : IEstado
{
    public void Manejar() => Console.WriteLine("Modo Inactivo");
}

public class Contexto
{
    private IEstado _estado;

    public void EstablecerEstado(IEstado estado) => _estado = estado;
    public void Solicitud() => _estado.Manejar();
}
```

**Uso:**

```csharp
var contexto = new Contexto();
contexto.EstablecerEstado(new EstadoActivo());
contexto.Solicitud();  // Modo Activo
```

---

## 9. Strategy

### ¿Qué hace?

Define una familia de algoritmos intercambiables.

### ¿Cuándo usarlo?

Cuando tienes múltiples formas de hacer algo y quieres que el algoritmo sea intercambiable en tiempo de ejecución.

### Ejemplo:

```csharp
public interface IOperacion
{
    int Calcular(int a, int b);
}

public class Suma : IOperacion
{
    public int Calcular(int a, int b) => a + b;
}

public class Resta : IOperacion
{
    public int Calcular(int a, int b) => a - b;
}

public class Calculadora
{
    private IOperacion _operacion;
    public void EstablecerOperacion(IOperacion operacion) => _operacion = operacion;
    public int Ejecutar(int a, int b) => _operacion.Calcular(a, b);
}
```

**Uso:**

```csharp
var calc = new Calculadora();
calc.EstablecerOperacion(new Suma());
Console.WriteLine(calc.Ejecutar(3, 2));  // 5
```

---

## 10. Template Method

### ¿Qué hace?

Define el esqueleto de un algoritmo en una clase base, dejando que las subclases implementen los pasos concretos.

### ¿Cuándo usarlo?

Cuando quieres **reutilizar el flujo principal** de un algoritmo, pero permitir personalización de algunos pasos.

### Ejemplo:

```csharp
public abstract class Juego
{
    public void Jugar()
    {
        Iniciar();
        JugarTurno();
        Finalizar();
    }

    protected abstract void Iniciar();
    protected abstract void JugarTurno();
    protected abstract void Finalizar();
}

public class Ajedrez : Juego
{
    protected override void Iniciar() => Console.WriteLine("Inicio ajedrez");
    protected override void JugarTurno() => Console.WriteLine("Moviendo ficha");
    protected override void Finalizar() => Console.WriteLine("Fin del juego");
}
```

**Uso:**

```csharp
var juego = new Ajedrez();
juego.Jugar();
```

---

## 11. Visitor

### ¿Qué hace?

Permite definir operaciones sobre objetos sin modificarlos.

### ¿Cuándo usarlo?

Cuando necesitas agregar nuevas operaciones a una jerarquía de clases sin alterarla.

### Ejemplo:

```csharp
public interface IElemento
{
    void Aceptar(IVisitante visitante);
}

public class ElementoConcreto : IElemento
{
    public void Aceptar(IVisitante visitante)
    {
        visitante.Visitar(this);
    }
}

public interface IVisitante
{
    void Visitar(ElementoConcreto elemento);
}

public class VisitanteConcreto : IVisitante
{
    public void Visitar(ElementoConcreto elemento)
    {
        Console.WriteLine("Visitando elemento");
    }
}
```

**Uso:**

```csharp
var elemento = new ElementoConcreto();
var visitante = new VisitanteConcreto();
elemento.Aceptar(visitante);
```