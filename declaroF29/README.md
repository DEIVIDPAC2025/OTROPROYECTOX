# Flujo de Proceso: Anotacion masiva de 4310-DTE

Nombre proceso: Programa Pro\*C - DeclaroF29.pc

Descripcion:DeclaroF29

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del programa `DeclaroF29`.

# Flujo principal DeclaroF29

```mermaid
flowchart TD

    A[Start] --> B[Verificar parámetros argc != 7?]
    B -->|Sí| C[Imprimir versión]
    C --> D["<b>modo_uso</b><br/><a href='https://.../modo_uso.svg' target='_blank'>Ver subflujo</a>"]
    D --> Z[Stop]

    B -->|No| E["Asignar lPeriodo = argv[1]"]
    E --> F{lPeriodo < 201501?}
    F -->|Sí| G[Error periodo inválido] --> Z
    F -->|No| H["abrir archivos: argv[2], argv[3], argv[4]"]

    H --> I[Asignar lEscen, Debug]
    I --> J{"lEscen válido (1-10)?"}
    J -->|No| K[Error escenario inválido] --> Z
    J -->|Sí| L["Crear archivos salida (SinF29, Anotar, FiltroCSEI)"]

    L --> M["<b>conectaBD</b><br/><a href='https://www.plantuml.com/plantuml/svg/RLD1Rjim4Bph5GDT8W694HVeHOABmAg26d2Tfcw1NZVIscPBaygIIeB-AQS-mHyBADc1BVT2WTpPuUnmTECyYM-t6fKrN7cQVewyyffngzlV5ZLZrPfAxVwP8qJKTKLPOOtpqYg1j9v0KctKauLJzQXvhaC3rkpPF2NnbxklPPpcKJOpdeqd0Js8alUUW5tPXaqUHMg5v71kBFX5ESyf_8ODakNkDOs0RBPjH6sLW4Mi85vOE4RJrdRFl5SHvm4jx5inICPfs3flcuYrOoGBsxCPLIdIwYy9bboQoXel5XDSvn6RMgsYIBXXyW4yPnRetQjXGitwT8OrUzTT-PrvssWAZ1VP1HehODTGfMnNTguYiyBL9vHUFRRiwH9kjcv9Ny8LLBEXmXf-KJPO0WHJ3aXC9kWXqzPLLDF0720x6MASTuSFmlGd0lg1-ddml56QaHYBykusxSq_RfvWF60FY87205lydC_FTHoCl_gGzY8wxu5Zzu7ict13GeBXv5sr_5KMMDxFKTmj5cNn0wFHg2zrhdG1MDwVttuUa_14xb5ND0ghhJa_0FT2_rlSQnwgFgQFY_xl2F639ap9SJmalpudx9xYy3s9vBjp7uyosqVnXatTRlKR'>Ver subflujo</a>"]
    M --> N["<b>conectaBD_DTE</b><br/><a href='https://.../conectaBD_DTE.svg' target='_blank'>Ver subflujo</a>"]

    N --> O[Reservar memoria datAux]

    O --> P{lEscen == 5?}
    P -->|Sí| Q[Leer fpFolios en bucle]
    Q --> R["<b>sqlExisteF29</b><br/><a href='https://.../sqlExisteF29.svg' target='_blank'>Ver subflujo</a>"]
    R --> S[Marcar N o S]
    S --> T[Imprimir estadísticas]
    T --> U[Generar archivo SinF29]
    U --> V[Imprimir versión y parámetros] --> Z

    P -->|No| W{"lEscen ∈ [1,2,3,4,7,10]?"}
    W -->|No| V
    W -->|Sí| X[Leer contribuyentes de fpFolios]
    X --> Y["<b>cargaArchivoAlertas</b><br/><a href='https://.../cargaArchivoAlertas.svg' target='_blank'>Ver subflujo</a>"]
    Y --> AA["<b>cargaArchivoAtributos</b><br/><a href='https://.../cargaArchivoAtributos.svg' target='_blank'>Ver subflujo</a>"]
    AA --> AB["<b>poblarDatos</b><br/><a href='https://.../poblarDatos.svg' target='_blank'>Ver subflujo</a>"]

    AB --> AC{lEscen == 10?}
    AC -->|Sí| AD["<b>nominaAnotar(1-4)</b><br/><a href='https://.../nominaAnotar.svg' target='_blank'>Ver subflujo</a>"] --> V
    AC -->|No| AE{lEscen == 7?}
    AE -->|Sí| AF["<b>nominaAnotar(2-3)</b><br/><a href='https://.../nominaAnotar.svg' target='_blank'>Ver subflujo</a>"] --> V
    AE -->|No| AG["<b>nominaAnotar(lEscen)</b><br/><a href='https://.../nominaAnotar.svg' target='_blank'>Ver subflujo</a>"] --> V

    V --> Z[Stop]
