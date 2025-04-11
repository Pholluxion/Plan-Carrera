# Compose Method y SLAP

## Compose Method

### ¿Qué es?
El método de composición es un patrón muy básico que debería estar presente en el arsenal de refactorización de todos. Un método de composición no es más que un método que llama a otros métodos. Se aplica mejor cuando todos los métodos llamados tienen prácticamente el mismo nivel de detalle.

Refactorizar hacia un método de composición suele implicar extraer código del método original. Si le resulta difícil nombrar los métodos extraídos, esto indica que el fragmento de código que iba a extraer era demasiado grande; en ese caso, intente encontrar un fragmento más pequeño. En los métodos más largos, algunas secciones suelen estar etiquetadas con un comentario; estas secciones pueden extraerse con frecuencia para crear nuevos métodos.

### ¿Por qué usarlo?
- Mejora la legibilidad del código.
- Facilita la reutilización.
- Ayuda a mantener el principio de una sola responsabilidad.
- Facilita el testeo individual de las partes.


```dart
void main() {
  final usuario = Usuario('Gabriela', 'Galvis');
  usuario.mostrarInformacion();
}

class Usuario {
  final String nombre;
  final String apellido;

  Usuario(this.nombre, this.apellido);

  void mostrarInformacion() {
    final nombreCompleto = _obtenerNombreCompleto();
    final saludo = _generarSaludo(nombreCompleto);
    _mostrarEnConsola(saludo);
  }

  String _obtenerNombreCompleto() => '$nombre $apellido';

  String _generarSaludo(String nombre) => 'Hola, $nombre 👋';

  void _mostrarEnConsola(String mensaje) => print(mensaje);
}

```

---

## SLAP (Single Level of Abstraction Principle)

### ¿Qué es?
El principio slap propone que el código tenga un único nivel de abstracción. Es decir, un bloque de código no debe mezclar lo que hace el código con su funcionamiento. Dado que SLAP promueve la claridad, la mantenibilidad y la reutilización del código, las funciones y los módulos se centran en completar una sola tarea a la vez. El código es más fácil de leer, comprender y modificar cuando se encuentra en el mismo nivel de abstracción, ya que es modular y cada parte puede entenderse de forma independiente. Por lo tanto, el código de una función o módulo debe estar en el mismo nivel de abstracción y no debe mezclar detalles de implementación de nivel inferior con lógica de negocio de nivel superior.

### ¿Por qué usarlo?
- Mejora la cohesión.
- Facilita la lectura: todo está al mismo nivel de pensamiento.
- Permite moverse rápidamente por el código sin perder contexto.

---

### Antes

``` dart
void enviarCorreo(String destinatario, String nombre) {
  final saludo = 'Hola $nombre';
  final asunto = 'Bienvenido';
  final cuerpo = 'Gracias por registrarte.';
  final mensaje = '$saludo\n\n$cuerpo';

  print('Enviando a $destinatario: $asunto\n$mensaje');
}

```

### Despues

```dart
void main() {
  final servicioCorreo = ServicioCorreo();
  servicioCorreo.enviarCorreo('gabriela@example.com', 'Gabriela');
}

class ServicioCorreo {
  void enviarCorreo(String destinatario, String nombre) {
    final mensaje = _crearMensaje(nombre);
    _enviar(destinatario, mensaje);
  }

  String _crearMensaje(String nombre) {
    final saludo = _crearSaludo(nombre);
    final cuerpo = _crearCuerpo();
    return '$saludo\n\n$cuerpo';
  }

  String _crearSaludo(String nombre) => 'Hola $nombre';
  String _crearCuerpo() => 'Gracias por registrarte.';
  void _enviar(String destino, String mensaje) {
    print('Enviando a $destino:\n$mensaje');
  }
}

```


---


## Escenario: Queremos registrar un usuario verificando su correo, almacenando la fecha de registro, y devolviendo un mensaje de éxito o error.


## Código inicial (antes del refactor)

```dart
class RegistroService {
  void registrar(String nombre, String correo) {
    if (!correo.contains('@')) {
      print('Correo inválido');
      return;
    }

    final fecha = DateTime.now().toIso8601String();
    print('Usuario $nombre registrado con el correo $correo');
    print('Fecha de registro: $fecha');
  }
}
```

Problemas:
- No sigue **Single Responsibility Principle**.
- Lógica de validación, registro y presentación están mezcladas.
- Difícil de mantener o testear.

---

## Paso 1: Aplicamos **Compose Method**

```dart
class RegistroService {
  void registrar(String nombre, String correo) {
    if (!_correoValido(correo)) {
      _mostrarError();
      return;
    }

    final fecha = _obtenerFechaActual();
    _mostrarConfirmacion(nombre, correo, fecha);
  }

  bool _correoValido(String correo) => correo.contains('@');

  String _obtenerFechaActual() => DateTime.now().toIso8601String();

  void _mostrarError() {
    print('Correo inválido');
  }

  void _mostrarConfirmacion(String nombre, String correo, String fecha) {
    print('Usuario $nombre registrado con el correo $correo');
    print('Fecha de registro: $fecha');
  }
}
```

Aquí ya usamos **Compose Method**: cada parte del proceso está separada en funciones descriptivas.

---

## Paso 2: Aplicamos **SLAP** (Single Level of Abstraction Principle)

```dart
class RegistroService {
  void registrar(String nombre, String correo) {
    if (!_correoValido(correo)) {
      _mostrarError();
      return;
    }

    _procesarRegistro(nombre, correo);
  }

  void _procesarRegistro(String nombre, String correo) {
    final fecha = _obtenerFechaActual();
    _mostrarConfirmacion(nombre, correo, fecha);
  }

  bool _correoValido(String correo) => correo.contains('@');

  String _obtenerFechaActual() => DateTime.now().toIso8601String();

  void _mostrarError() {
    print('Correo inválido');
  }

  void _mostrarConfirmacion(String nombre, String correo, String fecha) {
    print('Usuario $nombre registrado con el correo $correo');
    print('Fecha de registro: $fecha');
  }
}
```