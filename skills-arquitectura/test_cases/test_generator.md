\# Test Case 1: Generador de Escenarios (01-sei-scenario-generator)



\## 1. Entrada (User Prompt)

> "Generame un escenario de calidad en formato SEI de 6 partes para un sistema bancario enfocado en la disponibilidad frente a la caída de la base de datos principal."



\## 2. Salida Esperada (Expected Output)

La skill debe generar un escenario estructurado estrictamente con las 6 partes estándar del SEI:



\* \*\*Fuente del estímulo (Source):\*\* Servidor/Instancia de la base de datos principal.

\* \*\*Estímulo (Stimulus):\*\* Fallo crítico no planificado por falla de hardware o pérdida de conectividad de red en el nodo primario.

\* \*\*Artefacto (Artifact):\*\* Módulo de persistencia / Base de datos relacional del sistema bancario.

\* \*\*Entorno (Environment):\*\* Operación normal en horario de pico transaccional.

\* \*\*Respuesta (Response):\*\* El sistema detecta la falla, activa el mecanismo de conmutación por error (failover) al nodo secundario sin perder transacciones confirmadas e informa el evento a los administradores.

\* \*\*Medida de la respuesta (Response Measure):\*\* Tiempo de recuperación (MTTR) menor a 30 segundos; 0% de pérdida de transacciones confirmadas (RPO = 0).

