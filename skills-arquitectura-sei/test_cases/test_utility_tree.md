# Test Case 3: Utility Tree Builder (03-utility-tree-builder)

## 1. Entrada (User Prompt)
> "Armá un Árbol de Utilidad (Utility Tree) para un e-commerce de alta escala considerando Rendimiento, Disponibilidad y Seguridad."

## 2. Salida Esperada — Paso A: Estructura jerárquica + Elicitación de prioridades

El objetivo de negocio general ya está dado ("e-commerce de alta escala"), así que la skill puede construir directamente la estructura jerárquica. Pero como no hay criterios de priorización de negocio, **no debe asignar la matriz H/M/L todavía**:

### Árbol de Utilidad: Plataforma E-commerce de Alta Escala (estructura preliminar)

* **Utilidad Global:** Plataforma de comercio electrónico de alta visibilidad y procesamiento de pagos en tiempo real.
  * **Rendimiento**
    * **Latencia de Búsqueda:** Durante la búsqueda de productos en horario pico, el catálogo responde en $t < 150\text{ ms}$ (p95).
    * **Caudal de Procesamiento (Throughput):** El checkout soporta $10.000\text{ transacciones/minuto}$ sin degradar tiempos de respuesta.
  * **Disponibilidad**
    * **Tolerancia a Fallas:** Ante la caída de una zona de disponibilidad, el tráfico conmuta automáticamente en $t < 10\text{ s}$.
  * **Seguridad**
    * **Integridad de Datos:** Frente a intentos de SQL Injection en el formulario de pago, el filtro WAF bloquea las peticiones sospechosas y registra el intento sin afectar la transacción.

### Antes de priorizar, necesito confirmar:
1. De estos 4 escenarios, ¿cuáles considerás "no negociables" (H) para el lanzamiento, cuáles son importantes pero tolerables (M), y cuáles son deseables nomás (L)?
2. ¿Hay restricciones de infraestructura ya definidas (ej. multi-AZ ya implementado, WAF ya contratado) que deba considerar para estimar el riesgo arquitectónico de cada uno?

Si preferís que asigne las prioridades yo mismo a criterio experto, decímelo y avanzo, marcando cada tupla asumida como [SUPUESTO].

## 3. Entrada de seguimiento (User Prompt)
> "Asigná vos las prioridades, a tu criterio de experto."

## 4. Salida Esperada — Paso B: Árbol completo con matriz de priorización

### Árbol de Utilidad: Plataforma E-commerce de Alta Escala

#### 1. Estructura Jerárquica del Árbol (Top-Down)
* **Utilidad Global:** Plataforma de comercio electrónico de alta visibilidad y procesamiento de pagos en tiempo real.
  * **Rendimiento**
    * **Latencia de Búsqueda:** Durante la búsqueda de productos en horario pico, el catálogo responde en $t < 150\text{ ms}$ (p95). **(Imp: H, Dif: M)**
    * **Caudal de Procesamiento (Throughput):** El checkout soporta $10.000\text{ transacciones/minuto}$ sin degradar tiempos de respuesta. **(Imp: H, Dif: H)**
  * **Disponibilidad**
    * **Tolerancia a Fallas:** Ante la caída de una zona de disponibilidad, el tráfico conmuta automáticamente en $t < 10\text{ s}$. **(Imp: H, Dif: H)**
  * **Seguridad**
    * **Integridad de Datos:** Frente a intentos de SQL Injection en el formulario de pago, el filtro WAF bloquea las peticiones sospechosas y registra el intento sin afectar la transacción. **(Imp: H, Dif: L)**

#### 2. Matriz de Priorización (ASRs Críticos)

| ID | Atributo | Sub-atributo | Escenario de Calidad Cuantificado | Imp. Negocio | Dif. Arquitectónica | Prioridad Global |
| :--- | :--- | :--- | :--- | :---: | :---: | :---: |
| **ES-01** | Rendimiento | Throughput | Checkout soporta 10.000 trans/min sin degradar la respuesta. | **H** | **H** | **CRÍTICA (H,H)** |
| **ES-02** | Disponibilidad | Failover | Conmutación entre zonas de disponibilidad en $t < 10\text{ s}$. | **H** | **H** | **CRÍTICA (H,H)** |
| **ES-03** | Rendimiento | Latencia | Búsqueda de productos responde en $t < 150\text{ ms}$ al p95. | **H** | **M** | **Alta** |
| **ES-04** | Seguridad | WAF / Filtro | Bloqueo de ataques SQLi sin interrumpir peticiones legítimas. | **H** | **L** | **Media** |

**Análisis de Riesgos Arquitectónicos (H, H):**
Los escenarios ES-01 y ES-02 son los ASRs más críticos: un fallo en el throughput de checkout o en el failover de disponibilidad tiene impacto directo en ingresos y continuidad del negocio, y ambos presentan alto riesgo arquitectónico por depender de mecanismos de escalado y conmutación complejos.

**Supuestos realizados:**
* **[SUPUESTO]** Todas las tuplas de Importancia de Negocio (H) fueron asignadas a criterio experto, no confirmadas por el usuario, por autorización explícita suya.
* **[SUPUESTO]** Las tuplas de Dificultad/Riesgo se estimaron sin conocer el stack tecnológico real del sistema, asumiendo una arquitectura cloud estándar con capacidad de auto-escalado.
