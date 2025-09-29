# Diagrama de Flujo - bajaObligados

```mermaid
flowchart TD
    A[Inicio] --> B[Validar parámetros]
    B -->|OK| C[ejecutaRemoto]
    B -->|Error| Z[Fin con error]

    C --> D[copiaRemota]
    D --> E[mismoLargo]
    E --> F[obligadoSinF29]
    F --> G[copiaHaciaPluton]
    G --> H[ejecutaRemotoAtrib]
    H --> I[recuperaAnotados]
    I --> J[recuperaAtributos]

    J --> K{Escenario}
    K -->|10| L[escenario10]
    K -->|7| M[escenario7]
    K -->|Otros| N[escenarioVarios]

    L --> O[rcpPlutonAnotar]
    M --> O
    N --> O

    O --> P[Respaldo archivos]
    P --> Q[Enviar correos OK/ERROR]
    Q --> R[Fin]

