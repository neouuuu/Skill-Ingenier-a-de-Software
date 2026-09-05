\# Test Case 2: Chequeador de Escenarios (02-sei-scenario-checker)



\## 1. Entrada (User Prompt)

> "Revisá y corregí este escenario de calidad: 'El sistema tiene que ser rápido cuando entran muchos usuarios a la plataforma'."



\## 2. Salida Esperada (Expected Output)

La skill debe detectar los problemas de imprecisión del escenario ambiguo y reescribirlo de forma cuantitativa:



\### Detección de Faltantes y Ambigüedades

\* \*\*Faltan partes clave:\*\* No especifica la fuente, el entorno ni la medida de respuesta exacta.

\* \*\*Ambigüedad:\*\* Palabras como "rápido" y "muchos usuarios" no son medibles ni verificables en ingeniería de software.



\### Escenario Corregido (SEI de 6 partes)

\* \*\*Fuente del estímulo:\*\* 5.000 usuarios concurrentes realizando peticiones simultáneas.

\* \*\*Estímulo:\*\* Solicitud masiva de carga de la página principal.

\* \*\*Artefacto:\*\* Servidor web / Frontend de la plataforma.

\* \*\*Entorno:\*\* Operación normal durante un evento de alta demanda (pico de tráfico).

\* \*\*Respuesta:\*\* El servidor procesa y sirve las peticiones entrantes balanceando la carga entre las instancias.

\* \*\*Medida de la respuesta:\*\* Tiempo de respuesta al percentil 95 (p95) $< 200\\text{ ms}$; tasa de error $< 0.01\\%$.

