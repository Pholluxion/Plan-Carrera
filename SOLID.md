
## SOLID

Los principios **SOLID** promueven un diseño mantenible y escalable en programación orientada a objetos.

### S — Single Responsibility Principle (SRP)

> Una clase debe tener una sola responsabilidad o razón para cambiar.

####  Ejemplo:


**Antes**: Una clase generaba y guardaba el reporte.
```dart
class ReportManager {
  String generateReport() {
    // Lógica de generación del reporte
    return 'Reporte generado';
  }

  void saveReport(String data) {
    // Lógica para guardar el reporte en archivo
    print('Guardando en archivo: $data');
  }

  void sendReportByEmail(String data) {
    // Lógica para enviar el reporte por correo
    print('Enviando correo: $data');
  }
}
```
**Después**: Cada clase se enfoca en una única responsabilidad.
```dart
class ReportGenerator {
  String generate() => 'Report data';
}

class ReportSaver {
  void saveToFile(String data) {
    print('Saving: $data');
  }
}
```



---

### O — Open/Closed Principle (OCP)

> Las clases deben estar abiertas para extensión, pero cerradas para modificación.

####  Ejemplo:

```dart
abstract class Shape {
  double area();
}

class Circle implements Shape {
  final double radius;
  Circle(this.radius);

  @override
  double area() => 3.14 * radius * radius;
}

class Square implements Shape {
  final double side;
  Square(this.side);

  @override
  double area() => side * side;
}
```

Nuevas figuras pueden agregarse **sin modificar** clases existentes.

---

### L — Liskov Substitution Principle (LSP)

> Las clases derivadas deben poder usarse en lugar de sus clases base sin romper el comportamiento esperado.

####  Ejemplo:

```dart
class Bird {
  void fly() => print('Flying...');
}

class Sparrow extends Bird {}

void letItFly(Bird bird) {
  bird.fly();
}
```

**Nota**: Si se añade una clase como `Penguin` que no puede volar, puede violar este principio.

---

### I — Interface Segregation Principle (ISP)

> No obligues a una clase a implementar interfaces que no usa.

####  Ejemplo:

```dart
abstract class Printer {
  void printDoc();
}

abstract class Scanner {
  void scanDoc();
}

class SimplePrinter implements Printer {
  @override
  void printDoc() => print('Printing...');
}
```

Interfaces específicas y pequeñas evitan la implementación innecesaria.

---

### D — Dependency Inversion Principle (DIP)

> Las clases deben depender de abstracciones, no de implementaciones concretas.

####  Ejemplo:

```dart
abstract class NotificationService {
  void send(String message);
}

class EmailService implements NotificationService {
  @override
  void send(String message) => print('Email: $message');
}

class Notifier {
  final NotificationService service;
  Notifier(this.service);

  void notify(String msg) => service.send(msg);
}
```

El `Notifier` funciona con cualquier implementación de `NotificationService`.

---