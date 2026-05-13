# 📍 Microservicio de Geolocalización - Sistema de Gestión de Mascotas

Este repositorio contiene el microservicio de **Geolocalización**, desarrollado con Spring Boot. Su responsabilidad dentro del ecosistema es procesar, almacenar y calcular las coordenadas geográficas relacionadas con las mascotas (por ejemplo, dónde se perdió o dónde fue avistada), facilitando las búsquedas por proximidad.

## 🚀 Arquitectura y Prácticas DevOps

Como servicio especializado, está diseñado para ser consumido por otros microservicios (como el motor de coincidencias) o a través del BFF. Su despliegue y actualización son completamente independientes del resto de la plataforma.

La automatización de su ciclo de vida se realiza mediante un pipeline de **CI/CD con GitHub Actions**:
1. Compila el código fuente en Java y ejecuta las pruebas de integridad.
2. Construye una imagen Docker empaquetando la aplicación.
3. Publica de forma segura la imagen en **Amazon Elastic Container Registry (ECR)**.
4. Despliega la aplicación en la instancia **EC2** correspondiente (Nodo Back 3) mediante **AWS Systems Manager (SSM)**, evitando exponer accesos SSH.
5. Inyecta dinámicamente las variables de entorno necesarias (conexión a DB, Service Discovery, IP privada) durante el arranque del contenedor.

### 🌐 Ecosistema de Infraestructura en AWS
Este microservicio está alojado en el tercer nodo de procesamiento del backend, compartiendo recursos con el sistema de notificaciones:

* **Nodo Web:** ApiGateway y Frontend
* **Nodo Back 1:** Eureka Server y BFF
* **Nodo Back 2:** Microservicios de Mascotas y Usuarios
* **Nodo Back 3:** **Microservicio de Geolocalización** (Este repositorio) 📍 y Notificaciones
* **Nodo Back 4:** Motor de Coincidencias
* **Base de Datos:** SanosDB (PostgreSQL)

## 🛠️ Tecnologías Principales

* **Framework:** Java 17 / Spring Boot 3
* **Persistencia:** Spring Data JPA / Hibernate (Soporte GIS si aplica)
* **Cloud Native:** Spring Cloud Netflix Eureka Client
* **Contenedores:** Docker
* **CI/CD:** GitHub Actions
* **Infraestructura AWS:** EC2, ECR, SSM, IAM

## ⚙️ Descubrimiento y Redes

* **Aislamiento de Red:** Todo el procesamiento espacial y las consultas a la base de datos ocurren estrictamente dentro de la VPC privada de AWS.
* **Auto-Registro (Eureka):** Al iniciar, el contenedor utiliza la metadata de EC2 para obtener su IP local y se registra dinámicamente en el servidor Eureka (ej. `MS-GEOLOCALIZACION`). Esto permite que el API Gateway, el BFF y el Motor de Coincidencias se comuniquen con él de forma resiliente y sin dependencias de IPs fijas.

## 📦 Repositorios del Proyecto

Explora el resto de la infraestructura y microservicios de este ecosistema:

**Frontend y Puertas de Enlace**
* 🌐 [Frontend_eft_fullstack_III](https://github.com/NBello26/Frontend_eft_fullstack_III)
* 🚪 [ApiGateway_eft_fullstack_III](https://github.com/NBello26/ApiGateway_eft_fullstack_III)
* 🌉 [BFF_eft_fullstack_III](https://github.com/NBello26/BFF_eft_fullstack_III)

**Descubrimiento y Base de Datos**
* 🧭 [Eureka_eft_fullstack_III](https://github.com/NBello26/Eureka_eft_fullstack_III)
* 🗄️ [BD_eft_fullstack_III](https://github.com/NBello26/BD_eft_fullstack_III)

**Microservicios de Negocio**
* 🐾 [Reporte_Mascota_eft_fullstack_III](https://github.com/NBello26/Reporte_Mascota_eft_fullstack_III)
* 👤 [Usuarios_eft_fullstack_III](https://github.com/NBello26/Usuarios_eft_fullstack_III)
* 📍 [Geolocalizacion_eft_fullstack_III](https://github.com/NBello26/Geolocalizacion_eft_fullstack_III) *(Estás aquí)*
* 🔔 [Notificaciones_eft_fullstack_III](https://github.com/NBello26/Notificaciones_eft_fullstack_III)
* 🧩 [Coincidencias_eft_fullstack_III](https://github.com/NBello26/Coincidencias_eft_fullstack_III)

---
*Desarrollado como parte del proyecto final de integración de arquitectura DevOps.*
