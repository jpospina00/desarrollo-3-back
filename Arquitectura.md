# Documento de Arquitectura del Sistema de Gestión de Órdenes y Entregas

## 1. Introducción  
Este documento describe la arquitectura inicial del sistema de gestión de órdenes y entregas, incluyendo requisitos funcionales, requisitos de calidad y restricciones clave que deben ser consideradas en el diseño del software.

**Equipo:** 05  
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
| **US-02** | Como administrador, quiero gestionar los pedidos de mis clientes para verificar que se realicen correctamente. | - El administrador debe poder visualizar todos los pedidos en un panel de control.<br>- Debe existir la opción de cambiar el estado de un pedido (Pendiente, En proceso, Enviado, Entregado, Cancelado).<br>- El sistema debe actualizar el estado del pedido en tiempo real.<br>- Se debe enviar una notificación al cliente cuando el estado de su pedido cambie. |
| **US-03** | Como repartidor, quiero ver mi lista de entregas asignadas para organizar mi ruta de trabajo. | - El repartidor debe iniciar sesión con credenciales válidas.<br>- Debe visualizar una lista de entregas pendientes asignadas a su usuario.<br>- La información de cada entrega debe incluir dirección, detalles del cliente y estado del pedido.<br>- Debe poder marcar una entrega como completada, lo que actualizará el estado en el sistema y notificará al cliente. |
| **US-04** | Como administrador, quiero gestionar los usuarios del sistema para controlar el acceso y los permisos. | - El administrador debe poder ver la lista de usuarios registrados.<br>- Debe poder asignar roles (Cliente, Repartidor, Administrador).<br>- Debe poder eliminar cuentas si es necesario. |
| **US-05** | Como cliente, quiero poder registrarme en la plataforma proporcionando mis datos personales, para poder realizar compras. | - El usuario debe ingresar nombre, correo, contraseña y confirmar la contraseña.<br>- Si los datos son válidos, se crea la cuenta y se envía un correo de confirmación.<br>- Si el correo ya está registrado, se muestra un mensaje de error. |
| **US-06** | Como cliente, quiero ver un catálogo de productos con imágenes, descripciones y precios, para elegir qué comprar. | - La interfaz debe mostrar una lista de productos con su imagen, nombre, descripción y precio.<br>- El usuario puede hacer clic en un producto para ver más detalles. |
| **US-07** | Como cliente, quiero poder buscar productos por nombre y aplicar filtros por categoría o precio, para encontrar más rápido lo que necesito. | - El usuario puede ingresar texto en un campo de búsqueda y la lista de productos se filtra en tiempo real.<br>- El usuario puede aplicar filtros por categoría. |
| **US-08** | Como cliente, quiero poder agregar productos a un carrito de compras, para organizar mi pedido antes de pagarlo. | - Cada producto en la tienda tiene un botón para agregar al carrito.<br>- Al agregar un producto, se muestra un mensaje de confirmación.<br>- El usuario puede ver un resumen de los productos en su carrito. |
| **US-09** | Como cliente, quiero poder completar un formulario de compra ingresando mis datos de entrega y método de pago, para finalizar mi compra. | - El usuario debe ingresar su dirección de entrega y seleccionar un método de pago.<br>- Si los datos son correctos, la orden se genera y se muestra un resumen de compra.<br>- Si falta algún dato obligatorio, se muestra un mensaje de error. |
| **US-10** | Como cliente, quiero ver el estado de mis órdenes en tiempo real, para saber cuándo llegará mi compra. | - En la sección "Mis Pedidos", cada orden debe mostrar su estado actual (Pendiente, En proceso, Entregado).<br>- Si la orden está en proceso, se debe actualizar en tiempo real. |
| **US-11** | Como cliente, quiero recibir notificaciones sobre el estado de mi pedido, para estar informado sobre su entrega. | - Se debe mostrar una notificación cuando el pedido cambie de estado.<br>- Las notificaciones pueden ser en la plataforma. |

---

## 3. Requisitos de Calidad  
Los requisitos de calidad se presentan en forma de **historias de calidad**, siguiendo la estructura de Len Bass.

### **Historias de Calidad**
| **ID**   | **Fuente** | **Estímulo** | **Artefactos** | **Entorno** | **Respuesta** | **Medida de Respuesta** |
|----------|-----------|-------------|---------------|------------|-------------|-----------------|  
| **RQ-01** | Cliente | Se solicita consultar en tiempo real el estado de las órdenes de compra | Modulo de logistica | El servicio esta caído | El sistema deberá recuperarse de manera autonoma | El esfuerzo requerido no debe superar 3 segundos para la recuperación del servicio, y el sistema debe notificar al administrador si el servicio falla más de 3 veces en un período de 30 minutos. |
| **RQ-02** | Cliente | Se solicita que las sesiones del cliente sean seguras | Modulo de autenticación | El token jwt este visible | El sistema deberá asegurar que el token JWT no sea accesible después de su expiración, y si un usuario intenta acceder tras el tiempo de expiración, se debe requerir reautenticación. | El token no deberá ser accesible tras haber pasado 24 horas desde que se generó y el sistema debe invalidarlo inmediatamente una vez que haya expirado. |
| **RQ-03** | Cliente | Se solicita que el tiempo de respuesta de cada consulta sea optimo | Sistema | El sistema se queda consultando por mas de 3 segundos la información | El sistema deberá optimizar los tiempos de respuesta para garantizar que ninguna consulta tarde más de 3 segundos. En caso de que una consulta exceda este tiempo, el sistema debe proporcionar un mensaje de error adecuado o intentar de nuevo. | El tiempo de respuesta no debe superar los 3 segundos en consultas estándar. |
| **RQ-04** | Desarrollador | Las contraseñas deben estar encriptadas en la base de datos | Modulo de registro y bases de datos | Las contraseñas estan expuestas en la base de datos | El sistema debe de encriptar todas las contraseñas de forma automatica y con un tipo de hash no vulnerable. | Todas las contraseñas deben estar encriptadas en la base de datos. |

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
