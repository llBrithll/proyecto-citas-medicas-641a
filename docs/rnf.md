# Requerimientos no funcionales

| # | Atributo | Métrica | Umbral | Condición de carga | Verificación | Consecuencia si no se cumple |
|---|---|---|---|---|---|---| fd
| 1 | Rendimiento | p95 de latencia | Menor a 400 ms | 200 usuarios concurrentes | Prueba de carga | Los usuarios pueden percibir lentitud y abandonar el proceso de reserva |
| 2 | Disponibilidad | Porcentaje de disponibilidad mensual | Mayor o igual al 99.5% | Operación normal del sistema | Monitoreo de disponibilidad | Los pacientes no podrían consultar o gestionar sus citas |
| 3 | Seguridad | Intentos fallidos permitidos | Máximo 5 intentos consecutivos | Inicio de sesión de usuarios | Prueba funcional de autenticación | Puede aumentar el riesgo de accesos no autorizados |
| 4 | Recuperabilidad | Tiempo de recuperación y pérdida máxima de datos | Recuperación en máximo 2 horas y pérdida máxima de 24 horas de datos | Falla del almacenamiento con hasta 10.000 documentos y 100 GB de archivos | Prueba de restauración de copias de seguridad y validación de integridad de archivos y metadatos | Se pueden perder documentos e interrumpir las actividades de la organización |

## Escenarios completos

### Escenario 1 - Rendimiento

- Fuente: Usuario o personal administrativo.
- Estímulo: El usuario realiza una búsqueda, consulta o descarga de un documento almacenado en el sistema.
- Artefacto: Sistema de Gestión Documental.
- Entorno: Hasta 200 usuarios utilizando el sistema de manera concurrente.
- Respuesta: El sistema procesa la solicitud y muestra los documentos o la información solicitada.
- Medida: El 95% de las consultas debe responder en menos de 400 ms.

### Escenario 2 - Disponibilidad

- Fuente: Usuario o personal administrativo.
- Estímulo: El usuario intenta ingresar al sistema para consultar, cargar, descargar o administrar documentos.
- Artefacto: Sistema de Gestión Documental.
- Entorno: Operación normal del sistema.
- Respuesta: El sistema debe permanecer disponible para permitir el acceso y gestión de los documentos.
- Medida: Disponibilidad mensual igual o superior al 99.5%.

### Escenario 3 - Seguridad

- Fuente: Usuario que intenta iniciar sesión.
- Estímulo: Ingresa credenciales incorrectas en cinco intentos consecutivos para una misma cuenta.
- Artefacto: Módulo de autenticación del Sistema de Gestión Documental.
- Entorno: Operación normal, durante el inicio de sesión.
- Respuesta: El sistema rechaza las credenciales incorrectas y, al quinto intento fallido consecutivo, bloquea temporalmente nuevos intentos de acceso a la cuenta.
- Medida: El bloqueo se activa al completar cinco intentos fallidos consecutivos, verificado mediante una prueba funcional de autenticación.

### Escenario 4 - Recuperabilidad

- Fuente: Falla del servicio de almacenamiento.
- Estímulo: Los documentos y sus metadatos dejan de estar accesibles por una falla del almacenamiento.
- Artefacto: Archivos y base de datos del Sistema de Gestión Documental.
- Entorno: Hasta 10.000 documentos y 100 GB de archivos, con copias de seguridad disponibles.
- Respuesta: El responsable de operación restaura los archivos y sus metadatos desde la copia de seguridad y verifica su integridad antes de restablecer el servicio.
- Medida: El servicio se restablece en máximo 2 horas desde la falla, con una pérdida de datos correspondiente a no más de las últimas 24 horas.