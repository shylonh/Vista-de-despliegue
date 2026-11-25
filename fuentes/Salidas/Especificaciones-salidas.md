# Especificaciones de salidas — UAM LINK

Las cinco salidas presentan consultas y resultados del sistema. Siguiendo los criterios de Kendall y Kendall, cada ficha identifica propósito, destinatario, contenido y medio. Todas se consultan bajo demanda y utilizan datos ficticios.

## SO-01. Agenda de citas

**1. Nombre y objetivo:** Agenda de citas. Consultar la programación y el estado de las citas para organizar la atención y dar seguimiento a los pacientes.

**2. Requerimientos funcionales:** RF-04, programación de citas; RF-05, seguimiento de estados e incidencias; RF-13, consultas y seguimiento. Representa la consulta de información, sin registrar incidencias ni generar alertas institucionales.

**3. Información presentada:** Fecha y hora, código y nombre abreviado del paciente, servicio, estudiante asignado, carrera y estado. Incluye búsqueda, filtros y acceso al detalle de cada cita.

**4. Usuarios destinatarios:** Coordinación consulta el conjunto; docentes, su grupo; estudiantes, sus citas; pacientes, únicamente sus propias citas.

**5. Formato de presentación:** Tabla en pantalla, descarga CSV compatible con Excel e impresión con opción de guardar como PDF desde el navegador.

**6. Boceto o prototipo:** [Ver captura de la agenda](../Recursos/SO-01-agenda.png) · [Abrir HTML de salidas](../../prototipo/salidas/UAM-LINK.html), vista «Agenda».

## SO-02. Detalle y documentos de cita

**1. Nombre y objetivo:** Detalle y documentos de cita. Mostrar la información de una cita y permitir conservar el documento correspondiente a su estado.

**2. Requerimientos funcionales:** RF-04, programación; RF-05, seguimiento de estados; RF-06, atención realizada. La constancia representa una atención de ejemplo, sin sustituir el registro clínico.

**3. Información presentada:** Código de cita, estado, paciente, servicio, fecha y hora, lugar, estudiante y modalidad. Si fue reprogramada, incluye la fecha anterior. El documento se denomina «Comprobante» para citas confirmadas o reprogramadas, «Constancia» para atendidas y «Detalle» para los demás estados.

**4. Usuarios destinatarios:** Paciente de la cita, coordinación y docentes o estudiantes dentro de su alcance de consulta.

**5. Formato de presentación:** Panel lateral en pantalla y documento HTML descargable e imprimible. Puede guardarse como PDF mediante la impresión del navegador; no se envía automáticamente.

**6. Boceto o prototipo:** [Ver captura del comprobante](../Recursos/SO-02-comprobante.png) · [Abrir HTML de salidas](../../prototipo/salidas/UAM-LINK.html) y seleccionar una cita de la agenda.

## SO-03. Resumen y seguimiento

**1. Nombre y objetivo:** Resumen y seguimiento. Identificar el volumen de citas, su distribución y las atenciones pendientes para apoyar la supervisión.

**2. Requerimientos funcionales:** RF-05, seguimiento de estados; RF-13, consultas y seguimiento. Los indicadores no implementan alertas por límites institucionales.

**3. Información presentada:** Total de citas, atendidas, por realizar, canceladas y ausencias, además de distribución por carrera. «Por realizar» agrupa pendientes, confirmadas y reprogramadas. Los indicadores responden al período y a los filtros generales; la búsqueda y el filtro de estado sólo afectan la tabla de agenda.

**4. Usuarios destinatarios:** Coordinación, docentes para su grupo y estudiantes para su actividad. No se presenta al paciente.

**5. Formato de presentación:** Indicadores numéricos y barras de distribución en pantalla.

**6. Boceto o prototipo:** [Ver resumen](../Recursos/SO-03-resumen.png) · [Ver distribución](../Recursos/SO-03-distribucion.png) · [Abrir HTML de salidas](../../prototipo/salidas/UAM-LINK.html), sección de resumen de la agenda.

## SO-04. Reporte de citas por estudiante

**1. Nombre y objetivo:** Reporte de citas por estudiante. Consolidar las citas realizadas y pendientes de cada estudiante durante el período seleccionado.

**2. Requerimientos funcionales:** RF-04, programación; RF-05, seguimiento de estados; RF-14, generación de reportes.

**3. Información presentada:** Estudiante, carrera, citas atendidas, por realizar, canceladas, ausencias y totales. Incluye período, filtros aplicados, identificación del formato REP-CIT-001, emisión, fecha de generación y fuente de los datos.

**4. Usuarios destinatarios:** Coordinación, docentes para los estudiantes de su grupo y estudiantes para su propio reporte.

**5. Formato de presentación:** Tabla en pantalla, CSV compatible con Excel e impresión/PDF mediante el navegador, con encabezados y paginación. La descarga tabular es CSV, no un archivo `.xlsx`.

**6. Boceto o prototipo:** [Ver captura del reporte](../Recursos/SO-04-reporte-citas.png) · [Abrir HTML de salidas](../../prototipo/salidas/UAM-LINK.html), vista «Reportes», reporte de citas.

## SO-05. Actividad académica

**1. Nombre y objetivo:** Actividad académica. Consultar la actividad registrada por estudiante y distinguir los resultados validados por el docente de los pendientes de validación.

**2. Requerimientos funcionales:** RF-06, registro de atención; RF-09, validación docente; RF-10, seguimiento académico; RF-14, reportes. Es una ampliación del alcance inicial: no calcula cumplimiento semestral sin metas institucionales aprobadas.

**3. Información presentada:** Estudiante, pacientes únicos, sesiones y horas registradas, validadas y por validar. Sólo se consideran citas atendidas; las horas pendientes de validación no se presentan como aprobadas. Incluye período, filtros e identificación de la emisión y fuente.

**4. Usuarios destinatarios:** Coordinación, docentes para su grupo y estudiantes para su propia actividad. No se presenta al paciente.

**5. Formato de presentación:** Tabla en pantalla, CSV compatible con Excel e impresión con opción de guardar como PDF desde el navegador.

**6. Boceto o prototipo:** [Ver captura de actividad académica](../Recursos/SO-05-actividad.png) · [Abrir HTML de salidas](../../prototipo/salidas/UAM-LINK.html), vista «Reportes», reporte de actividad académica.

## Alcance común

Los destinatarios se simulan mediante un selector de vista; el prototipo no implementa autenticación ni permisos reales. La información corresponde a ejemplos con corte simulado del 23 de octubre de 2026 a las 18:00 h en Nicaragua. Los reportes identifican su generación y fuente para distinguir la fecha de consulta del corte de datos. Los HTML de entrada y salida son independientes: completar una solicitud no modifica estas salidas.
