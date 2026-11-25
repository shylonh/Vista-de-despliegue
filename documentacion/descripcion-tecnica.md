# Descripción técnica de la vista de despliegue

**Proyecto:** UAM LINK · **Presentación individual:** Shylon Emeil Andrews Hunter

## 1. Propósito y alcance

El modelo explica dónde se ejecuta cada parte de UAM LINK y cómo se comunica con las demás. El sistema vincula pacientes con prácticas supervisadas de Odontología, Psicología, Nutrición y Medicina; permite solicitar atención, organizar citas y consultar actividad académica.

Se incluyen dos vistas: **arquitectura objetivo propuesta** y **prototipo actual**. La primera corresponde al sistema completo previsto en la matriz de viabilidad. La segunda documenta lo comprobado en los HTML. Una propuesta arquitectónica no demuestra que los servicios estén implementados o desplegados.

## 2. Nodos y entornos de la arquitectura objetivo

| Nodo | Tipo UML y entorno | Responsabilidad y justificación |
|---|---|---|
| Dispositivo del usuario | `«device»`; `«executionEnvironment» Navegador web` | Computadora o teléfono de pacientes, recepción, estudiantes, docentes y coordinación. Presenta la interfaz responsiva y ejecuta JavaScript. El navegador no accede directamente a MySQL. |
| Servidor de aplicación | `«device»`; `«executionEnvironment» Node.js + servidor HTTPS` | Equipo o máquina virtual de alojamiento. Sirve HTML/CSS/JS y ejecuta la API. Centraliza reglas, autorización y operaciones de citas para evitar que cada cliente mantenga información aislada. Node.js es una elección propuesta para reutilizar JavaScript; no figura como backend ya existente. |
| Servidor de datos | `«device»`; `«executionEnvironment» MySQL` | Equipo o máquina virtual en la red privada del alojamiento. Mantiene usuarios, pacientes, servicios, disponibilidad, solicitudes, citas, atenciones y validaciones. MySQL es una opción citada en la viabilidad técnica y se adopta como propuesta concreta. |
| Servidor de correo | `«device»`; `«executionEnvironment» Servicio SMTP` | Infraestructura externa del proveedor de correo. Recibe mensajes de confirmación, reprogramación o cancelación. Se separa para no asumir que el servidor web entrega correo directamente. |

Los nodos de servidor representan funciones desplegadas en equipos o máquinas virtuales. No se afirma que existan cuatro máquinas físicas disponibles en la UAM. Su proveedor, capacidad, sistema operativo y dominio deben concretarse durante la implementación.

## 3. Componentes de software

| Ubicación | Componente | Función |
|---|---|---|
| Navegador | Interfaz UAM LINK | Formulario del paciente, agenda, comprobantes, consultas y reportes. |
| Node.js | API UAM LINK | Coordina las solicitudes de la interfaz y aplica autorización y validaciones del servidor. |
| Node.js | Usuarios y permisos | Autenticación y permisos según paciente, recepción, estudiante, docente o coordinación. Previsto; los selectores de rol actuales son una simulación. |
| Node.js | Solicitudes y citas | Registra preferencias, verifica disponibilidad y gestiona asignación, confirmación, reprogramación y cancelación. Una fecha preferida no confirma una cita. |
| Node.js | Atenciones y validaciones | Registra atenciones y evidencias y permite validación docente. Las horas pendientes no cuentan como aprobadas. |
| Node.js | Consultas y reportes | Genera agenda, comprobantes, indicadores y actividad académica respetando el alcance del usuario. |
| Node.js | Notificaciones | Solicita envíos de avisos al servicio SMTP después de los cambios correspondientes. |
| MySQL | Persistencia UAM LINK | Conserva los registros relacionados y soporta integridad referencial y transacciones. |

En el diagrama principal se agrupan los módulos de negocio dentro del componente API para conservar legibilidad. Sus responsabilidades se enumeran en la nota técnica del modelo.

## 4. Artefactos

| Artefacto UML | Despliegue | Estado |
|---|---|---|
| `uam-link-web.zip` | En el servidor de aplicación; su HTML/CSS/JS se carga en el navegador | Paquete previsto de distribución de la interfaz. Los HTML independientes sí existen; el paquete unificado aún no. |
| `uam-link-api.zip` | Entorno Node.js | Unidad prevista con código del backend y dependencias declaradas. No implementada en el ZIP recibido. |
| `uam-link-schema.sql` | MySQL | Script previsto para crear y migrar el esquema. El proyecto tiene diseño de datos, pero este script no fue aportado. |
| `UAM-LINK-entrada.html` | Navegador local, vista actual | Archivo real: formulario de solicitud en cuatro pasos. |
| `UAM-LINK.html` | Navegador local, vista actual | Archivo real: consultas, agenda y reportes con ejemplos. |

