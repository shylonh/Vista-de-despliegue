# UAM LINK · Vista de despliegue UML

**Asignatura:** Análisis y Diseño de Sistemas · Universidad Americana  
**Entrega individual:** Shylon Emeil Andrews Hunter  
**Fecha:** 25 de noviembre de 2026

UAM LINK organiza solicitudes de pacientes, citas y seguimiento de prácticas supervisadas de Odontología, Psicología, Nutrición y Medicina. Los usuarios son pacientes, recepción, estudiantes, docentes y coordinación.

## Entregables

| Archivo | Contenido |
|---|---|
| [Proyecto editable](diagramas/UAM-LINK-Despliegue.feap) | Modelo de Enterprise Architect con dos diagramas de despliegue |
| [Diagrama principal PDF](diagramas/UAM-LINK-Despliegue.pdf) | Arquitectura objetivo propuesta para el sistema completo |
| [Diagrama principal PNG](diagramas/UAM-LINK-Despliegue.png) | Imagen del mismo modelo |
| [Prototipo actual PDF](diagramas/UAM-LINK-Prototipo-Actual.pdf) | Despliegue local observado en los HTML entregados |
| [Descripción técnica](documentacion/descripcion-tecnica.md) | Nodos, entornos, componentes, artefactos, conexiones y decisiones |
| [Guía de defensa](documentacion/guia-defensa.md) | Exposición y preguntas con respuestas |
| [Uso de Enterprise Architect](documentacion/abrir-en-enterprise-architect.md) | Cómo abrir y revisar el modelo |

## Alcance y evidencia

Los HTML de `prototipo/` son la implementación disponible: funcionan localmente, utilizan datos ficticios, no comparten información y no tienen autenticación ni persistencia reales. Abrirlos directamente en un navegador:

- [Formulario de solicitud](prototipo/entradas/UAM-LINK-entrada.html).
- [Agenda, consultas y reportes](prototipo/salidas/UAM-LINK.html).

El diagrama principal es una **arquitectura objetivo propuesta**, no un despliegue ya operativo. Está fundamentado en la [matriz de viabilidad técnica](fuentes/Viabilidad-Tecnica.xlsx), que contempla web responsiva, API, base relacional, alojamiento y SMTP. Se propone Node.js para la API y MySQL para persistencia; no se afirma que esas tecnologías ya estén implementadas. Los ZIP de código y SQL de esos futuros servicios no existen todavía.

El segundo diagrama refleja estrictamente el estado actual del prototipo. GitHub conserva los archivos y versiones de esta entrega; no sustituye el servidor de aplicación ni la base de datos. No se ha activado GitHub Pages.

## Arquitectura objetivo

1. Un paciente o miembro autorizado utiliza el navegador de su computadora o teléfono.
2. El navegador solicita la interfaz y consume la API mediante HTTPS, puerto 443.
3. El servidor de aplicación valida roles, solicitudes, disponibilidad, citas, atenciones y reportes.
4. La API consulta MySQL por TCP 3306 en una red privada, con TLS configurado.
5. El módulo de notificaciones envía avisos mediante SMTP 587 con STARTTLS.

No se representa un expediente clínico completo como una función implementada. La disponibilidad real de un servicio, el consentimiento clínico y la validación docente siguen sujetos a procesos y reglas institucionales.

## Organización

- `diagramas/`: FEAP, PDF, PNG y fuente PlantUML de referencia.
- `documentacion/`: descripción y material para la defensa.
- `prototipo/`: HTML originales, con sus datos ficticios.
- `fuentes/`: documentación y evidencias del proyecto recibido.

No se incluyeron grabaciones de entrevistas ni credenciales. Los artefactos del servidor y de base de datos dibujados en la vista propuesta son unidades de despliegue previstas, no archivos de backend entregados.
