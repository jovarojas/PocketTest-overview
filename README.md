# 🎓 PocketTest: Ecosistema Educativo Inteligente

> Plataforma de evaluación académica respaldada por una API RESTful robusta que analiza el rendimiento del alumno y automatiza la generación de repasos personalizados.

[![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white)](https://www.java.com/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-F2F4F9?style=for-the-badge&logo=spring-boot)](https://spring.io/projects/spring-boot)
[![MySQL](https://img.shields.io/badge/MySQL-00000F?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Angular](https://img.shields.io/badge/Angular-DD0031?style=for-the-badge&logo=angular&logoColor=white)](https://angular.io/)
[![Kotlin](https://img.shields.io/badge/Kotlin-0095D5?style=for-the-badge&logo=kotlin&logoColor=white)](https://kotlinlang.org/)

---

## 📺 Demostración de funcionamiento

<div align="center">
  <video src="./pocketTest_demo.mp4" width="650" autoplay loop muted playsinline></video>
</div>

---

## ⚙️ Arquitectura central y Backend

El núcleo de PocketTest es una **API RESTful** estructurada en **Java 17** con **Spring Boot**. El diseño lógico se ha implementado siguiendo minuciosamente las directrices de **Clean Code y los principios SOLID**, garantizando un software con alta cohesión, desacoplado y completamente mantenible.

### 🔐 Seguridad y control de acceso
* **Spring Security:** Configuración e implementación nativa en el servidor para el blindaje absoluto de los endpoints de la API.
* **Autenticación Stateless (JWT):** Control de sesiones y transmisiones de datos seguras sin estado mediante tokens cifrados firmados con algoritmos HMAC-SHA.
* **Control de Acceso Basado en Roles (RBAC):** Filtros personalizados para la restricción rigurosa de rutas según el perfil de usuario autenticado (**Administrador, Profesor o Alumno**).

### 🗄️ Modelado y persistencia de datos
* **MySQL:** Base de datos relacional normalizada y estructurada para mantener la trazabilidad completa del flujo académico (`users`, `classrooms`, `exams`, `questions`, `options`, `attempts`).
* **Manejo eficiente de relaciones N:M:** Modelado de la entidad intermedia `exam_questions` utilizando JPA/Hibernate para personalizar de forma dinámica el peso y el orden de los reactivos dentro de cada examen.

### 🧠 Algoritmo de repaso inteligente
Toda la lógica de negocio pesada reside de manera exclusiva en el servidor, mitigando vulnerabilidades en el cliente. Cuando un alumno solicita generar un repaso de refuerzo, el backend:
1. Rastrea el histórico de ejecuciones en la base de datos filtrando por el identificador del alumno.
2. Identifica y aísla de forma automática las respuestas erróneas (`is_correct = false`).
3. Instancia y persiste dinámicamente un nuevo objeto de examen de tipo `REVIEW`, dejándolo expuesto únicamente para el perfil del alumno propietario.

---

## 🏗️ Diagrama de arquitectura (Ecosistema)

Este diagrama se renderiza de manera nativa en GitHub mediante **Mermaid.js**, ilustrando el patrón de **"Un cerebro centralizado, múltiples interfaces cliente"**:

```mermaid
graph TD
    subgraph Clientes [Interfaces de Usuario]
        A[💻 Panel Web Profesor<br/><b>Angular</b>]
        B[📱 App Móvil Alumno<br/><b>Kotlin / Android</b>]
    end

    subgraph Servidor [Backend Centralizado]
        C((⚙️ <b>API RESTful</b><br/>Spring Boot / Java))
        D{🛡️ <b>Seguridad</b><br/>Spring Security & JWT}
    end

    subgraph Persistencia [Base de Datos]
        E[(🗄️ <b>Base de Datos</b><br/>MySQL)]
    end

    A <-->|Peticiones HTTP/JSON<br/>Token JWT| D
    B <-->|Peticiones HTTP/JSON<br/>Token JWT| D
    
    D --- C
    
    C <-->|JPA / Hibernate<br/>Consultas SQL| E

    style A fill:#dd0031,stroke:#fff,stroke-width:2px,color:#fff
    style B fill:#0095d5,stroke:#fff,stroke-width:2px,color:#fff
    style C fill:#6db33f,stroke:#fff,stroke-width:2px,color:#fff
    style D fill:#f2f4f9,stroke:#6db33f,stroke-width:2px,color:#333
    style E fill:#00000f,stroke:#fff,stroke-width:2px,color:#fff

```

---

## 📱 Integración de clientes (Frontend)

Para verificar y validar la interoperabilidad de la API REST, el sistema abastece en tiempo real a dos tipos de arquitecturas cliente ligeras:

* **Panel Administrativo Web (Angular):** Single Page Application construida de forma **autodidacta** fuera del currículo oficial del ciclo formativo. Cuenta con internacionalización completa (i18n), protección de navegación mediante *Guards*, manipulación de formularios reactivos dinámicos y paneles analíticos para el seguimiento del rendimiento de las calificaciones de las aulas.
* **Aplicación Móvil Nativa (Kotlin):** Cliente Android enfocado en brindar una experiencia de usuario fluida, optimizado para la ejecución asíncrona de simulacros cronometrados y el consumo directo del API para renderizar las correcciones automáticas.

---

## 👨‍💻 Sobre el desarrollo

Este proyecto ha sido desarrollado en su totalidad por **Jovanna Rojas** como proyecto final integrador de la titulación de Desarrollo de Aplicaciones Multiplataforma (DAM).

El objetivo principal ha sido consolidar conocimientos técnicos avanzados en el **desarrollo Backend corporativo**, demostrando versatilidad técnica y una alta capacidad de autoaprendizaje al integrar frameworks robustos de la industria de producción actual.

---

## 📬 Contacto y redes

Si deseas conocer más detalles técnicos sobre el diseño del sistema o conectar profesionalmente:

* **LinkedIn:** www.linkedin.com/in/jovannarojasm
* **Email:** jovrojmal@outlook.es
