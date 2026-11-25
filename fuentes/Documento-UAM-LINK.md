# UAM LINK

## Diseño de entradas y salidas del sistema

**UNIVERSIDAD AMERICANA**  
**FACULTAD DE INGENIERÍA Y ARQUITECTURA**  
**Asignatura:** Análisis y diseño de sistemas

**Integrantes del proyecto**

| Identificación | Nombre completo |
| --- | --- |
| 25015790 | Roberto José Jerez Largaespada |
| 26010836 | Michael Alejandro Wong Espinoza |
| 25015315 | David Alejandro Bermudez Barberena |
| 26010747 | Shane Alejandro Rodriguez Vega |
| 25012339 | Shylon Emeil Andrews Hunter |

**Docente:** Jose Alejandro Duran Garcia  
**Período:** Segundo semestre de 2026  
**Lugar y fecha:** Managua, Nicaragua, 19 de octubre de 2026


---

## 1. Descripción del sistema

UAM LINK centraliza solicitudes, programación y seguimiento de pacientes en las prácticas supervisadas de Odontología, Psicología, Nutrición y Medicina de la UAM. Sus actores son pacientes, estudiantes, recepción, coordinación y docentes.

La entrega incluye un formulario en cuatro pasos y un módulo de consultas y reportes. Los HTML son independientes, funcionan sin Internet y utilizan datos ficticios; no guardan ni intercambian información. Las vistas por destinatario son una demostración, no autenticación real.

## 2. Fundamentación y coherencia

Siguiendo los criterios de Kendall y Kendall, las entradas priorizan precisión, facilidad de uso, consistencia y simplicidad; las salidas consideran propósito, destinatario, cantidad, oportunidad y medio. La identidad aqua y blanca mantiene la continuidad visual entre módulos.

El flujo lógico propuesto es:

```text
Paciente → Solicitud → Evaluación y programación → Cita
Estudiante y docente → Registro y validación de atención → Actividad académica
Citas y actividad académica → Consultas y reportes para cada destinatario
```

La fecha preferida no confirma una cita. La asignación, asistencia, horas y validación docente requieren procesos administrativos posteriores. Sus resultados se representan con ejemplos, pero sus entradas administrativas todavía no están implementadas.

## 3. Diseños de entradas y especificaciones

**Usuario:** paciente, con posible asistencia de recepción. **Formato común:** pantalla web en [el HTML de entrada](../prototipo/entradas/UAM-LINK-entrada.html).

Las fichas completas de cada paso están en [Especificaciones de entradas](Entradas/Especificaciones-entradas.md).

Los campos obligatorios se identifican con asteriscos. «Siguiente» valida cada paso, «Anterior» conserva los datos y «Limpiar formulario» solicita confirmación.

### EN-01 Datos del paciente

**Objetivo:** identificar al solicitante y obtener su contacto. **RF:** RF-02.

| Campo | Validación |
| --- | --- |
| Nombres y apellidos | Obligatorios; máximo 80 y 100 caracteres, respectivamente. |
| Correo | Obligatorio, formato válido y máximo 254 caracteres. |
| Teléfono | Opcional; 8–15 dígitos y máximo 20 caracteres con separadores. |
| Nacimiento | Obligatorio y anterior a hoy en Nicaragua. |

**Boceto:** [captura del paso 1](Recursos/EN-01-datos.png).

### EN-02 Selección del servicio

**Objetivo:** indicar el servicio para orientar la programación posterior. **RF:** RF-04.

La selección es única y obligatoria: valoración odontológica, limpieza dental, atención psicológica, consulta nutricional o medicina general. Cada opción tiene un código de servicio y una carrera asociados. No asigna automáticamente estudiante ni cita.

**Boceto:** [captura del paso 2](Recursos/EN-02-servicio.png).

### EN-03 Preferencia de atención

**Objetivo:** recoger modalidad, horario preferido y motivo general. **RF:** RF-04.

Se exige modalidad presencial o virtual y una fecha/hora futura interpretada en Nicaragua, UTC−6. El motivo es opcional, con máximo 4000 caracteres. La disponibilidad y las modalidades permitidas por servicio deben revisarse institucionalmente; el motivo no sustituye un expediente clínico.

**Boceto:** [captura del paso 3](Recursos/EN-03-preferencia.png).

### EN-04 Revisión y aceptación

**Objetivo:** revisar y corregir los datos antes de finalizar. **RF:** RF-08, parcialmente.

Muestra paciente, contacto, servicio y preferencias con botones para corregir. Incluye información consultable y aceptación obligatoria; modificar datos desmarca la aceptación. El texto es de demostración y no reemplaza el consentimiento clínico oficial. La acción final sólo valida el ejemplo.

**Boceto:** [captura del paso 4](Recursos/EN-04-revision.png).

## 4. Diseños de salidas y especificaciones

**Prototipo común:** [HTML de salidas](../prototipo/salidas/UAM-LINK.html).

Las fichas completas de cada salida están en [Especificaciones de salidas](Salidas/Especificaciones-salidas.md).

Las vistas delimitan los ejemplos por coordinación, grupo docente, estudiante o paciente. Cada salida identifica período, formato, emisión, generación y fuente. La consulta es bajo demanda; el corte del 23 de octubre de 2026 a las 18:00 h es simulado, no una actualización real.

### SO-01 Agenda de citas

**Objetivo:** consultar programación y estados. **RF:** RF-04, RF-05 y RF-13.

