# 📊 Flujo de Proceso: bajaObligados

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `bajaObligados`.

---

## 🔹 Flujo Principal

```mermaid
flowchart TD
    A([Inicio]) --> B[Validar parámetros]

    B -->|OK| C[["ejecutaRemoto<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70000'>Ver subflujo</a>"]]
    B -->|Error| Z([Fin con error])

    C --> D[["copiaRemota<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70001'>Ver subflujo</a>"]]
    D --> E[["mismoLargo<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70002'>Ver subflujo</a>"]]
    E --> F[["obligadoSinF29<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70003'>Ver subflujo</a>"]]
    F --> G[["copiaHaciaPluton<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70004'>Ver subflujo</a>"]]
    G --> H[["ejecutaRemotoAtrib<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70005'>Ver subflujo</a>"]]
    H --> I[["recuperaAnotados<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70006'>Ver subflujo</a>"]]
    I --> J[["recuperaAtributos<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70007'>Ver subflujo</a>"]]

    J --> K{Escenario}
    K -->|10| L[["escenario10<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70008'>Ver subflujo</a>"]]
    K -->|7| M[["escenario7<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa70009'>Ver subflujo</a>"]]
    K -->|Otros| N[["escenarioVarios<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa7000A'>Ver subflujo</a>"]]

    L --> O[["rcpPlutonAnotar<br/><a href='https://www.plantuml.com/plantuml/svg/SoWkIImgAStDuNBCoKnELT3AJ4vLqBLJ24ZDoSa7000B'>Ver subflujo</a>"]]
    M --> O
    N --> O

    O --> P[Respaldo archivos]
    P --> Q[Enviar correos OK/ERROR]
    Q --> R([Fin])

