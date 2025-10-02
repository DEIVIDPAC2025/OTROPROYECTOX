# Flujo de Proceso: Anotacion 4310

Nombre Shell: Proce4310.sh

Descripcion: El proceso 4310 Permite crear un archivo con contribuyentes con la anotacion 4310 de acuerdo a un periodo tributario. Estos contribuyetes anotados con la 4310 se forman a apartir del listado de obligados generados en el proceso anterior bajaObligado.sh.
Se exceptuan de la anotacion 4310 aquellos contribuyente que tuvieron una anotacion (73), (543) o si declaro un F29 en el periodo de procesamiento de los obligados o si tiene una declaracion F29 vigente. Estos filtros bajan el universo de anotyados con la 4310. La salida del proceso es un archivo de anotados que se envia a la mauina de docminio RIAC(PLUTON), para el procesamiento posterior de esas anotaciones en el dominio RIAC. 
Tanto para obtener los contribuyentes obligados como para anotar los contribuynetes obligados con la anotacion 4310 esto se ejecuta en la mauina pluton (dominIo de RIAC) 

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `bajaObligados`.

# Flujo principal - Programa Pro\*C (DeclarF29)

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

    L --> M["<b>conectaBD</b><br/><a href='https://.../conectaBD.svg' target='_blank'>Ver subflujo</a>"]
    M --> N["<b>conectaBD_DTE</b><br/><a href='https://.../conectaBD_DTE.svg' target='_blank'>Ver subflujo</a>"]

    N --> O[Reservar memoria datAux]

    O --> P{lEscen == 5?}
    P -->|Sí| Q[Leer fpFolios en bucle]
    Q --> R["<b>sqlExisteF29</b><br/><a href='https://.../sqlExisteF29.svg' target='_blank'>Ver subflujo</a>"]
    R --> S[Marcar N o S]
    S --> T[Imprimir estadísticas]
    T --> U[Generar archivo SinF29]
    U --> V[Imprimir versión y parámetros] --> Z

    P -->|No| W{lEscen ∈ [1,2,3,4,7,10]?}
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