**Información:** fecha/hora, paciente abreviado y código, servicio, estudiante, carrera y estado. Permite búsqueda, filtros y acceso al detalle.

**Destinatarios:** coordinación, docentes y estudiantes según su alcance; el paciente consulta sus propias citas. **Formato:** pantalla, CSV e impresión/PDF.

**Boceto:** [agenda](Recursos/SO-01-agenda.png).

### SO-02 Detalle y documentos de cita

**Objetivo:** consultar una cita y conservar el documento correspondiente. **RF:** RF-04, RF-05 y RF-06.

**Información:** código, estado, paciente, servicio, fecha/hora, lugar, estudiante, modalidad y fecha anterior si fue reprogramada. Distingue comprobante para confirmadas/reprogramadas, constancia para atendidas y detalle para los demás estados.

**Destinatarios:** paciente y personal autorizado. **Formato:** panel lateral y HTML descargable e imprimible; sin envío automático.

**Boceto:** [comprobante](Recursos/SO-02-comprobante.png).

### SO-03 Resumen y seguimiento

**Objetivo:** identificar volumen de citas y pendientes. **RF:** RF-05 y RF-13.

**Información:** total, atendidas, por realizar, canceladas, ausencias y distribución por carrera. «Por realizar» suma pendientes, confirmadas y reprogramadas. Los indicadores usan filtros generales; la búsqueda y el estado sólo afectan la tabla.

**Destinatarios:** coordinación, docentes y estudiantes; no pacientes. **Formato:** indicadores y barras en pantalla.

**Bocetos:** [resumen](Recursos/SO-03-resumen.png) y [distribución](Recursos/SO-03-distribucion.png).

### SO-04 Reporte de citas por estudiante

**Objetivo:** consolidar citas realizadas y pendientes por período. **RF:** RF-04, RF-05 y RF-14.

**Información:** estudiante, carrera, atendidas, por realizar, canceladas, ausencias y totales. Incluye filtros, formato REP-CIT-001, emisión y generación.

**Destinatarios:** coordinación, docentes para su grupo y estudiantes para su actividad. **Formato:** pantalla, CSV e impresión/PDF con encabezados y paginación. CSV es compatible con Excel, pero no es `.xlsx`.

**Boceto:** [reporte de citas](Recursos/SO-04-reporte-citas.png).

### SO-05 Actividad académica

**Objetivo:** distinguir actividad registrada y validación docente. **RF:** RF-06, RF-09, RF-10 y RF-14.

**Información:** estudiante, pacientes únicos, sesiones y horas registradas, validadas y por validar. Sólo considera citas atendidas; las horas por validar no son aprobadas.

**Destinatarios:** coordinación, docentes y estudiantes según su alcance. **Formato:** pantalla, CSV e impresión/PDF. Es una ampliación del alcance inicial y no calcula cumplimiento semestral sin metas aprobadas.

**Boceto:** [actividad académica](Recursos/SO-05-actividad.png).

## 5. Cobertura de requerimientos

Las relaciones anteriores muestran qué datos o resultados representa cada diseño; no significan implementación completa del RF.

| Requerimientos | Alcance o pendiente |
| --- | --- |
| RF-01 | Vistas de roles simuladas; sin registro de usuarios ni permisos reales. |
| RF-02 y RF-04 | Captura y consulta; faltan persistencia, mantenimiento y asignación administrativa. |
| RF-03, RF-07, RF-11 y RF-12 | Sin prototipos de elegibilidad, expediente, remisiones/cierre ni costos/adjuntos. |
| RF-05 y RF-13 | Estados, conteos y consultas; faltan registro de incidencias y alertas por límites institucionales. |
| RF-06 y RF-09 | Se muestran resultados; faltan entradas para registrar atenciones y validar evidencias. |
| RF-08 | Aceptación de solicitud; pendiente consentimiento clínico oficial y su conservación. |
| RF-10 y RF-14 | Actividad y reportes con datos ficticios; pendientes metas y operación con información real. |

## 6. Verificación y conclusiones

Se verificaron navegación, validaciones, corrección, limpieza protegida, alcance de vistas, cálculos, descargas y adaptación móvil. El ejemplo contiene 16 citas: 3 atendidas, 10 por realizar, 2 canceladas y 1 ausencia. Su impresión ocupa dos páginas con identificación y pies correctos.

El diseño organiza la captura y presenta resultados interpretables sin duplicar operaciones. La trazabilidad distingue lo representado de lo pendiente y mantiene separados los datos solicitados, programados y validados. Para operar se necesitan reglas institucionales, consentimiento aprobado, integración, almacenamiento, seguridad y validación con usuarios. Los prototipos no acreditan cumplimiento integral del sistema.

## 7. Referencias y uso

- Kendall y Kendall (2008), *Systems Analysis and Design*, 7.ª edición: materiales de [entradas](https://www.slideserve.com/marlow/designing-effective-input) y [salidas](https://www.slideserve.com/hasad/designing-effective-output), reproducciones públicas identificadas como material de Pearson.
- Documentos del proyecto: *Propuesta Caso de Estudio Final - 2S2026* y *Requerimientos Funcionales y no Funcionales*.

Abre los HTML de `Entradas/` y `Salidas/` con un navegador y utiliza datos ficticios. Conserva `Recursos/` junto al Markdown para abrir las capturas. Completar la entrada no agrega registros a las salidas.
