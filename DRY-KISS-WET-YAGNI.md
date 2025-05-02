##  1. DRY — Don't Repeat Yourself

> Evita duplicar lógica o estructuras de código. Usa funciones, clases o mixins reutilizables.

####  Ejemplo:

```dart
double calculateArea(double width, double height) => width * height;

// Reutilización:
double a1 = calculateArea(5, 4);
double a2 = calculateArea(6, 7);
```

---

##  2. KISS — Keep It Simple, Stupid

> Mantén el código simple, claro y directo. Evita complejidad innecesaria.

####  Ejemplo:

```dart
//  Complejo:
bool isEven(int n) => n % 2 == 0 ? true : false;

//  Simple:
bool isEvenSimple(int n) => n % 2 == 0;
```

---

##  3. WET — Write Everything Twice

> Antipatrón. Ocurre cuando se repite código en varios lugares.

####  Ejemplo Incorrecto:

```dart
void printUser() {
  print('Nombre: John');
  print('Edad: 30');
}

void printAdmin() {
  print('Nombre: John');
  print('Edad: 30');
}
```

####  Solución DRY:

```dart
void printPerson(String name, int age) {
  print('Nombre: $name');
  print('Edad: $age');
}
```

---

##  4. YAGNI — You Aren't Gonna Need It

> No implementes funcionalidades "por si acaso". Solo agrega lo necesario en el momento que se requiera.

####  Ejemplo Incorrecto:

```dart
class User {
  String name;
  String email;
  String? phoneNumber; // ¿Se necesita?
  User(this.name, this.email, [this.phoneNumber]);
}
```

####  Mejor práctica:

```dart
class User {
  String name;
  String email;

  User(this.name, this.email);
}
```