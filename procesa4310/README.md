# Flujo de Proceso: Procesa4310

Nombre Shell: Procesa4310.pc

Descripcion: Procesa4310.pc
 Objetivo    : Anotacion masiva de 4310
 Trabaja con : /DIC2004_008_FOR/BATCH/ADES/Ejecutables

 Escenario 2
 1.- Lee obligados sid_ultima_info_                               
 2.- Valida presencia de F29 o giro               
 3.- Filtra nomina de Riac, los que estan en nomina tienen 7503 activa

 Escenario 3
 - Lee nomina de posibles anotados y posteriormente busca la presencia de un f29
   para dejar calendarizado que este sea desanotado.
 Modificacion : 06/04/2010
	        Se cambian los meses de marzo, junio, septiembre y diciembre
                Segun ERD : OIN_SIMNET_ERD_Modifica_anota_4310.doc
 Modificacion : Cambio de año.
 Modificacion : Cambio de año 19/12/2017.
 Modificacion : Cambio de año 19/12/2018.
 Modificacion : Cambio de año 18/12/2019.
 Modificacion : Agrega alertas TG 73 + (37,50,5001,60)  02/11/2020
 Modificacion : Cambio de año 30/12/2020

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del programa PRO C `Procesa4310`.

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



