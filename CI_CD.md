### **CI/CD – Integración Continua y Despliegue Continuo**

**CI/CD** es un conjunto de prácticas de desarrollo de software que automatiza las etapas de construcción, prueba y despliegue de aplicaciones. Su objetivo es entregar software de forma **más rápida, segura y confiable**.

---

### **CI – (Continuous Integration)**

* Los desarrolladores integran cambios de código frecuentemente (varias veces al día) en un repositorio compartido.
* Cada cambio dispara un **proceso automático de compilación y pruebas**.
* Beneficios:

  * Detecta errores rápidamente.
  * Mejora la calidad del código.
  * Reduce conflictos al integrar código.

---

### **CD - (Continuous Delivery / Deployment)**

* **Entrega Continua (Continuous Delivery):**

  * El software pasa automáticamente por pruebas y queda **listo para ser desplegado** manualmente.
  * Se usa cuando se quiere mantener control sobre cuándo liberar.

* **Despliegue Continuo (Continuous Deployment):**

  * El software se **despliega automáticamente a producción** tras pasar las pruebas.
  * Ideal para productos que requieren actualizaciones frecuentes.

---

### ✅ **Ventajas de CI/CD**

* Reducción de errores en producción.
* Feedback más rápido para desarrolladores.
* Menor tiempo entre desarrollo y entrega.
* Mejora en la colaboración del equipo.

---

# Flujo de CI/CD con Azure DevOps

Este escenario describe el flujo de datos a través de un proceso completo de CI/CD utilizando Azure DevOps.

---

## 🧪 Pipeline de Pull Request (PR)

Una **pull request (PR)** en Azure Repos Git activa un pipeline de PR. Este pipeline realiza verificaciones rápidas de calidad, incluyendo:

- Compilación del código (requiere obtener dependencias de un sistema de gestión de dependencias).
- Análisis del código con herramientas como:
  - Análisis estático de código
  - Linting
  - Escaneo de seguridad
- Pruebas unitarias

📌 **Si alguna verificación falla**, el pipeline termina y el desarrollador debe realizar los cambios necesarios.

📌 **Si todas las verificaciones pasan**, se solicita una **revisión de PR**.  
- Si la revisión falla, el pipeline termina y el desarrollador debe corregir.
- Si la revisión y las verificaciones pasan, la PR se fusiona correctamente.

---

## 🔁 Pipeline de Integración Continua (CI)

Una **fusión al repositorio** en Azure Repos Git activa un pipeline de CI.  
Este pipeline ejecuta las mismas verificaciones que el pipeline de PR **con adiciones importantes**:

- Ejecuta pruebas de integración.
  - Estas pruebas pueden ser costosas en recursos.
  - Son ideales para detectar errores que no se descubren en el pipeline de PR.
  - Ayudan a asegurar que los cambios no rompan el código después de la fusión.

⚠️ **Nota:** Las pruebas exitosas en la PR no garantizan que también pasen después de hacer merge, debido a posibles cambios en la rama principal.

🔐 Si las pruebas requieren secretos, estos se obtienen desde **Azure Key Vault**.

📌 Si todo pasa correctamente, se crean y publican **artefactos de compilación**.

---

## 🚀 Disparador del Pipeline de CD

La publicación de artefactos en el pipeline de CI activa el pipeline de CD.

---

## 🧪 Lanzamiento CD a Staging

El pipeline de CD:

1. Descarga los artefactos de compilación del pipeline de CI.
2. Despliega la solución en un entorno **staging**.
3. Ejecuta pruebas de aceptación para validar el despliegue.

📌 Si alguna prueba falla, el pipeline termina y el desarrollador debe corregir.

✅ Si las pruebas pasan, se puede requerir una **validación manual** por una persona o grupo antes de continuar.

---

## 🚢 Lanzamiento CD a Producción

Si la intervención manual continúa (o no se requiere), el pipeline:

1. Despliega la solución en **producción**.
2. Ejecuta **pruebas de humo** (smoke tests) para verificar que el sistema funciona como se espera.

📌 Si la intervención manual se cancela, las pruebas de humo fallan o hay errores, el despliegue:
- Se revierte (rollback),
- El pipeline termina,
- Y el desarrollador debe hacer los cambios necesarios.

---

## 📈 Monitoreo

- **Azure Monitor** recopila datos observables como logs y métricas para analizar salud, rendimiento y uso.
- **Application Insights** recoge datos específicos de la aplicación, como trazas.
- **Azure Log Analytics** se utiliza para almacenar todos estos datos.

---

## 🖼️ Diagrama de Arquitectura CI/CD

![Arquitectura CI/CD de Azure DevOps](https://learn.microsoft.com/en-us/azure/devops/pipelines/architectures/media/azure-devops-ci-cd-architecture.svg?view=azure-devops)
