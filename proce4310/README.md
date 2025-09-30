# Flujo de Proceso: Anotacion 4310

Nombre Shell: Proce4310.sh

Descripcion: El proceso 4310 Permite crear un archivo con contribuyentes con la anotacion 4310 de acuerdo a un periodo tributario. Estos contribuyetes anotados con la 4310 se forman a apartir del listado de obligados generados en el proceso anterior bajaObligado.sh.
Se exceptuan de la anotacion 4310 aquellos contribuyente que tuvieron una anotacion (73), (543) o si declaro un F29 en el periodo de procesamiento de los obligados o si tiene una declaracion F29 vigente. Estos filtros bajan el universo de anotyados con la 4310. La salida del proceso es un archivo de anotados que se envia a la mauina de docminio RIAC(PLUTON), para el procesamiento posterior de esas anotaciones en el dominio RIAC. 
Tanto para obtener los contribuyentes obligados como para anotar los contribuynetes obligados con la anotacion 4310 esto se ejecuta en la mauina pluton (dominIo de RIAC) 

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `bajaObligados`.

---

## 🔹 Flujo Principal
