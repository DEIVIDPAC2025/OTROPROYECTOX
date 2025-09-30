# Flujo de Proceso: Anotacion 4310

Nombre Shell: Proce4310.sh

Descripcion: El proceso 4310 Permite crear un archivo con contribuyentes con la anotacion 4310 de acuerdo a un periodo tributario. Estos contribuyetes anotados con la 4310 se forman a apartir del listado de obligados generados en el proceso anterior bajaObligado.sh.
Se exceptuan de la anotacion 4310 aquellos contribuyente que tuvieron una anotacion (73), (543) o si declaro un F29 en el periodo de procesamiento de los obligados o si tiene una declaracion F29 vigente. Estos filtros bajan el universo de anotyados con la 4310. La salida del proceso es un archivo de anotados que se envia a la mauina de docminio RIAC(PLUTON), para el procesamiento posterior de esas anotaciones en el dominio RIAC. 
Tanto para obtener los contribuyentes obligados como para anotar los contribuynetes obligados con la anotacion 4310 esto se ejecuta en la mauina pluton (dominIo de RIAC) 

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `bajaObligados`.

---

# Flujo principal - Proceso Batch `proce4310.sh`

El siguiente diagrama representa el flujo principal en Mermaid.  
Cada nodo que corresponde a un **subflujo auxiliar** contiene un enlace al archivo `.svg` exportado desde PlantUML.

```mermaid
flowchart TD
    A[Inicio] --> B["Validar parámetros (nPeriodo, nEscenario)"]
    B --> C{¿Existen archivos de entrada?}
    C -- No --> D[Logs + enviar mail error]
    D --> Z1[Fin]

    C -- Sí --> E["Configurar entorno (Producción/Desarrollo)"]
    E --> F[Inicializar logs]

    F --> G[Revisa_SID_ULTIMA]
    G --> H{¿nObligados >= nNotNull?}
    H -- No --> I[Logs + enviar mail error]
    I --> Z2[Fin]
    H -- Sí --> J[Continuar]

    J --> K[Ejecutar Proceso]
    K --> L[Forzar anotación 7503 dummy]
    L --> M["Contar registros (7503, 73, 543)"]
    M --> N[Ejecutar Procesa4310 con archivos generados]

    N --> O{¿Error en Procesa4310?}
    O -- Sí --> P[Logs + mail error]
    P --> Z3[Fin]
    O -- No --> Q[Generar archivo AnotaMensual4310 si Escenario=2]
    Q --> R[Copiar y comprimir archivos de salida]

    R --> S[Enviar correo final con resultados]
    S --> T[MarcaUltPerProcesado]
    T --> U{¿Error en MarcaUltPerProcesado?}
    U -- Sí --> V[Logs + mail error]
    V --> Z4[Fin]

    U -- No --> W[Generar CTLFILE para revisión diferida]
    W --> X["Programar ejecución con at (20h después)"]
    X --> Z5[Fin]

    %% --- Subflujos con enlaces a los .svg ---
    click D "logs.png" "Abrir subflujo Logs"
    click G "Revisa_SID_ULTIMA.png" "Abrir subflujo Revisa_SID_ULTIMA"
    click T "MarcaUltPerProcesado.png" "Abrir subflujo MarcaUltPerProcesado"
    click K "Proceso.png" "Abrir subflujo Proceso"
