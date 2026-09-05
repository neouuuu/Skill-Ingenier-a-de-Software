\# Test Case 3: Utility Tree Builder (03-utility-tree-builder)



\## 1. Entrada (User Prompt)

> "Armá un Árbol de Utilidad (Utility Tree) para un e-commerce de alta escala considerando Rendimiento, Disponibilidad y Seguridad."



\## 2. Salida Esperada (Expected Output)

La skill debe estructurar el árbol jerárquico y clasificar las hojas con la tupla de priorización $(H, M, L)$:



\### Árbol de Utilidad: Plataforma E-commerce de Alta Escala



\#### Estructura Jerárquica

\* \*\*Utilidad Global:\*\* Plataforma de comercio electrónico de alta visibilidad y procesamiento de pagos en tiempo real.

&#x20; \* \*\*Rendimiento\*\*

&#x20;   \* \*\*Latencia de Búsqueda:\*\* Durante la búsqueda de productos en horario pico, el catálogo responde en $t < 150\\text{ ms}$ (p95). \*\*(Imp: H, Dif: M)\*\*

&#x20;   \* \*\*Caudal de Procesamiento (Throughput):\*\* El checkout soporta $10.000\\text{ transacciones/minuto}$ sin degradar tiempos de respuesta. \*\*(Imp: H, Dif: H)\*\*

&#x20; \* \*\*Disponibilidad\*\*

&#x20;   \* \*\*Tolerancia a Fallas:\*\* Ante la caída de una zona de disponibilidad, el tráfico conmuta automáticamente en $t < 10\\text{ s}$. \*\*(Imp: H, Dif: H)\*\*

&#x20; \* \*\*Seguridad\*\*

&#x20;   \* \*\*Integridad de Datos:\*\* Frente a intentos de SQL Injection en el formulario de pago, el filtro WAF bloquea las peticiones sospechosas y registra el intento sin afectar la transacción. \*\*(Imp: H, Dif: L)\*\*



\#### Matriz de Priorización (ASRs Críticos)



| ID | Atributo | Sub-atributo | Escenario de Calidad Cuantificado | Imp. Negocio | Dif. Arquitectónica | Prioridad Global |

| :--- | :--- | :--- | :--- | :---: | :---: | :---: |

| \*\*ES-01\*\* | Rendimiento | Throughput | Checkout soporta 10.000 trans/min sin degradar la respuesta. | \*\*H\*\* | \*\*H\*\* | \*\*CRÍTICA (H,H)\*\* |

| \*\*ES-02\*\* | Disponibilidad | Failover | Conmutación entre zonas de disponibilidad en $t < 10\\text{ s}$. | \*\*H\*\* | \*\*H\*\* | \*\*CRÍTICA (H,H)\*\* |

| \*\*ES-03\*\* | Rendimiento | Latencia | Búsqueda de productos responde en $t < 150\\text{ ms}$ al p95. | \*\*H\*\* | \*\*M\*\* | \*\*Alta\*\* |

| \*\*ES-04\*\* | Seguridad | WAF / Filtro | Bloqueo de ataques SQLi sin interrumpir peticiones legítimas. | \*\*H\*\* | \*\*L\*\* | \*\*Media\*\* |

