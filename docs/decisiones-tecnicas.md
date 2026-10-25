# Decisiones técnicas

## DT-01 – Organización interna de la API (25/10/2026, Sprint 2, T10)
**Decisión:** un solo proyecto de API organizado por módulos (Alumnos, Rutinas, Agenda, Pagos), cada uno con sus endpoints, su lógica y sus entidades, más una parte común para el acceso a datos y las integraciones externas.
**Alternativa descartada:** Clean Architecture en cuatro proyectos (Domain, Application, Infrastructure, Api).
**Motivo:** sigue lo definido en el anteproyecto (Tabla 4 y sección 2.8: "una única API organizada en módulos reduce la complejidad"), reduce la estructura a mantener para un solo desarrollador y permite separar un módulo más adelante si hiciera falta.

## DT-02 – Acceso a la base de datos (25/10/2026, Sprint 2, T10)
**Decisión:** la API accede a Azure SQL Database mediante Entity Framework Core, con migraciones versionadas en el repositorio.
**Alternativa descartada:** consultas SQL escritas a mano (Dapper o ADO.NET).
**Motivo:** el anteproyecto establece que en el repositorio se versionan las migraciones de base de datos (sección 2.10.4) y que el modelo de clases se traduce en tablas (sección 2.9.2), lo que EF Core resuelve de forma nativa en el ecosistema .NET elegido (sección 2.3).

## DT-03 – Lenguaje de la PWA (25/10/2026, Sprint 2, T10)
**Decisión:** la PWA se desarrolla en React con TypeScript.
**Alternativa descartada:** React con JavaScript.
**Motivo:** extiende al frontend el criterio de tipado fuerte con el que se eligió .NET para un sistema que maneja datos de salud (Tabla 5), y es coherente con las convenciones del plan de calidad, que incluyen interfaces y componentes en PascalCase (sección 2.10.3). Es una tecnología nueva para el autor; su aprendizaje se incorpora a la capacitación del sprint (riesgo R1).

## DT-04 – Organización de la PWA (25/10/2026, Sprint 2, T10)
**Decisión:** el código de la PWA se organiza por funcionalidad (auth, alumnos, rutinas, agenda, pagos, home), con una carpeta compartida para los componentes comunes y un único cliente que concentra las llamadas a la API, y con rutas separadas por rol (PT y Alumno).
**Alternativa descartada:** organización por tipo de archivo (pages, components, services).
**Motivo:** espeja los módulos de la API definidos en el anteproyecto (Tabla 4, DT-01); el cliente único respeta que el frontend se comunique solo con la API y nunca con servicios externos (sección 2.8); las rutas por rol responden a los Home diferenciados del PT y del alumno (CU28, CU29).

## DT-05 – Columna "Segundo plano" en el tablero (25/10/2026, Sprint 2)
**Decisión:** se agrega al tablero una quinta columna, "Segundo plano", para las tareas continuas del sprint (capacitación, gestión y documentación), además de Por hacer, En curso, En prueba y Hecho.
**Alternativa descartada:** mantener solo las cuatro columnas de la sección 2.10.1 y dejar esas tareas en Por hacer hasta el cierre.
**Motivo:** son tareas que se realizan de forma constante durante todo el sprint; ubicarlas en En curso ocuparía el límite de dos tarjetas destinado al desarrollo, y dejarlas en Por hacer no reflejaría que están en marcha. Ajuste al marco de trabajo de la sección 2.10.1, a reflejar en el documento final.

## DT-06 – Repositorios separados para backend y frontend (25/10/2026, Sprint 2)
**Decisión:** el código se versiona en dos repositorios: gestion-gym-app-back (API .NET) y gestion-gym-app-front (PWA React), cada uno con su propio pipeline, su análisis de SonarQube y su regla de protección de main. El tablero de GitHub Projects es único y reúne los issues de ambos.
**Alternativa descartada:** un único repositorio con la API y la PWA en carpetas separadas, como se planteó en la sección 2.10.4.
**Motivo:** el backend y el frontend son aplicaciones independientes que se despliegan por separado; separarlos da a cada uno su propio historial, pipeline y despliegue, y prepara el producto para crecer. Cambio respecto del anteproyecto, a reflejar en la sección 2.10.4 y en el anexo de acceso al repositorio en el documento final.
