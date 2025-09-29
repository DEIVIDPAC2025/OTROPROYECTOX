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


```markdown
- [ejecutaRemoto](diagrams/ejecutaRemoto.svg)
- [copiaRemota](diagrams/copiaRemota.svg)
- [mismoLargo](diagrams/mismoLargo.svg)
- [obligadoSinF29](diagrams/obligadoSinF29.svg)
- [copiaHaciaPluton](diagrams/copiaHaciaPluton.svg)
- [ejecutaRemotoAtrib](diagrams/ejecutaRemotoAtrib.svg)
- [recuperaAnotados](diagrams/recuperaAnotados.svg)
- [recuperaAtributos](diagrams/recuperaAtributos.svg)
- [rcpPlutonAnotar](diagrams/rcpPlutonAnotar.svg)
- [escenario10](diagrams/escenario10.svg)
- [escenario7](diagrams/escenario7.svg)
- [escenarioVarios](diagrams/escenarioVarios.svg)