Un componente describe una responsabilidad lógica del software; un artefacto es una unidad física que se distribuye. La dependencia `«manifest»` va del artefacto al componente que materializa. Los artefactos están anidados en el entorno donde se despliegan. El artefacto web del servidor tiene una dependencia `«manifest»` hacia la interfaz ejecutada en el navegador, donde se carga su contenido.

## 5. Comunicaciones

| Origen y destino | Mecanismo | Datos y justificación |
|---|---|---|
| Navegador - aplicación | HTTPS, TCP 443 | Descarga de HTML/CSS/JS y consumo de API; peticiones y respuestas JSON. TLS protege el tránsito y autentica el servidor mediante su certificado. |
| Aplicación - MySQL | Protocolo MySQL, TCP 3306, TLS; red privada | Consultas, transacciones y resultados. Acceso restringido al servidor de aplicación. La protección TLS debe configurarse; el puerto por sí solo no la garantiza. |
| Aplicación - correo | SMTP, TCP 587, STARTTLS | Envío autenticado de avisos. El servicio SMTP debe soportar y exigir la actualización TLS. |
| Navegador - archivos locales (vista actual) | Lectura local, URL `file://` | No existe intercambio de datos entre los dos HTML. Las descargas CSV/HTML y la impresión/PDF se producen en el cliente. |

Las líneas continuas entre nodos son caminos de comunicación UML; las flechas discontinuas `«manifest»` relacionan artefactos con componentes. Las dependencias de software se dibujan discontinuas y no sustituyen los caminos físicos de comunicación.

GitHub conserva el código, el modelo y la documentación. No participa en las consultas de pacientes de la arquitectura objetivo y por ello no se mezcla con sus nodos de operación. El repositorio no equivale a un hosting de API o de MySQL.

## 6. Flujo de ejemplo

1. El paciente completa una solicitud en el navegador.
2. La interfaz envía los datos a la API por HTTPS.
3. La API valida campos y autorización y guarda la solicitud en MySQL.
4. Recepción o coordinación revisa disponibilidad y asigna la cita; la preferencia del paciente no se convierte automáticamente en confirmación.
5. Tras confirmar, la API persiste el cambio y solicita el aviso al servicio SMTP.
6. El personal registra la atención y el docente valida la actividad. Los reportes distinguen horas registradas, validadas y pendientes.

Este flujo describe la operación objetivo. En el prototipo actual completar el formulario no añade una cita a la pantalla de salidas.

## 7. Coherencia y decisiones

- La interfaz web corresponde a los HTML responsivos existentes y a VT-03 y VT-09.
- El servidor/API responde al alojamiento contemplado en VT-05. El proveedor de ejemplo no se representa como contratado.
- La base relacional responde a VT-04. Un motor central evita que cada usuario mantenga citas distintas.
- SMTP responde a VT-06; HTTPS a VT-07. Ambos son objetivos de implementación.
- GitHub corresponde al control de versiones de VT-08.
- Usuarios, solicitudes, citas, atención, validación y reportes se derivan de la documentación UAM LINK; no se incluyen módulos de matrícula o QualityTrack.
- El backend controla accesos: ocultar elementos de la interfaz o cambiar el rol visual no constituye autorización.
- Separar datos y aplicación facilita restringir el acceso a MySQL y gestionar respaldos. La arquitectura no afirma alta disponibilidad ni redundancia.

## 8. Validación y límites

Se comprobaron los archivos HTML y la matriz de viabilidad del ZIP. Se verificaron elementos, tipos, relaciones y referencias del proyecto FEAP y se generaron PDF/PNG a partir de la misma definición de arquitectura. La apertura y apariencia final en Enterprise Architect 15 deben revisarse en la instalación del estudiante; las imágenes exportadas fueron generadas programáticamente y no se presentan como una exportación ejecutada desde EA.

No se realizaron pruebas de un backend, servidor MySQL, SMTP ni infraestructura operativa, porque esos servicios no están implementados en el material recibido. El modelo no acredita aprobación institucional, gestión de expedientes clínicos ni funcionamiento real con pacientes.

## 9. Fuentes del proyecto

- `fuentes/Documento-UAM-LINK.md`: propósito, actores, entradas, salidas, cobertura y limitaciones del prototipo.
- `fuentes/Viabilidad-Tecnica.xlsx`: VT-01 a VT-10.
- `prototipo/entradas/UAM-LINK-entrada.html` y `prototipo/salidas/UAM-LINK.html`: artefactos disponibles.
