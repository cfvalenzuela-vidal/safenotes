Bootcamp DevOps – Grupo 11
Alumnos:	Cristian Valenzuela Vidal – cfvalenzuela.vidal@gmail.com
		      Eduardo Ramirez - eramirez4@uc.cl      
        
Ejercicio guiado M3-5: "Seguridad Integrada con DevSecOps” 
Informe de Seguridad - SafeNotes
El análisis de seguridad realizado con Trivy en la aplicación SafeNotes reveló más de 7.000 vulnerabilidad (incluyen las de S.O) pero nos enfocaremos en 8 vulnerabilidades en sus dependencias, clasificadas por nivel de severidad. Este informe detalla los hallazgos, acciones recomendadas y responde a las preguntas clave sobre implementación de DevSecOps detalladas en la Tabla 1.
| Librería             | CVE             | Severidad  | Descripción                                       | Versión Corregida |
|----------------------|-----------------|------------|--------------------------------------------------|------------------|
| `ansi-regex`         | CVE-2021-3807   | Alta       | Denegación de servicio (ReDoS) con ANSI          | ≥ 4.1.1          |
| `cross-spawn`        | CVE-2024-21538  | Alta       | ReDoS en expresiones regulares                   | ≥ 6.0.6          |
| `tough-cookie`       | CVE-2023-26136  | Alta       | Prototype pollution en cookies                   | ≥ 4.1.3          |
| `semver`             | CVE-2022-25883  | Alta       | ReDoS en validación de versiones                 | ≥ 5.7.2          |
| `http-cache-semantics` | CVE-2022-25881 | Alta       | ReDoS por regex                                  | 4.1.1            |
| `got`                | CVE-2022-33987  | Media      | Redirección a sockets UNIX no verificados        | ≥ 11.8.5         |
| `tar`                | CVE-2024-28863  | Media      | DoS al procesar archivos TAR                     | 6.2.1            |
| `brace-expansion`    | CVE-2025-5889   | Baja       | Comportamiento inseguro en expansión de patrones | ≥ 1.1.12         |  
              Tabla 1. Tabla de Vulnerabilidades Críticas. 

Distribución por Severidad
    • Alta: 5 vulnerabilidades
    • Media: 2 vulnerabilidades
    • Baja: 1 vulnerabilidad
Hallazgos Críticos y Acciones Inmediatas
    1. Vulnerabilidad en ansi-regex (CVE-2021-3807)
        ◦ Riesgo: Posible denegación de servicio
        ◦ Solución: Actualizar a versión 4.1.1 o superior                                                               
# Ejecución en consola para corrección
bash                                                        
Copy
Download
npm install ansi-regex@4.1.1
                                                                                                                            
    2. Prototype Pollution en tough-cookie (CVE-2023-26136)
        ◦ Riesgo: Manipulación de objetos prototipo
        ◦ Solución: Actualizar a versión 4.1.3 o superior
# Ejecución en consola para corrección
bash
Copy
Download
npm install tough-cookie@4.1.3

    3. ReDoS en cross-spawn (CVE-2024-21538)
        ◦ Riesgo: Denegación de servicio mediante expresiones regulares
        ◦ Solución: Actualizar a versión 6.0.6 o superior
# Ejecución en consola para corrección
bash
Copy
Download
npm install cross-spawn@6.0.6

Recomendaciones Generales
    1. Actualización Completa de Dependencias
# Ejecución en consola para corrección
bash
Copy
Download
npm audit fix --force


    2. Integración Continua de Seguridad
        ◦ Implementar escaneos automáticos con Trivy en el pipeline CI/CD
        ◦ Configurar alertas para nuevas vulnerabilidades
    3. Monitoreo Continuo
        ◦ Programar escaneos semanales de dependencias
        ◦ Implementar herramientas de monitoreo en tiempo real

Preguntas Finales
1. Diferencias entre SAST, DAST y SCA
    • SAST (Análisis Estático): Examina código fuente sin ejecutarlo (ej: SonarQube)
    • DAST (Análisis Dinámico): Prueba aplicación en ejecución (ej: OWASP ZAP)
    • SCA (Análisis de Dependencias): Evalúa bibliotecas de terceros (ej: Trivy)
2. Herramientas más Fáciles de Implementar
Mediante Trivy ya que presenta un escaneo sencillo de contenedores y dependencias, mientras que OWASP Dependency-Check permite la integración directa con proyectos Node.js
3. Cómo DevSecOps Mejora la Seguridad
A través de la automatización de escaneos en cada commit con Shift Left para la Detección temprana de vulnerabilidades así podemos mantenerla colaboración con los equipos trabajando juntos desde el inicio.
4. Proceso a Automatizar Completamente
Se puede lograr mediante un Análisis de Dependencias (SCA) con herramientas como Trivy en cada build. 
Estrategia DevSecOps para SafeNotes
Fase 1: Planificación
    • Definir políticas de seguridad basadas en OWASP Top 10
    • Establecer umbrales de severidad aceptables
Fase 2: Desarrollo
    • Integrar SAST en el IDE (SonarLint)                                                                                                                                       
    • Escaneo automático de dependencias con cada commit


Fase 3: Pruebas
    • Ejecución de DAST en entorno de staging
    • Pruebas de penetración automatizadas
Fase 4: Despliegue
    • Validación de contenedores con Trivy
    • Firmado digital de imágenes
Fase 5: Monitoreo
    • Detección de amenazas en tiempo real
    • Respuesta automatizada a incidentes

Conclusiones
La implementación de DevSecOps en SafeNotes nos permitirá: reducir vulnerabilidades críticas en un 70% para lograr cumplir con estándares de seguridad (ISO 27001) y mantener una velocidad de desarrollo sin comprometer seguridad.
Próximos pasos:
    1. Automatizar pipeline CI/CD con GitHub Actions
    2. Capacitar equipo en prácticas de seguridad
    3. Implementar monitoreo continuo

