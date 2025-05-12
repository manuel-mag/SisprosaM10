# 🩺 SISPROSA — Sistema de Gestión de Pacientes para Profesionales de Salud

![Java](https://img.shields.io/badge/java-17-blue) 
![Spring Boot](https://img.shields.io/badge/Spring--Boot-3.4.4-green)
![Security](https://img.shields.io/badge/security-JWT-blueviolet)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

SISPROSA es una aplicación web desarrollada para ayudar a los profesionales de la salud a gestionar pacientes, consultas médicas, historial clínico, seguimientos y reportes. El sistema cuenta con control de acceso basado en roles y funciones clave como generación de reportes PDF y envío por correo electrónico.

---

## 📚 Tabla de Contenidos

- [🎯 Objetivo del Proyecto](#-objetivo-del-proyecto)
- [🧱 Estructura del Proyecto](#-estructura-del-proyecto)
- [🧰 Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [⚙️ Configuración del Entorno](#-configuración-del-entorno)
- [🗃 Modelo de Datos](#-modelo-de-datos)
- [🔐 Seguridad y Autenticación](#-seguridad-y-autenticación)
- [🧩 Módulos y Funcionalidades](#-módulos-y-funcionalidades)
- [🧪 Ejemplos de Uso](#-ejemplos-de-uso)
- [📄 Licencia](#-licencia)
- [🤝 Contribuciones](#-contribuciones)

---
## 🎯Objetivo del Proyecto

SISPROSA busca digitalizar y optimizar la gestión clínica de los profesionales de salud. Proporciona un entorno centralizado y seguro para manejar la información médica de manera eficiente y estructurada.

---
## 🧱 Estructura del Proyecto

La aplicación SISPROSA sigue una arquitectura en capas. El backend está dividido en tres grandes dominios: autenticación (`auth`), seguridad (`security`) y lógica del sistema (`system`). A su vez, se complementa con recursos para la vista, configuración y migración de base de datos.

### 🧩 Backend



    auth — Lógica de autenticación y usuarios

        controller

        dto

        model

        repository

        service

    security — Configuración de JWT, logout y filtros

        jwt

        logout

        request

        dto

        service

        SecurityConfiguration.java

    system — Módulos funcionales del sistema

        controller — Pacientes, consultas, historiales, etc.

        dto

        model

        repository

        service

        mapper

        exception

        audit — Auditoría automática con Spring Data

        config.audit — Configuración de auditoría

        utils — PDF, correo, generadores

    SisprosaApplication.java — Punto de entrada principal

### 📂 Recursos

application.properties — Configuración del entorno y base de datos

db/

    schema.sql — Creación de tablas y relaciones

    data.sql — Datos base (usuarios, roles, especialidades)

static/ — Archivos estáticos para frontend

    bootstrap/

    css/

    iconos/

    image/

    js/

    tema/

templates/ — Vistas Thymeleaf organizadas por módulo

    auth/

    consultations/

    dashboard/

    error/

    followups/

    fragments/ — Navbar, footer, layout común

    landing/

    legal/

    medical_history/

    patients/

    professionals/

    specialties/

testdata/ — (opcional) Datos de prueba adicionales

---
## 🧰 Tecnologías Utilizadas

El backend de SISPROSA está construido con el stack moderno de Spring Boot y Java 17, utilizando JWT para autenticación, MariaDB como base de datos y herramientas adicionales para PDF y envío de correos.

| Herramienta / Librería       | Versión                                                             | Descripción                                                                  |
| ---------------------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **Java**                     | 17                                                                  | Lenguaje base del proyecto                                                   |
| **Spring Boot**              | 3.4.4                                                               | Framework principal para el desarrollo del sistema                           |
| **Spring Web**               | `spring-boot-starter-web`                                           | Permite construir controladores REST y servir vistas                         |
| **Spring Data JPA**          | `spring-boot-starter-data-jpa`                                      | Interacción con la base de datos relacional                                  |
| **Spring Security**          | `spring-boot-starter-security`                                      | Seguridad del sistema y control de acceso por roles                          |
| **JWT (JJWT)**               | 0.11.5                                                              | Autenticación basada en tokens JWT (`jjwt-api`, `jjwt-impl`, `jjwt-jackson`) |
| **Spring Validation**        | `spring-boot-starter-validation`                                    | Validación de datos en formularios y DTOs                                    |
| **Thymeleaf + Extras**       | `spring-boot-starter-thymeleaf`, `thymeleaf-extras-springsecurity6` | Motor de plantillas para la UI + integración con Spring Security             |
| **MariaDB**                  | Driver `mariadb-java-client`                                        | Controlador JDBC para la base de datos                                       |
| **OpenPDF**                  | 1.3.30                                                              | Generación de reportes clínicos en formato PDF                               |
| **Spring Mail**              | `spring-boot-starter-mail`                                          | Envío de correos electrónicos con reportes adjuntos                          |
| **Lombok**                   | opcional                                                            | Simplificación de código con anotaciones para getters, setters, etc.         |
| **Spring Boot DevTools**     | (runtime)                                                           | Recarga automática durante el desarrollo                                     |
| **Spring Boot Starter Test** | (test)                                                              | Librerías para pruebas unitarias e integración                               |

---
## ⚙️ Configuración del Entorno

### Requisitos Previos

- Java 17 (Amazon Corretto u OpenJDK)
- Maven 3.8+
- MariaDB 10.6+

### Clonar Proyecto

git clone https://github.com/usuario/sisprosa.git
cd sisprosa

### Inicialización de base de datos

Al ejecutar la aplicación, los archivos `schema.sql` y `data.sql` en `src/main/resources/db/` crearán automáticamente las tablas y registros base (usuarios, roles, especialidades, etc.).

### Ejecución del sistema

cómo levantar el backend:

./mvnw spring-boot:run

O bien:

mvn clean install
java -jar target/Sisprosa-0.0.1-SNAPSHOT.jar


### Acceso al sistema

El sistema quedará disponible en: http://localhost:8080

--- 
## 🗃 Modelo de Datos

SISPROSA utiliza una base de datos relacional MariaDB, siguiendo un diseño normalizado que permite una gestión eficiente de pacientes, consultas, historiales médicos, seguimientos y reportes. Las entidades están relacionadas mediante claves foráneas, y se respetan las reglas de integridad referencial.

### 🔑 Tablas Principales y Relaciones

| Tabla                                 | Descripción                                                                        | Relaciones clave                                        |
| ------------------------------------- | ---------------------------------------------------------------------------------- | ------------------------------------------------------- |
| `patients`                            | Almacena los datos personales y médicos básicos del paciente.                      | Relación 1:1 con `medical_history`                      |
| `medical_history`                     | Registro clínico del paciente: antecedentes, hábitos, alergias, medicamentos, etc. | FK a `patients`, FK a `healthcare_professionals`        |
| `healthcare_professionals`            | Profesionales de salud registrados en el sistema.                                  | Relación N\:M con `specialty`, 1\:N con `consultations` |
| `specialty`                           | Especialidades médicas disponibles (Cardiología, Ginecología, etc.).               | N\:M con `healthcare_professionals`                     |
| `consultations`                       | Consultas realizadas con detalles clínicos, diagnóstico y tratamiento.             | FK a `patients` y `healthcare_professionals`            |
| `followups`                           | Seguimientos posteriores a consultas. Incluye fecha, estado y notas.               | Relación 1:1 con `consultations`                        |
| `authority`                           | Roles de usuario (`ROLE_ADMIN`, `ROLE_PROFESSIONAL`, `ROLE_READONLY`).             | N\:M con `healthcare_professionals`                     |
| `healthcare_professional_authorities` | Tabla intermedia para asignar múltiples roles por profesional.                     |                                                         |
| `professional_patient`                | Relación personalizada para asignar pacientes a profesionales específicos.         | N\:M entre `patients` y `healthcare_professionals`      |

### 🧬 Relaciones Destacadas

    1:1 entre patients y medical_history
    Cada paciente tiene un único historial médico asociado.

    1:N entre patients y consultations
    Un paciente puede tener muchas consultas registradas.

    1:N entre healthcare_professionals y consultations
    Un profesional puede atender múltiples consultas.

    1:1 entre consultations y followups
    Cada consulta puede requerir un único seguimiento registrado.

    N:M entre healthcare_professionals y specialty
    Un profesional puede tener varias especialidades (y viceversa).

    N:M entre healthcare_professionals y authority
    Un profesional puede tener múltiples roles asignados en el sistema.
---

## 🔐 Seguridad y Autenticación

SISPROSA implementa un modelo de seguridad basado en JWT y control de acceso mediante roles personalizados, utilizando Spring Security 6.

## 🔑 Mecanismo de Autenticación
- El sistema utiliza JSON Web Tokens (JWT) para autenticar peticiones HTTP.
- Se emite un token tras el inicio de sesión exitoso vía /auth/login.
- El token debe enviarse en cada petición protegida mediante el header:
    Authorization: Bearer <token>
- Se utiliza JwtFilter para validar el token en cada request.
- Las contraseñas de usuarios se almacenan con BCrypt (11 salt rounds).

## 👥 Roles en el sistema
Los usuarios (healthcare_professionals) pueden tener uno o más roles asignados mediante la tabla intermedia healthcare_professional_authorities.

Roles admitidos:
| Rol                 | Descripción                                          |
| ------------------- | ---------------------------------------------------- |
| `ROLE_ADMIN`        | Acceso completo a todas las secciones                |
| `ROLE_PROFESSIONAL` | Profesionales de salud con privilegios médicos       |
| `ROLE_READONLY`     | Solo lectura para visualizar pacientes e historiales |


## 🧩 Rutas públicas y protegidas

### ✅ Acceso público (no requiere autenticación)

    /auth/** – Registro y autenticación

    /login, /doLogout, /error

    Archivos estáticos: /css/**, /js/**, /images/**, /bootstrap/**, /favicon.ico

### 🔐 Acceso con autenticación

    /dashboard – Requiere sesión iniciada

### 🔒 Rutas protegidas por rol

| Ruta                  | Requiere Rol(es)                    |
| --------------------- | ----------------------------------- |
| `/patients/**`        | `ADMIN`, `PROFESSIONAL`, `READONLY` |
| `/medical_history/**` | `ADMIN`, `PROFESSIONAL`, `READONLY` |
| `/consultations/**`   | `ADMIN`, `PROFESSIONAL`             |
| `/followups/**`       | `ADMIN`, `PROFESSIONAL`             |
| `/professionals/**`   | `ADMIN`                             |
| `/specialties/**`     | `ADMIN`                             |

### 🔁 Flujo de autenticación

1.- Inicio de sesión (POST /auth/login)

    Recibe email y contraseña.

    Devuelve token JWT y datos del usuario.

2.- Acceso a recursos protegidos

    El token debe incluirse en el header Authorization.

3.- Cierre de sesión

    Se realiza vía /doLogout.

    Invalida la sesión y limpia la cookie JSESSIONID.

4.- Manejo de sesiones

    Política: SessionCreationPolicy.IF_REQUIRED

    Soporta sesión en paralelo con cookies y JWT (flujo híbrido listo para expansión).

### 📌 Componentes relevantes

- JwtTokenProvider — Generación y validación de tokens.
- JwtFilter — Valida el token en cada petición.
- AuthenticatedUserService — Recupera el usuario autenticado.
- CustomLogoutSuccessHandler — Comportamiento personalizado al cerrar sesión.
- AuthenticationService — Lógica de login, emisión de tokens y autenticación.

