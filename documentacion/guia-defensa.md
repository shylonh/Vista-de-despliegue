# Guía para la defensa individual

**Estudiante:** Shylon Emeil Andrews Hunter · **Proyecto:** UAM LINK

## Exposición sugerida: 3 a 4 minutos

Mi proyecto es UAM LINK. Su propósito es organizar solicitudes de pacientes, citas y actividad de prácticas supervisadas en las carreras de salud de la UAM. Los usuarios son pacientes, recepción, estudiantes, docentes y coordinación.

El diagrama principal representa la arquitectura objetivo propuesta. La documentación contempla una aplicación web, una base relacional, alojamiento y correo. Actualmente contamos con prototipos HTML que trabajan con datos ficticios, por eso también presento un diagrama del estado actual.

En el primer nodo está el dispositivo del usuario: una computadora o teléfono. Dentro se encuentra el navegador, que es el entorno de ejecución de la interfaz. El navegador presenta el formulario, la agenda y los reportes.

El segundo nodo es el servidor de aplicación. Propongo Node.js para ejecutar la API y servir la interfaz por HTTPS. La API centraliza usuarios y permisos, solicitudes y citas, atenciones, validaciones docentes, consultas y notificaciones. El cliente no debe decidir por sí solo si una persona puede consultar datos de otro paciente.

El tercer nodo contiene MySQL. Allí se almacenan los usuarios, pacientes, servicios, disponibilidad, citas y actividad académica. La API se conecta al motor por la red privada. El navegador no conoce las credenciales ni consulta la base directamente.

El cuarto nodo es el servidor SMTP para los avisos de confirmación, reprogramación y cancelación. La API solicita el envío y el proveedor de correo se encarga de entregarlo.

Las conexiones son HTTPS por el puerto 443, protocolo MySQL por 3306 con TLS configurado y SMTP por 587 con STARTTLS. Las líneas continuas representan caminos de comunicación. Los archivos ZIP y SQL son artefactos previstos de despliegue; las flechas manifest indican qué componente materializan.

La vista actual muestra un solo dispositivo con el navegador y los dos HTML reales. No hay una base de datos conectada ni comunicación entre esas pantallas. Mi propuesta describe la infraestructura necesaria para pasar de esa demostración al sistema completo. GitHub conserva esta entrega y su historial.

## Preguntas probables

| Pregunta | Respuesta |
|---|---|
| ¿Qué diferencia hay entre nodo, entorno y componente? | El nodo aloja software; el dispositivo representa el equipo o VM. El entorno, como el navegador o Node.js, permite ejecutarlo. El componente representa una responsabilidad del software, como gestionar citas. |
| ¿Qué es un artefacto? | Un archivo o paquete físico que se distribuye, por ejemplo el HTML actual o el paquete previsto de la API. |
| ¿Por qué dos diagramas? | Para distinguir el prototipo realmente disponible de la arquitectura necesaria para el sistema completo. |
| ¿Ya funciona el backend? | No. Los HTML son prototipos independientes. Node.js, MySQL y SMTP son parte de la propuesta, fundamentada en la viabilidad técnica. |
| ¿Por qué Node.js? | Es una propuesta para mantener JavaScript en el cliente y el servidor. La documentación pide una API, pero no fija ese runtime. |
| ¿Por qué MySQL? | Se necesita persistencia relacional y la matriz de viabilidad lo menciona como ejemplo. Aquí se concreta como opción propuesta. |
| ¿Puede el navegador conectarse a MySQL? | La arquitectura prevista hace que acceda a la API. La API valida permisos y consulta la base sin entregar sus credenciales al navegador. |
| ¿Una fecha solicitada equivale a cita confirmada? | No. Recepción o coordinación debe revisar disponibilidad y asignación antes de confirmar. |
| ¿Las horas registradas son horas aprobadas? | No. Requieren validación docente. Los reportes deben separar registradas, validadas y pendientes. |
| ¿Dónde se despliegan los artefactos? | La interfaz y el backend en el servidor de aplicación; el esquema SQL se aplica en MySQL. El contenido de la interfaz se carga y ejecuta en el navegador. |
| ¿Por qué SMTP es otro nodo? | Representa infraestructura de un proveedor que recibe los avisos enviados por la API. No es una función del navegador. |
| ¿El puerto 3306 garantiza cifrado? | No. TLS y la validación de certificados deben configurarse. El puerto identifica el servicio, no prueba su seguridad. |
| ¿Qué pasa si falla el correo? | La cita debe conservar su estado en la base. La implementación debe gestionar errores y reintentos de envío; eso todavía no está programado. |
| ¿GitHub ejecuta todo el sistema? | Guarda los archivos y sus versiones. El repositorio por sí solo no ejecuta la API ni MySQL. |
| ¿Necesitamos cuatro equipos físicos? | El diagrama separa responsabilidades en nodos de despliegue. Los servidores pueden ser máquinas virtuales; su contratación y dimensionamiento quedan pendientes. |
| ¿Es una arquitectura de alta disponibilidad? | No. No se han previsto réplicas ni balanceadores en este modelo. |
| ¿Qué falta implementar? | Integración de pantallas, API, autenticación y permisos, persistencia, operaciones administrativas, validación docente, correo y configuración de infraestructura. |

## Antes de presentar

1. Descargar el `.feap` con el botón **Raw/Download raw file** de GitHub.
2. Abrirlo en EA 15 y localizar los dos diagramas del paquete de despliegue.
3. Revisar que las cajas, conexiones y etiquetas sean visibles.
4. Tener a mano el PDF y los HTML como apoyo.
5. Explicar siempre cuáles elementos son actuales y cuáles son propuestos.
