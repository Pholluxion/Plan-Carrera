## Antipatrones de Diseño

Los antipatrones son prácticas comunes pero erróneas en el desarrollo de software. A continuación se listan los más relevantes:

### 1. Clase Anémica

**Descripción:** Clases que solo contienen atributos con métodos getters y setters, sin ninguna lógica de negocio.

**Problema:** Viola el principio de encapsulamiento y delega la lógica a otras clases externas.

**Ejemplo:**

```java
public class Usuario {
    private String nombre;
    private String correo;

    public String getNombre() { return nombre; }
    public void setNombre(String nombre) { this.nombre = nombre; }
    public String getCorreo() { return correo; }
    public void setCorreo(String correo) { this.correo = correo; }
}
```

**Solución:** Agregar lógica relacionada directamente dentro de la clase.

```java
public class Usuario {
    private String nombre;
    private String correo;

    public Usuario(String nombre, String correo) {
        this.nombre = nombre;
        this.correo = correo;
    }

    public void enviarCorreoBienvenida() {
        // lógica para enviar correo
    }
}
```

---

### 2. Objeto Dios (God Object)

**Descripción:** Clases que centralizan demasiadas responsabilidades o manejan múltiples dominios de la aplicación.

**Problema:** Dificultan la comprensión, el mantenimiento y el testeo.

**Solución:** Aplicar el principio de responsabilidad única y dividir en clases especializadas.

---

### 3. Código Espagueti (Spaghetti Code)

**Descripción:** Código desorganizado, sin estructura clara, con múltiples dependencias entre componentes.

**Problema:** Se vuelve inentendible, difícil de modificar y propenso a errores.

**Solución:** Aplicar patrones de diseño y principios SOLID. Modularizar y estructurar el código.

---

### 4. Repetición de Código (Code Duplication)

**Descripción:** Copiar y pegar código en múltiples lugares en lugar de abstraerlo.

**Problema:** Dificulta el mantenimiento, aumenta el riesgo de errores en cambios.

**Solución:** Extraer funciones reutilizables o crear componentes comunes.

---

### 5. Valores Quemados (Hardcoded Values)

**Descripción:** Incluir valores fijos directamente en el código.

**Problema:** Reduce la flexibilidad, dificulta la modificación y la configuración.

**Solución:** Utilizar constantes, archivos de configuración o parámetros.

---

### 6. Acoplamiento Fuerte (Tight Coupling)

**Descripción:** Las clases están altamente dependientes entre sí.

**Problema:** Las modificaciones en una clase afectan directamente a otras.

**Solución:** Introducir interfaces, inversión de dependencias e inyección de dependencias.

---

### 7. Controladores Gruesos (Fat Controller)

**Descripción:** Controladores (en arquitecturas MVC) que incluyen lógica de negocio en lugar de delegarla.

**Problema:** Rompen la separación de responsabilidades.

**Solución:** Extraer la lógica a servicios o clases del dominio.

---

### 8. Números y Cadenas Mágicas (Magic Numbers / Magic Strings)

**Descripción:** Uso de números o cadenas sin contexto ni explicación.

**Problema:** Dificulta la comprensión del código y lo hace más propenso a errores.

**Solución:** Declarar constantes con nombres significativos.

---

### 9. Sobreingeniería (Overengineering)

**Descripción:** Crear soluciones excesivamente complejas para problemas simples.

**Problema:** Aumenta el costo de desarrollo y mantenimiento sin beneficios reales.

**Solución:** Aplicar el principio KISS (Keep It Simple, Stupid) y evitar anticiparse a problemas que no existen.

---

### 10. Programación por Copia (Copy-Paste Programming)

**Descripción:** Copiar soluciones existentes sin adaptar ni abstraer.

**Problema:** Genera duplicación de lógica y errores difíciles de rastrear.

**Solución:** Entender el código copiado, abstraerlo y reutilizar componentes correctamente.
