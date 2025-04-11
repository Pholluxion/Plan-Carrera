
# Paradigmas de Programación

## 1. Paradigma Orientado a Objetos (OOP)

- **Descripción:** Organiza el software en objetos que combinan datos y comportamientos.
- **Usos:** Aplicaciones móviles (Flutter), backend con Dart, lógica de negocio estructurada.
- **Lenguajes comunes:** Dart, Java, C#, Kotlin.

Este paradigma se basa en el concepto de "objetos", que son instancias de clases que encapsulan datos (atributos) y comportamientos (métodos). La programación orientada a objetos permite modelar entidades del mundo real, favorece la reutilización del código mediante la herencia y promueve una arquitectura más mantenible a través del principio de encapsulamiento. Dart es un lenguaje orientado a objetos por naturaleza, por lo que este enfoque es el más común en aplicaciones desarrolladas con Flutter.

**Ejemplo (Dart):**
```dart
class Suma {
  final List<int> numeros;

  Suma(this.numeros);

  int calcular() {
    return numeros.reduce((a, b) => a + b);
  }
}

void main() {
  var s = Suma([1, 2, 3, 4]);
  print(s.calcular());
}
```

**Explicación:** Se crea una clase `Suma` que contiene una lista de números y un método `calcular` que realiza la suma usando `reduce`.

---

## 2. Paradigma Funcional

- **Descripción:** Usa funciones puras, evita mutabilidad, y se basa en composición funcional.
- **Usos:** Transformaciones de datos, programación reactiva, manipulación inmutable.
- **Lenguajes comunes:** Dart, Haskell, Scala, Elixir.

La programación funcional se centra en el uso de funciones como bloques fundamentales de construcción. Se evita la modificación del estado o datos mutables, favoreciendo funciones puras, es decir, aquellas que para los mismos argumentos siempre retornan el mismo resultado y no generan efectos secundarios. Dart incorpora muchas características funcionales que permiten escribir código más conciso, expresivo y fácil de testear, especialmente útil al trabajar con colecciones.

**Ejemplo (Dart):**
```dart
void main() {
  final numeros = [1, 2, 3, 4];
  final resultado = numeros.reduce((a, b) => a + b);
  print(resultado);
}
```

**Explicación:** Se usa `reduce` para sumar todos los elementos de la lista sin modificar su estado original.

---

## 3. Paradigma Imperativo / Estructurado

- **Descripción:** Define paso a paso cómo resolver el problema, usando bucles y variables mutables.
- **Usos:** Scripts, lógica de control detallada.
- **Lenguajes comunes:** Dart, C, Python, JavaScript.

Este paradigma describe en detalle las instrucciones que debe seguir la computadora para alcanzar un objetivo. Utiliza variables, estructuras de control como bucles y condicionales, y se centra en el "cómo" resolver una tarea. Es uno de los estilos más accesibles para principiantes y sigue siendo útil para resolver problemas simples de forma directa. En Dart, es común usar este estilo en scripts o bloques específicos donde el control del flujo es fundamental.

**Ejemplo (Dart):**
```dart
void main() {
  final numeros = [1, 2, 3, 4];
  int suma = 0;
  for (var n in numeros) {
    suma += n;
  }
  print(suma);
}
```

**Explicación:** Se inicializa una variable y se suma cada elemento mediante un bucle `for`.

---

## 4. Paradigma Declarativo

- **Descripción:** Enfocado en *qué* se quiere lograr más que *cómo*. Dart lo permite en parte con colecciones y UI declarativa (Flutter).
- **Usos:** Declaración de UI, reglas, configuraciones.
- **Lenguajes comunes:** Dart (UI con Flutter), SQL, HTML/CSS.

En la programación declarativa, el desarrollador especifica el resultado deseado sin definir el paso a paso para lograrlo. Este paradigma es ampliamente utilizado en el desarrollo de interfaces gráficas, donde los componentes se declaran en lugar de construirse de forma imperativa. Flutter, el framework de UI de Dart, se basa completamente en este enfoque, permitiendo construir interfaces de manera más intuitiva y legible.

**Ejemplo (Flutter - Dart declarativo):**
```dart
import 'package:flutter/material.dart';

void main() => runApp(SumaApp());

class SumaApp extends StatelessWidget {
  final List<int> numeros = [1, 2, 3, 4];

  @override
  Widget build(BuildContext context) {
    final suma = numeros.reduce((a, b) => a + b);

    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Suma Declarativa')),
        body: Center(child: Text('Resultado: $suma')),
      ),
    );
  }
}
```

**Explicación:** Se construye la interfaz visual declarando los widgets que deben mostrarse y su contenido.

---

## 5. Paradigma Reactivo / Orientado a Eventos

- **Descripción:** Responde a flujos de datos y eventos de forma asincrónica y reactiva.
- **Usos:** Interfaces en tiempo real, streams, Flutter con `StreamBuilder` o RxDart.
- **Lenguajes comunes:** Dart (RxDart, Flutter), JavaScript (RxJS), Java (Reactor).

Este paradigma gira en torno a la gestión de eventos y flujos de datos. Los programas reactivos responden de manera eficiente a eventos que ocurren a lo largo del tiempo, como interacciones del usuario o cambios de estado en tiempo real. En Dart, el uso de `Stream` y paquetes como RxDart permiten construir aplicaciones altamente interactivas y con buena capacidad de respuesta, ideales para Flutter y entornos móviles.

**Ejemplo (Dart con `Stream`):**
```dart
void main() async {
  final stream = Stream.fromIterable([1, 2, 3, 4]);
  final suma = await stream.reduce((a, b) => a + b);
  print(suma);
}
```

**Explicación:** Se usa un `Stream` para emitir los valores de la lista y `reduce` para sumar los datos cuando estén disponibles.

---

## 💡 Comparación: Suma de una lista

Todos los ejemplos anteriores realizan la misma tarea de sumar los elementos de una lista `[1, 2, 3, 4]`, usando el estilo correspondiente a cada paradigma. Esto demuestra cómo una misma solución puede variar en estructura según el enfoque de programación.

---

## ✅ Conclusión

Dart es un lenguaje moderno y flexible que permite usar varios paradigmas: desde el orientado a objetos (por defecto), hasta el funcional, declarativo y reactivo, especialmente en combinación con Flutter.
