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
    B -->|Sí válidos| D[Conectar a BD<br/><a href='https://www.plantuml.com/plantuml/svg/bLRRRkCs47tNLmpGXqs1tK2I9LdERXUh2_aKj5ku1VfAKsE52KLwIQgfM-HZ-Wtx2VcnGf83I7A4EdhacJbdT7Wmu1Vhc75j8u5hXTonlFISS19Xs-xsihtNy644UU_Wf__vl7UG6Nud_jGtODrHehq-j8syfDC-27LWXZMmxHh1EYEu6vgfLfM68w1rGcgeKQ5XSjIoO_oXDhfLLQ6bDl03xRzHXRrZbNuKgWPdMXm1fowZq40GZu0IzwoLZchbVcODGcR4H7E4RyNV246u0FQ_izEo6k6PCVhnjpl17nHQ2-5rE0TFFr8RThpKUUwqGGj7A9ZL5Yg4twr-c_UiunWcPezeTODp4Fxn0FAvtsL44XfqY3OLcjDfcAwZBF6Wkq1tEWlYQ9NutjE8jxN8cSNNcMb1LmMTC-VhJUpdK-PrcIH-wZrTQ5SfM6rOmtgZjiXRL5omjzbbyLlNDem-lhQGH7wyyW1knHvlXSB9z2SFHkYPdmd9QEe1V6N62IuEJBafHHxHTJWhcBEGdCQqSwbaZksOdKwnpiCeACRecVTPcPUTenSPMaXc-_Zzihj7f-tRhEIIMRiGWGt9IJQFm2OCyp2OHY290X8aat3ftJrojq0SqeX6S-8uYBCu6t94b1Fk25UDhb3gBYaLSzh-E1_yqoViApz_Vbs9f3IXgxbIaEN5fXYKygwQcIDS2UNGx1d7FfcjRPaH-XN5tQbZIPEMf2J5NBFmLvim7pGBhPpH4gxay_TQSDRfAQmrVrMF3zMBSeHko7ekLqPPuPSlSb8YTq8h2rTIMCViUs36O2srVG-SkUT_fQwdzWxtrwc_D2zw_9BswGxQf7w-kNWh5BevQ8NAzKakqHwamBh5DuRvXMKn3IcDpz8GhDCacWRQp-DL54y2pQLkgoK7IaBzEMzIhA9qDU7OQrcXMOnDNfwH55b20p8X-TPYkx2qovZ6v3pkPRgAqWb7TLez2wCC-sT6SzfRJvxdUVqBnhl9TaOOOCFJ0woehW-FrKVlfj3AEjCA0vnLg5Z_clbBF7zN0zYzR0paPNSEv0zImFRNsu-UTVhWVK5LjOty3m00'>Ver subflujo</a>]

    %% Conexión a BD
    D -->|Error| ERR[Error de conexión] --> STOP2([Stop])
    D -->|OK| E{"Escenario (1,2,3)"}

    %% Escenario 1
    E -->|1| F1["Leer archivo de Riac (7503...)"]
    F1 --> F2["Filtrar con Obligados"]
    F2 --> F3[["Filtra_anotar<br/><a href='https://www.plantuml.com/plantuml/svg/bLRRZjis47tNLmpGXpX06kXkUPC6qOrv2Pe2c_QreAbPBNTfZaDINRZ5Vao_8P-G7ojaUG59Ng5UFUhCd3CyF1ZmetNSk6wdW4db3F-JQtBSU4uwXN3TRMzKTqVmympsNi4l__Dvho0tubR-HLTWtK6XVRllTkgIJdilzPuRleFhlX6iCrAuePcHRWWEWDP9HT2YHiFLg6NBnNrhgDDDIOeC_CIEtwZ2tlA67gHkmPaEHy2fosWq42GZeC8RtYd7IBjV-GuXDtAYESAlvTy8GRW07e-p9TMCyDmOUlXwAyMzHciXV1lEmTD1MiCFbpel71cqS82IMxBG8FnkwMNUyvvZc9W_eAKTpa7unmCevdvNSPsoe4V8D6XEVyDi7UUf1_q5kjE_88cZrFSUHxoTHS4jFi_CIXQLRCvSh3U9NqoPrrMQ-fdtUA5TbUIjuJj-DEeQHOTQIFuokon-wzk6qSVN5jQndqGUm6TvWv-bnidq9mz6w9cVQPspp0FuZHidXTnpxQOKHSpMuQnWpb8NB66zInLtVCljT8fr4SP1EKRFlC-hekeTlSZGKd5xZD-NxHqwiY-pKYXkxK84DdLHv_C8RCAm28Df1D8ug8Dq4YxQtg5m2yGXYray9qw294_o8KUrTj8TOBMZ1XNrIMcu8_jwFlZxztYi_F3XUQKwOocBvaf1NfIRSb0g-cfk3h2Isg6vuGAFoUninusaPnItfuubJLRLLLtEDKi_seJ5e5cITeOKhDIFxwqKlDVJs99uLayCrOjoDTlKwxbS5UUbNpt9AON2IT8MLafQn-qRuCPWgyY-0S7TZtyLjLDxX_lhrP-Q5pr-Iljq1sqolzXSl1LAskr9etR795TezqfYs-4Bm_p4ifY6Z2LdQGZMMHfF0-qNIHGdaq0BHLspv41LCt_EcvPHd4KJZXjI3Ph5s1JL6KcPfooe9oJVEkmMbdQLiAG-ZtkLHN4suMXEgsTXb67_p6XEU-lHyppl-9BnheQ7YW63hRJEa8Kz6LWdVWG7-FhfdNVr1rUouGO4xonNaCGHh1gqmzC6h0H1ng3TasxmzJlFEjfx7r4ttKxz1m00'>Ver subflujo</a>"]]

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



