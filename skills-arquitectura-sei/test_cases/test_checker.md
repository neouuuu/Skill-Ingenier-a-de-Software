# Test Case 2: Chequeador de Escenarios (02-sei-scenario-checker)

## 1. Entrada (User Prompt)
> "Revisá y corregí este escenario de calidad: 'El sistema tiene que ser rápido cuando entran muchos usuarios a la plataforma'."

## 2. Salida Esperada — Paso A: Diagnóstico + Elicitación (Grilling)

La skill primero audita el escenario ambiguo, y como los vacíos detectados requieren contexto de negocio (no solo redacción), **no debe proponer la corrección todavía**:

### Detección de Faltantes y Ambigüedades
* **Faltan partes clave:** No especifica la fuente, el entorno ni la medida de respuesta exacta.
* **Ambigüedad:** Palabras como "rápido" y "muchos usuarios" no son medibles ni verificables en ingeniería de software.

### Antes de proponer la corrección, necesito confirmar:
1. ¿Cuántos usuarios concurrentes aproximadamente constituyen "muchos" para este sistema (orden de magnitud)?
2. ¿Qué tiempo de respuesta consideran aceptable, y para qué percentil (p95, p99)?
3. ¿Qué tasa de error es tolerable en ese pico de carga?
4. ¿Esto ocurre en operación normal con picos de tráfico, o en un evento particular (ej. lanzamiento, promoción)?

Si preferís que proponga una corrección con supuestos razonables en vez de preguntar, decímelo y avanzo, marcando explícitamente cada supuesto.

## 3. Entrada de seguimiento (User Prompt)
> "Asumí un caso típico de e-commerce en promoción."

## 4. Salida Esperada — Paso B: Reporte de Auditoría completo

### Reporte de Auditoría de Escenario
**Estado General:** AMBIGUO

#### 1. Evaluación por Componente (6 Partes)
* **1. Source of Stimulus:** FALTANTE — No se especifica quién genera la carga.
* **2. Stimulus:** AMBIGUO — "Muchos usuarios" no es cuantificable.
* **3. Artifact:** AMBIGUO — "El sistema" es demasiado genérico.
* **4. Environment:** FALTANTE — No se indica el estado operativo.
* **5. Response:** FALTANTE — No se describe la acción del sistema.
* **6. Response Measure:** AMBIGUO — "Rápido" no es medible.

#### 2. Diagnóstico y Vicios Encontrados
El escenario mezcla estímulo y medida de respuesta en una sola oración vaga, sin diferenciar las 6 partes formales, y usa adjetivos subjetivos en lugar de umbrales verificables.

#### 3. Propuesta de Escenario Corregido y Completo
**Atributo de Calidad:** Performance

| Parte del Escenario | Valor Propuesto / Corregido |
| :--- | :--- |
| **1. Source of Stimulus** | Usuarios concurrentes realizando peticiones simultáneas |
| **2. Stimulus** | Solicitud masiva de carga de la página principal durante una promoción |
| **3. Artifact** | Servidor web / Frontend de la plataforma |
| **4. Environment** | Operación normal durante un evento de alta demanda (pico de tráfico por promoción) |
| **5. Response** | El servidor procesa y sirve las peticiones entrantes balanceando la carga entre las instancias |
| **6. Response Measure** | Tiempo de respuesta al percentil 95 (p95) < 200 ms; tasa de error < 0.01% |

**Supuestos realizados:**
* **[SUPUESTO]** Volumen de "5.000 usuarios concurrentes" tomado como orden de magnitud típico de una promoción de e-commerce, no confirmado por el usuario.
* **[SUPUESTO]** Umbrales de p95 < 200 ms y tasa de error < 0.01%, tomados como valores típicos de la industria, no confirmados por el usuario.
