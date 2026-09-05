# SEI Software Architecture Skills Pack

Este paquete contiene **3 skills estructuradas (custom prompts / agent instructions)** diseñadas para asistir a alumnos, docentes y arquitectos de software en el modelado, evaluación y priorización de atributos de calidad y requerimientos arquitectónicamente significativos (**ASRs**), basándose estrictamente en los estándares del **Software Engineering Institute (SEI)** y en el libro *Software Architecture in Practice* (4.ª Edición, Bass, Clements, Kazman).

---

## 🆕 Filosofía de diseño de esta versión: "Grillar" antes de resolver

### El problema que se buscó resolver

La primera versión de estas 3 skills, ante un requerimiento incompleto o ambiguo, **completaba los huecos por su cuenta** ("asumí condiciones operativas estándar razonables") y avanzaba directo a entregar el escenario, el diagnóstico o el árbol de utilidad terminado. Esto es cómodo, pero tiene dos problemas:

1. **Le quita al alumno la práctica más importante del método.** El valor real del ATAM y de los escenarios de calidad no es la plantilla de 6 partes en sí, sino el ejercicio de **elicitación**: saber qué preguntarle a un stakeholder para no inventar contexto de negocio en su nombre. Si la skill completa todo sola, el alumno nunca practica esa habilidad.
2. **Mezcla decisiones técnicas con decisiones de negocio.** Cosas como "¿qué tan crítico es este escenario para el negocio?" o "¿qué umbral de disponibilidad es aceptable?" no son inferencias técnicas razonables: son decisiones que le corresponden al stakeholder, no al arquitecto ni mucho menos al modelo.

Esto está anclado en la propia bibliografía del pack: el Cap. 19.4 describe que un utility tree útil se construye interviewing a los stakeholders, y el Cap. 21.5 (ATAM) formaliza el rol de **Questioner**, cuyo trabajo específico durante la evaluación es hacer preguntas incisivas sobre atributos de calidad — no completar la información con supuestos propios.

### La solución: fase obligatoria de elicitación ("Grilling")

Las 3 skills ahora incorporan, como paso obligatorio previo a cualquier entrega final, una fase de preguntas. Las reglas de esta fase son las mismas en las 3 skills, para que el comportamiento sea predecible:

| Regla | Qué significa en la práctica |
| :--- | :--- |
| **Nunca asumir en silencio** | Si falta o es ambiguo cualquiera de los 6 elementos de un escenario (o los criterios de negocio de un utility tree), la skill debe listar preguntas concretas y **esperar la respuesta del usuario** antes de generar la salida final. |
| **Vía de escape explícita (opt-out)** | Si el usuario contesta algo como "asumí lo que te parezca" o "dale, avanzá vos", ahí sí se habilita el modo de inferencia razonable — pero documentada (ver más abajo). Esto evita loops infinitos y respeta a quien ya sabe lo que quiere y no necesita que le pregunten. |
| **Preguntas acotadas y priorizadas** | Máximo 5 preguntas por ronda, agrupadas por lo que más cambia el resultado (ej. "¿qué constituye una falla — caída total o degradación parcial?" pesa mucho más que un detalle cosmético). No es un interrogatorio infinito. |
| **Distinguir "falta un dato" de "el dato es una decisión de negocio"** | La Importancia de Negocio (H/M/L) en el Utility Tree, o el umbral de una Response Measure, **nunca** se completan con una inferencia técnica "razonable" — eso le corresponde al usuario. La Dificultad/Riesgo arquitectónico sí se puede estimar con criterio experto, pero también amerita preguntar si falta contexto técnico (stack, restricciones existentes). |

Cada skill aplica esto a su propio contexto:

* **Generator:** antes de construir el escenario de 6 partes, pregunta por lo que falta del estímulo, el entorno o la medida de respuesta.
* **Checker:** distingue entre un problema de **redacción** (lo puede corregir directo, con su criterio de auditor) y un vacío de **contexto de negocio** (ahí pregunta antes de proponer la corrección).
* **Utility Tree Builder:** separa explícitamente la pregunta de Importancia de Negocio (siempre se pregunta primero) de la de Riesgo Arquitectónico (se puede estimar, pero mejor con contexto), y entrega el árbol en dos pasadas cuando hace falta elicitar: primero la estructura jerárquica para validar cobertura, después la matriz de priorización.

### El marcador `[SUPUESTO]`

Cuando el usuario autoriza a la skill a asumir (en vez de responder las preguntas), **todo dato completado por inferencia debe marcarse explícitamente** con la etiqueta `[SUPUESTO]` en la tabla o matriz final, y nunca mezclarse en silencio con los datos confirmados por el usuario. Esto hace que el resultado final sea siempre **auditable**: cualquiera que lea el escenario, el reporte o el árbol puede distinguir de un vistazo qué fue decisión del usuario y qué fue inferencia del modelo.

### La frase de opt-out estandarizada

Las 3 skills cierran su ronda de preguntas con una variación de la misma frase, para que el comportamiento sea consistente y predecible en las tres:

> *"Si preferís que asuma valores razonables [o: que asigne las prioridades yo mismo a criterio experto], decímelo y avanzo igual, dejando explícito qué asumí."*

---

## 📁 Estructura del Repositorio

```text
skills-arquitectura-sei/
├── README.md
├── skills/
│   ├── 01-sei-scenario-generator/
│   │   ├── SKILL.md
│   │   └── resources/
│   │       └── intro_QAS.pdf, material_QAS.pdf
│   ├── 02-sei-scenario-checker/
│   │   ├── SKILL.md
│   │   └── resources/
│   │       └── intro_QAS.pdf, material_QAS.pdf
│   └── 03-utility-tree-builder/
│       ├── SKILL.md
│       └── resources/
│           └── intro_UT.pdf, material_UT.pdf
└── test_cases/
    ├── test_generator.md
    ├── test_checker.md
    └── test_utility_tree.md
```

## Las 3 skills

1. **Quality Attribute Scenario Generator** (`01-sei-scenario-generator`) — transforma un requerimiento informal en un escenario formal de 6 partes (Source, Stimulus, Artifact, Environment, Response, Response Measure), preguntando antes de asumir cualquier dato ambiguo, con métricas obligatoriamente cuantitativas.
2. **Quality Attribute Scenario Checker** (`02-sei-scenario-checker`) — audita un escenario existente contra las 6 partes del estándar SEI, detecta partes faltantes o ambiguas, y pregunta por contexto de negocio antes de proponer la corrección (nunca lo asume en silencio).
3. **Utility Tree Builder** (`03-utility-tree-builder`) — arma el árbol de utilidad jerárquico (Atributo → Sub-atributo → Escenario) siguiendo ATAM, y su matriz de priorización H/M/L, elicitando primero cuáles escenarios son "no negociables" para el negocio antes de asignar cualquier prioridad.

## Test cases

Los `test_cases/*.md` fueron actualizados para documentar el flujo completo de dos pasos que ahora se espera de cada skill:

1. **Paso A — Elicitación:** la skill recibe un pedido incompleto y responde con preguntas concretas (máx. 5) en vez de resolver directo, cerrando con la frase de opt-out.
2. **Paso B — Entrega final:** una vez que el usuario responde (o autoriza a asumir), la skill entrega el escenario / reporte / árbol completo, marcando con `[SUPUESTO]` todo lo que no fue confirmado explícitamente.

Esto sirve tanto para verificar que la skill se comporta como se espera, como para que quien evalúe el pack (docente, revisor) tenga un ejemplo concreto y documentado del comportamiento de "grilling" en acción.
