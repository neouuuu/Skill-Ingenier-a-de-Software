# Test Case 1: Generador de Escenarios (01-sei-scenario-generator)

## 1. Entrada (User Prompt)
> "Generame un escenario de calidad en formato SEI de 6 partes para un sistema bancario enfocado en la disponibilidad frente a la caída de la base de datos principal."

## 2. Salida Esperada — Paso A: Elicitación (Grilling)

Como el pedido no especifica umbrales ni el estado operativo del sistema, la skill **no debe generar el escenario todavía**. Debe responder primero algo equivalente a:

> Antes de armar el escenario formal, necesito confirmar algunos puntos:
>
> 1. Cuando cae la base de datos principal, ¿existe un nodo secundario para failover, o el sistema debe operar en modo degradado?
> 2. ¿Qué tiempo máximo de recuperación (MTTR) es aceptable para el negocio?
> 3. ¿Es tolerable perder transacciones no confirmadas, o el requisito es RPO = 0?
> 4. ¿En qué horario/contexto operativo debe evaluarse esto — pico transaccional, operación normal, ambos?
>
> Si preferís que asuma valores razonables y típicos de la industria, decímelo y avanzo igual, dejando explícito qué asumí.

## 3. Entrada de seguimiento (User Prompt)
> "Dale, asumí valores típicos de un banco."

## 4. Salida Esperada — Paso B: Escenario completo

La skill debe generar el escenario estructurado con las 6 partes estándar del SEI, marcando explícitamente los supuestos:

### Escenario de Calidad: Failover de Base de Datos Principal
**Atributo de Calidad:** Disponibilidad

| Parte del Escenario | Descripción Detallada |
| :--- | :--- |
| **1. Source of Stimulus** | Servidor/Instancia de la base de datos principal |
| **2. Stimulus** | Fallo crítico no planificado por falla de hardware o pérdida de conectividad de red en el nodo primario |
| **3. Artifact** | Módulo de persistencia / Base de datos relacional del sistema bancario |
| **4. Environment** | Operación normal en horario de pico transaccional |
| **5. Response** | El sistema detecta la falla, activa el mecanismo de conmutación por error (failover) al nodo secundario sin perder transacciones confirmadas e informa el evento a los administradores |
| **6. Response Measure** | Tiempo de recuperación (MTTR) menor a 30 segundos; 0% de pérdida de transacciones confirmadas (RPO = 0) |

**Supuestos realizados:**
* **[SUPUESTO]** Existencia de nodo secundario de failover (no confirmado explícitamente por el usuario).
* **[SUPUESTO]** MTTR < 30 s y RPO = 0, tomados como valores típicos de la industria bancaria, no confirmados por el usuario.
* **[SUPUESTO]** Entorno de "horario de pico transaccional", asumido como el escenario más exigente y relevante para un banco.
