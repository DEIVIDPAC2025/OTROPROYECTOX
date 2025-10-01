# Flujo de Proceso: Obligados a Declarar F29

Nombre Shell: bajaObligado.sh

Descripcion: Permite obtener un listado de contribuyente obligados a declarar el formulario F9. La shell bajaObligado.sh, se conecta a la maquina pluton (ambiente de dominio RIAC)
donde se ejecuta un procedimiento almacenado. Este proceso bajaObligado.sh almacena y deja en una carpeta llamada obligado, un archivo llamado obl_<añomes> con registros de contribuyentes. (En produccion son aprox 1,6mill de registros) 

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `bajaObligados`.

---

## 🔹 Flujo Principal

# Diagrama de Flujo Principal - Procesa4310.pc

```mermaid
flowchart TD

    A([Inicio]) --> B[Leer parámetros de entrada]

    B -->|No válidos| MU[Mostrar uso<br/><a href='./modo_uso.svg'>Ver subflujo</a>] --> STOP1([Stop])
    B -->|Válidos| C[Conectar a BD<br/><a href='./conectaBD.svg'>Ver subflujo</a>]

    C -->|Error| ERR1[Error de conexión] --> STOP2([Stop])
    C -->|OK| D{Escenario}

    D -->|1| E1["Leer archivo Riac (7503...)"<br/>Filtrar con Obligados<br/><a href='./Filtra_anotar.svg'>Ver subflujo</a>]

    D -->|2| E2[Leer Obligados desde BD<br/>Cruzar con archivo de Riac<br/><a href='./obligadoYcompararTG.svg'>Ver subflujo</a>] --> E1

    D -->|3| E3[Leer nómina de anotados<br/>Verificar existencia F29<br/><a href='./sqlExisteF29.svg'>Ver subflujo</a>] --> E4[Desanotar<br/><a href='./sqlIns_Desanotar.svg'>Ver subflujo</a>]

    E1 --> F[Recorrer candidatos a anotar<br/><a href='./Debe_anotar.svg'>Ver subflujo</a>]

    F --> G[Generar archivos de salida<br/><a href='./FCreaArchivo.svg'>Ver subflujo</a>]

    G --> H[Enviar notificación por correo<br/><a href='./iEnviaMail.svg'>Ver subflujo</a>]

    H --> I([Fin])





