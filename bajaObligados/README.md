# Flujo de Proceso: Obligados a Declarar F29

Nombre Shell: bajaObligado.sh

Descripcion: Permite obtener un listado de contribuyente obligados a declarar el formulario F9. La shell bajaObligado.sh, se conecta a la maquina pluton (ambiente de dominio RIAC)
donde se ejecuta un procedimiento almacenado. Este proceso bajaObligado.sh almacena y deja en una carpeta llamada obligado, un archivo llamado obl_<añomes> con registros de contribuyentes. (En produccion son aprox 1,6mill de registros) 

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `bajaObligados`.

---

## 🔹 Flujo Principal

```mermaid
flowchart TD
    A([Inicio]) --> B[Validar parámetros]

    B -->|OK| C["ejecutaRemoto"]
    B -->|Error| Z([Fin con error])

    C --> D["copiaRemota"]
    D --> E["mismoLargo"]
    E --> F["obligadoSinF29"]
    F --> G["copiaHaciaPluton"]
    G --> H["ejecutaRemotoAtrib"]
    H --> I["recuperaAnotados"]
    I --> J["recuperaAtributos"]

    J --> K{Escenario}
    K -->|10| L["escenario10"]
    K -->|7| M["escenario7"]
    K -->|Otros| N["escenarioVarios"]

    L --> O["rcpPlutonAnotar"]
    M --> O
    N --> O

    O --> P[Respaldo archivos]
    P --> Q[Enviar correos OK/ERROR]
    Q --> R([Fin])

    %% Definir links a SVG locales para cada nodo
    click C "diagrams/ejecutaRemoto.svg" "Ver diagrama ejecutaRemoto"
    click D "diagrams/copiaRemota.svg" "Ver diagrama copiaRemota"
    click E "diagrams/mismoLargo.svg" "Ver diagrama mismoLargo"
    click F "diagrams/obligadoSinF29.svg" "Ver diagrama obligadoSinF29"
    click G "diagrams/copiaHaciaPluton.svg" "Ver diagrama copiaHaciaPluton"
    click H "diagrams/ejecutaRemotoAtrib.svg" "Ver diagrama ejecutaRemotoAtrib"
    click I "diagrams/recuperaAnotados.svg" "Ver diagrama recuperaAnotados"
    click J "diagrams/recuperaAtributos.svg" "Ver diagrama recuperaAtributos"
    click L "diagrams/escenario10.svg" "Ver diagrama escenario10"
    click M "diagrams/escenario7.svg" "Ver diagrama escenario7"
    click N "diagrams/escenarioVarios.svg" "Ver diagrama escenarioVarios"
    click O "diagrams/rcpPlutonAnotar.svg" "Ver diagrama rcpPlutonAnotar"

