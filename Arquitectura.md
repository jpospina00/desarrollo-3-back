# Documento de Arquitectura del Sistema de Gestión de Órdenes y Entregas

## 1. Introducción  
Este documento describe la arquitectura inicial del sistema de gestión de órdenes y entregas, incluyendo requisitos funcionales, requisitos de calidad y restricciones clave que deben ser consideradas en el diseño del software.

**Equipo:** _[Pendiente]_  
**Integrantes:**
| Nombre Completo           | Número de Identificación |
|---------------------------|--------------------------|
| Diana Oviedo              | 2459375                  |
| Juan Pablo Ospina         | 2411023                  |
| Kevin Steven Ramirez      | 2259371                  |
| Juan Manuel Hoyos         | 2380796                  |
| Sebastian Cifuentes Florez| 2380764                  |
| Christian Ruiz Devia      | 2160357                  |

**Fecha:** _20/02/2025_  

---

## 2. Requisitos Funcionales  
Los requisitos funcionales se presentan en forma de **historias de usuario**, especificando los **criterios de aceptación**.

### **Historias de Usuario**
| **ID**    | **Historia de Usuario**                                                                                                           | **Criterios de Aceptación**                                                                                                                                                                                                                                                                                            |
| --------- | --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **US-01** | Como cliente registrado, quiero iniciar sesión en la plataforma para acceder a mi historial de pedidos y realizar nuevas compras. | - El usuario debe ingresar un correo y contraseña válidos.<br>- Si las credenciales son correctas, el usuario es redirigido a su perfil.<br>- Si las credenciales son incorrectas, se muestra un mensaje de error sin revelar detalles específicos.<br>- El usuario puede solicitar un restablecimiento de contraseña. |
| **US-02** | _[Agregar historia de usuario]_                                                                                                   | _[Agregar criterios de aceptación]_                                                                                                                                                                                                                                                                                    |
| **US-03** | _[Agregar historia de usuario]_                                                                                                   | _[Agregar criterios de aceptación]_                                                                                                                                                                                                                                                                                    |

>  **Instrucciones:**  
> - Completar al menos **tres historias de usuario**.  
> - Asegurar que cada historia tenga criterios de aceptación claros y verificables.  

---

## 3. Requisitos de Calidad  
Los requisitos de calidad se presentan en forma de **historias de calidad**, siguiendo la estructura de Len Bass.

### **Historias de Calidad**
| **ID**   | **Fuente** | **Estímulo** | **Artefactos** | **Entorno** | **Respuesta** | **Medida de Respuesta** |
|----------|-----------|-------------|---------------|------------|-------------|-----------------|  
| **RQ-01** | Cliente | Se solicita consultar en tiempo real el estado de las órdenes de compra | Modulo de logistica | El servicio esta caído | El sistema deberá recuperarse de manera autonoma | El esfuerzo requerido no debe superar 3 segundos para la recuperación del servicio, y el sistema debe notificar al administrador si el servicio falla más de 3 veces en un período de 30 minutos. |
| **RQ-02** | Cliente | Se solicita que los datos del cliente esten cifrados | Modulo de autenticación | El token jwt este visible | El sistema deberá asegurar que el token JWT no sea accesible después de su expiración, y si un usuario intenta acceder tras el tiempo de expiración, se debe requerir reautenticación. | El token no deberá ser accesible tras haber pasado 24 horas desde que se generó y el sistema debe invalidarlo inmediatamente una vez que haya expirado. |
| **RQ-03** | Cliente | Se solicita que el tiempo de respuesta de cada consulta sea optimo | Sistema | El sistema se queda consultando por mas de 3 segundos la información | El sistema deberá optimizar los tiempos de respuesta para garantizar que ninguna consulta tarde más de 3 segundos. En caso de que una consulta exceda este tiempo, el sistema debe proporcionar un mensaje de error adecuado o intentar de nuevo. | El tiempo de respuesta no debe superar los 3 segundos en consultas estándar. |

---

## 4. Restricciones del Sistema  
Las restricciones establecen **limitaciones** en la arquitectura del sistema, ya sean tecnológicas, de negocio, regulatorias o de infraestructura.

### **Lista de Restricciones**
| **Tipo de Restricción** | **Descripción** |
|------------------------|----------------|
| Tecnológica | El sistema debe desarrollarse utilizando **Spring Boot y PostgreSQL**, debido a la infraestructura actual de la empresa y su compatibilidad con otros sistemas internos. |
| _[Agregar otro tipo]_ | _[Describir la restricción]_ |

>  **Tipos de restricciones:**  
> - **Tecnológicas:** Lenguajes, frameworks o herramientas que deben utilizarse.  
> - **De negocio:** Normativas o estándares de la empresa.  
> - **Regulatorias:** Cumplimiento de normativas legales o de seguridad.  
> - **De infraestructura:** Limitaciones en hardware, red o almacenamiento.  

---

## 5. Formato de Entrega  
- **Formato:** Markdown (`.md`) en el repositorio de Codelabs, El documento debe llamarse `Arquitectura.md`.  
- **Extensión máxima:** 3 páginas.  

---

## **Tiempo estimado para completar el ejercicio: 50 minutos**  
**15 min** → Definir **3 historias de usuario con criterios de aceptación**.  
**15 min** → Definir **3 historias de calidad alineadas con atributos clave**.  
**10 min** → Identificar **2 restricciones relevantes**.  
**10 min** → Revisión y ajustes finales del documento.  
