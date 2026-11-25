# Especificaciones de entradas — UAM LINK

Las cuatro entradas son pasos de un mismo formulario de solicitud, dirigido al paciente con posible asistencia de recepción. Su organización aplica los criterios de claridad, simplicidad, consistencia y reducción de errores de Kendall y Kendall.

## EN-01. Datos del paciente

**1. Nombre y propósito:** Datos del paciente. Identificar al solicitante y obtener sus datos de contacto.

**2. Requerimiento funcional:** RF-02, registro de pacientes. El prototipo representa la captura; no almacena registros.

**3. Datos ingresados:**

| Dato | Tipo | Obligatorio | Longitud o formato |
| --- | --- | --- | --- |
| Nombres | Texto | Sí | Máximo 80 caracteres |
| Apellidos | Texto | Sí | Máximo 100 caracteres |
| Correo electrónico | Correo (`email`) | Sí | Máximo 254 caracteres |
| Teléfono | Texto telefónico (`tel`) | No | Máximo 20 caracteres; entre 8 y 15 dígitos |
| Fecha de nacimiento | Fecha (`date`) | Sí | AAAA-MM-DD como valor interno; presentación según navegador |

**4. Validaciones:** Nombres y apellidos no pueden contener solamente espacios. El correo debe cumplir el formato de correo del navegador. El teléfono, cuando se ingresa, admite dígitos, espacios, paréntesis, guiones y signo `+`, respetando sus límites. El nacimiento debe ser una fecha válida anterior al día actual en Nicaragua. No se permite continuar con campos obligatorios incompletos o inválidos.

**5. Boceto o prototipo:** [Ver captura del paso 1](../Recursos/EN-01-datos.png) · [Abrir HTML, paso Datos del paciente](UAM-LINK-entrada.html#datos).

## EN-02. Selección del servicio

**1. Nombre y propósito:** Selección del servicio. Indicar la atención solicitada para orientar la programación posterior.

**2. Requerimiento funcional:** RF-04, programación de citas. Recoge un insumo para programar; no asigna estudiante ni confirma una cita.

**3. Datos ingresados:**

| Dato | Tipo | Obligatorio | Longitud o dominio |
| --- | --- | --- | --- |
| Servicio solicitado | Enumeración; selección única | Sí | Una de cinco opciones: valoración odontológica, limpieza dental, atención psicológica, consulta nutricional o consulta de medicina general |

La carrera se deriva del servicio seleccionado; no se vuelve a solicitar al paciente. La longitud no aplica porque se utilizan opciones cerradas.

**4. Validaciones:** Exigir una selección antes de continuar. Los botones de opción permiten elegir un solo servicio del catálogo. La correspondencia servicio–carrera permanece definida por el sistema.

**5. Boceto o prototipo:** [Ver captura del paso 2](../Recursos/EN-02-servicio.png) · [Abrir HTML de entrada](../../prototipo/entradas/UAM-LINK-entrada.html), paso «Servicio».

## EN-03. Preferencia de atención

**1. Nombre y propósito:** Preferencia de atención. Recoger modalidad, horario preferido y motivo general de la solicitud.

**2. Requerimiento funcional:** RF-04, programación de citas. El horario es una preferencia sujeta a revisión de disponibilidad.

**3. Datos ingresados:**

| Dato | Tipo | Obligatorio | Longitud o formato |
| --- | --- | --- | --- |
| Modalidad | Enumeración; selección única | Sí | Presencial o virtual; longitud no aplicable |
| Fecha y hora preferidas | Fecha y hora (`datetime-local`) | Sí | AAAA-MM-DDTHH:mm; interpretada en Nicaragua, UTC−6 |
| Motivo general | Texto multilínea | No | Máximo 4000 caracteres |

**4. Validaciones:** Exigir una modalidad y una fecha/hora válida posterior al momento actual en Nicaragua. Respetar el límite del motivo. La disponibilidad y la compatibilidad entre modalidad y servicio requieren revisión institucional posterior; el prototipo no las comprueba. El motivo no sustituye el expediente clínico.

**5. Boceto o prototipo:** [Ver captura del paso 3](../Recursos/EN-03-preferencia.png) · [Abrir HTML de entrada](../../prototipo/entradas/UAM-LINK-entrada.html), paso «Preferencia».

## EN-04. Revisión y aceptación

**1. Nombre y propósito:** Revisión y aceptación de la solicitud. Permitir comprobar y corregir los datos antes de validar el ejemplo.

**2. Requerimiento funcional:** RF-08, relación parcial con la aceptación informada. Esta aceptación de solicitud no implementa el consentimiento clínico institucional.

**3. Datos ingresados:**

| Dato | Tipo | Obligatorio | Longitud o dominio |
| --- | --- | --- | --- |
| Aceptación de la información de solicitud | Booleano; casilla de verificación | Sí | Marcada/desmarcada; debe estar marcada para finalizar |

El resumen de paciente, contacto, servicio, modalidad y horario se obtiene de los pasos anteriores; no constituye una nueva captura. Los enlaces de corrección permiten volver al paso correspondiente.

**4. Validaciones:** Exigir la aceptación y volver a validar los pasos previos al finalizar. Si se modifica cualquier dato, desmarcar la aceptación para que el usuario revise nuevamente la información. El texto informativo está disponible antes de aceptar. La acción final sólo valida datos de ejemplo: no envía ni conserva información.

**5. Boceto o prototipo:** [Ver captura del paso 4](../Recursos/EN-04-revision.png) · [Abrir HTML de entrada](../../prototipo/entradas/UAM-LINK-entrada.html), paso «Revisión».

## Comportamiento común

Los campos obligatorios tienen asterisco y los errores muestran un mensaje y señalan el campo que debe corregirse. «Anterior» conserva los datos y «Limpiar formulario» pide confirmación. Las validaciones descritas se ejecutan en el navegador; al implementar el sistema deben repetirse en el servidor antes de guardar información.
