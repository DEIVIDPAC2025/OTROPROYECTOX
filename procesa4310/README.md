# Flujo de Proceso: Procesa4310

Nombre Shell: Procesa4310.pc

Descripcion: Permite obtener un listado de contribuyente obligados a declarar el formulario F9. La shell bajaObligado.sh, se conecta a la maquina pluton (ambiente de dominio RIAC)
donde se ejecuta un procedimiento almacenado. Este proceso bajaObligado.sh almacena y deja en una carpeta llamada obligado, un archivo llamado obl_<añomes> con registros de contribuyentes. (En produccion son aprox 1,6mill de registros) 

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `bajaObligados`.

---

## 🔹 Flujo Principal

# Diagrama de Flujo Principal - Procesa4310.pc

```mermaid
flowchart TD

    %% Inicio
    A(["Inicio del programa (main)"]) --> B["Leer parámetros de entrada (argc, argv)"]

    %% Validación de parámetros
    B -->|No válidos| C["Mostrar uso (modo_uso)<br/><a href='./modo_uso.svg'>Ver subflujo</a>"] --> STOP1([Stop])
    B -->|Sí válidos| D[Conectar a BD<br/><a href='./conectaBD.svg'>Ver subflujo</a>]

    %% Conexión a BD
    D -->|Error| ERR[Error de conexión] --> STOP2([Stop])
    D -->|OK| E{"Escenario (1,2,3)"}

    %% Escenario 1
    E -->|1| F1["Leer archivo de Riac (7503...)"]
    F1 --> F2["Filtrar con Obligados"]
    F2 --> F3[["Filtra_anotar<br/><a href='./Filtra_anotar.svg'>Ver subflujo</a>"]]

    %% Escenario 2
    E -->|2| G1["Leer Obligados desde BD"]
    G1 --> G2["Cruzar con archivo de Riac"]
    G2 --> G3[["obligadoYcompararTG<br/><a href='./obligadoYcompararTG.svg'>Ver subflujo</a>"]]
    G3 --> F3

    %% Escenario 3
    E -->|3| H1["Leer nómina de anotados"]
    H1 --> H2["Verificar existencia F29"]
    H2 --> H3[["sqlExisteF29<br/><a href='./sqlExisteF29.svg'>Ver subflujo</a>"]]
    H3 --> H4["Si aplica, desanotar"]
    H4 --> H5[["sqlIns_Desanotar<br/><a href='./sqlIns_Desanotar.svg'>Ver subflujo</a>"]]

    %% Flujo común después de escenarios
    F3 --> I["Recorrer candidatos a anotar"]
    H5 --> I
    I --> I2[["Debe_anotar<br/><a href='./Debe_anotar.svg'>Ver subflujo</a>"]]

    I2 --> J["Generar archivos de salida"]
    J --> J2[["FCreaArchivo<br/><a href='./FCreaArchivo.svg'>Ver subflujo</a>"]]

    J2 --> K["Enviar notificación por correo"]
    K --> K2[["iEnviaMail<br/><a href='./iEnviaMail.svg'>Ver subflujo</a>"]]

    K2 --> END([Fin])



