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


# Flujo principal - Proceso Batch `proce4310.sh`

```mermaid
flowchart TD
    A[Inicio] --> B["Validar parámetros<br/>(nPeriodo, nEscenario)"]
    B -->|Archivos no existen| E[["Error<br/><a href='https://www.plantuml.com/plantuml/svg/JSqn3i8m343HtQVm218IUxeK2JOa1axW9cwJoeshsE7y2CJ0_FNqHtDgtZT1qSN0YmlZiq-pz5K3tdMnmyRLQEKJ9dOIuIDy4OJ7v5ovuSmnqpbh8wJedMI0SBFOobGQ_ZHonQZLL6Y0SDbthkc_KOkvlFHpl9Ah3M2kEunSKz_a3G00'>Ver subflujo</a>"]]
    B -->|Archivos existen| C[Configurar entorno<br/>(Producción/Desarrollo)]
    C --> D[Inicializar logs]

    D --> F[["Revisa_SID_ULTIMA<br/><a href='https://www.plantuml.com/plantuml/svg/RSon2i8m483XFKznWuCAwjw2A5erK5kqEfThSqfAcaXoqK5yTz75nVt__aLWz1nx0qUwwu1r9TVrEJ_9_LAmPaDGnUPYOkUIFyKNYoGdyj1wKcHRZOO2A8B1SrVkizSiQ3MzFLGgagoZDZ9wg0uvJERGkcXvE1u1MM1i3C9lNSjYKzPodHKdkP6hvKgMHIgIRKIlq8Ed40sZSXzhoyReAoeNKX7OtSI2h8gzUGC0'>Ver subflujo</a>"]]
    F -->|nObligados < nNotNull| E
    F -->|OK| G[Continuar]

    G --> H[["Proceso<br/><a href='https://www.plantuml.com/plantuml/svg/dT31IiD040RW-px575k48hIXa1HjHIk5eiMavx1k9idMpOxCJgelvSa74EoBIOCA7cgXjs7uP-PZfa4qIziuM34P3AJ4YaD8syVIjHkAV_jTKCLBH0RDfhPRWe0EZUJ5XlEjhT0BXe4BagXuRfsmPc2iR12c08OycDrxOIk2SNG-J5HyYnxtePzrCq-Y2mhvP8wcrXS3UPL4sH9wdnytpCIWNvwwuSi-I8qUUkdkhQy0uYLL0SwWqTO1xgE90WX2pmfzOKjrLFIVPpmy8Zh5y-UHYxiidsKFYwjrTd-THgDXFl4hP4i5VTyyYEl2XtJHw0HQLq_H5stZlW00'>Ver subflujo</a>"]]
    H --> I[Forzar anotación 7503 dummy]
    I --> J["Contar registros (7503, 73, 543)"]
    J --> K[Ejecutar Procesa4310 con archivos generados]

    K -->|Error| E
    K -->|OK| L[Escenario 2?]

    L -->|Sí| M[Generar archivo AnotaMensual4310<br/>Copiar/comprimir archivos]
    L -->|No| N[Comprimir archivos de salida]

    M --> O[Enviar correo final con resultados]
    N --> O

    O --> P[["MarcaUltPerProcesado<br/><a href='https://www.plantuml.com/plantuml/svg/RO-zQiCm601tFSL7A6HhTvj0r5Yb0SaIijtLADBNLa6sZ7x8KFhkfStQ-Ow3E-PYKgbB066IDLCe2fDAqM8sBfBYIq0OwkKzr6ji_fV-4gJXY0biGeUhzIPW1eVmyFKg1Vj-ojuzRZVNaePTqTPY4aogeoE3uTpDYcegsAZbG00o5b1KY_cDSgaFgyBaeui4uFQ92U-ib-9PiyD-ukDPo5bfUMA3d7lPiHEdclOZsxUaiN5PV6b9m-D7XjsBNs7vNO3j7jsr99UuaIEkhYxX1m00'>Ver subflujo</a>"]]
    P -->|Error| E
    P -->|OK| Q[Generar CTLFILE para revisión diferida]

    Q --> R["Programar ejecución con `at` (20h después)"]
    R --> S[Fin]

    %% Subflujo común de errores
    E --> S



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


