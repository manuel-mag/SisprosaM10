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

