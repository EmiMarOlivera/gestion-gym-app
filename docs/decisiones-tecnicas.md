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
