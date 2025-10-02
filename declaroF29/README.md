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
    M --> N["<b>conectaBD_DTE</b><br/><a href='https://www.plantuml.com/plantuml/svg/PLD1Rjim4Bpp5GDT8W694HVenOABrBA26d3jfdQ1tegDjBRPqgH2KadGF-NK9_XZ1IKhiEMB175dTsU6epldoVfwhr0OpOMdoVJNT9qBBxrYtAlwjq79sDIwa8T_keSIJRSOPKOxRsjfOMjF85livBE1a-MWUYb34xRiMJ_7qPVbrpnAKZ6QQS_QamKzMcdVUm9sOohMgH1oWxWxrmRyAftd17x76l7gy9O8O3JRLrRkfGLRQooYXO5ZL7LfZfCx5l5qdITH6dei-zfgnCCaV3flAi7ACUA5QMTgMKXIyYzPh3ZNXT7U6enncmhMfTm8ORbYyW4yPxPGXpVDX9BLkP8jUzUi_CwyhnI5YLUZArJ6Wbr5XJHDsRc2z0Otdv1x-LIpfskusROcTGsNKScQCgFvLPfW312iwP0OZz529hKhgAIUHS3eJCGmRGuVBTCV0RI2MZrusKd5YBL1lhnFsYiuRHvZs9iU43s60RRuCPzVykYCl_cGj2GQxu5Jzu7HDyiLMRBeAs-g-Syym-fXZcovMEJP6eF109_NQ4FPWXf_ca2i7YvvNCOcN9PxKWKDmjEKtCObxU17ucUGhdZKq5TnkYJAslycX1AAC277cAxpgB_Wzd9eSptT-oocxsv-FCbn6yyxrcMzL_y1'>Ver subflujo</a>"]

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
    X --> Y["<b>cargaArchivoAlertas</b><br/><a href='https://www.plantuml.com/plantuml/svg/VP5FJyCm3CNl-HG-Rc93dU2oJKYR60SaJXEtQKAcSJkZDAaSj_pvz2XjDmqqk2Nsoy_FBwkeADfK3dAK4jUI7xWDQqUY68soEe8DOobO8LY2mZLl0QQNrAEnCHtDcCMZvvpHyHSAj2YChuxYqYp03sAuWwoxRwdag1BY4x4DGzsy7zWHZA0eIUF8iIUSm6sMPHCewW4nXh4105YSCK_7AvWj--vzg1a5Qk6A94IO9--OAmb5GB1DLNsUfBubKPQ-2fYylqYZG__XGmL9mBOfYixLRhx_EUSCFikcivi1ekYEb7NaqlUv93OWn0rgYBtrtN65_RNTDh_VsFPlURjfTzd-mf0q-vzdpvqryhOBFNrUbS9Y0GsABgsAGwgrX9mYMenBOuIq4N-At4GDjLcHjqtblW40)'>Ver subflujo</a>"]
    Y --> AA["<b>cargaArchivoAtributos</b><br/><a href='https://.../cargaArchivoAtributos.svg' target='_blank'>Ver subflujo</a>"]
    AA --> AB["<b>poblarDatos</b><br/><a href='https://.../poblarDatos.svg' target='_blank'>Ver subflujo</a>"]

    AB --> AC{lEscen == 10?}
    AC -->|Sí| AD["<b>nominaAnotar(1-4)</b><br/><a href='https://.../nominaAnotar.svg' target='_blank'>Ver subflujo</a>"] --> V
    AC -->|No| AE{lEscen == 7?}
    AE -->|Sí| AF["<b>nominaAnotar(2-3)</b><br/><a href='https://.../nominaAnotar.svg' target='_blank'>Ver subflujo</a>"] --> V
    AE -->|No| AG["<b>nominaAnotar(lEscen)</b><br/><a href='https://.../nominaAnotar.svg' target='_blank'>Ver subflujo</a>"] --> V

    V --> Z[Stop]
