# Flujo de Proceso: Anotacion 4310

Nombre Shell: Proce4310.sh

Descripcion: El proceso 4310 Permite crear un archivo con contribuyentes con la anotacion 4310 de acuerdo a un periodo tributario. Estos contribuyetes anotados con la 4310 se forman a apartir del listado de obligados generados en el proceso anterior bajaObligado.sh.
Se exceptuan de la anotacion 4310 aquellos contribuyente que tuvieron una anotacion (73), (543) o si declaro un F29 en el periodo de procesamiento de los obligados o si tiene una declaracion F29 vigente. Estos filtros bajan el universo de anotyados con la 4310. La salida del proceso es un archivo de anotados que se envia a la mauina de docminio RIAC(PLUTON), para el procesamiento posterior de esas anotaciones en el dominio RIAC. 
Tanto para obtener los contribuyentes obligados como para anotar los contribuynetes obligados con la anotacion 4310 esto se ejecuta en la mauina pluton (dominIo de RIAC) 

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `bajaObligados`.

---

## 🔹 Flujo Principal

# Documentación del Proceso Batch `proce4310.sh`

Este proceso tiene como objetivo generar anotaciones masivas (4310) en base a información entregada por Riac.  
El batch realiza validaciones, prepara archivos de entrada y salida, ejecuta procesos en Oracle y genera logs y notificaciones.

---

## 📊 Diagrama de Flujo Principal

![Flujo Principal](./diagrams/proce4310_main.svg)

---

## 🔧 Subflujos Auxiliares

### 1. Logs
Función encargada de registrar mensajes en consola y en el archivo de log.

![Subflujo Logs](./diagrams/proce4310_logs.svg)

---

### 2. Revisa_SID_ULTIMA
Valida en la tabla `SID_ULTIMA_INFO_IDENTIFICACION` la cantidad de obligados no nulos.  
Si no cumple la condición mínima, aborta el proceso.

![Subflujo Revisa_SID_ULTIMA](./diagrams/proce4310_revisa_sid_ultima.svg)

---

### 3. MarcaUltPerProcesado
Actualiza el parámetro `ULTIMO_PROCESO_NODECLARANTE` en la tabla `SID_PARAMETROS` para marcar el último periodo procesado.

![Subflujo MarcaUltPerProcesado](./diagrams/proce4310_marca_ultper.svg)

---

### 4. Proceso
Genera archivos de anotación a partir de la fiscalización:  
- `7503`  
- `73`  
- `543`

Cada bloque maneja errores individuales (awk, creación de archivo, etc.).

![Subflujo Proceso](./diagrams/proce4310_proceso.svg)

---

## 📂 Estructura sugerida de archivos


