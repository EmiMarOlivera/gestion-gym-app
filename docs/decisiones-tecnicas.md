# Decisiones técnicas

## DT-01 – Organización interna de la API (25/10/2026, Sprint 2, T10)
**Decisión:** un solo proyecto de API organizado por módulos (Alumnos, Rutinas, Agenda, Pagos), cada uno con sus endpoints, su lógica y sus entidades, más una parte común para el acceso a datos y las integraciones externas.
**Alternativa descartada:** Clean Architecture en cuatro proyectos (Domain, Application, Infrastructure, Api).
**Motivo:** sigue lo definido en el anteproyecto (Tabla 4 y sección 2.8: "una única API organizada en módulos reduce la complejidad"), reduce la estructura a mantener para un solo desarrollador y permite separar un módulo más adelante si hiciera falta.
