# 📊 Flujo de Proceso: Obligados a Declarar F29

Nombre Shell: bajaObligado.sh

Descripcion: Permite obtener un listado de contribuyente obligados a declarar el formulario F9. La shell bajaObligado.sh, se conecta a la maquina pluton (ambiente de dominio RIAC)
donde se ejecuta un procedimiento almacenado. Este proceso bajaObligado.sh almacena y deja en una carpeta llamada obligado, un archivo llamado obl_<añomes> con registros de contribuyentes. (En produccion son aprox 1,6mill de registros) 

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `bajaObligados`.

---

## 🔹 Flujo Principal

```mermaid
flowchart TD
    A([Inicio]) --> B[Validar parámetros]

    B -->|OK| C[["ejecutaRemoto<br/><a href='https://www.plantuml.com/plantuml/svg/DSh1Ji9050NG_VkA9s7HBafmsuP8XGP9gDM2wsR2FEYOTXvvCzK5wIVv5VwO6TJTlUVUfVDA_D1tIEzq7BoggMVFS6D8Ttp6oT-2ubeyaqqizyQgvE9dhfraa0QVNilyzMtxd3TrKLQ7VCIam-brTVY7fdhSRST0vVgMD_cwQlPFWUmBYM7DOmRfPb2YbU2ATKq-0p0dZ7uBtYrm_X2ZRybYjF_-YW4nBUo7KO975Y56JKWYB1WvOtfbkZWB9_TP15tSPq1McnE0yto19LazzDqF'>Ver subflujo</a>"]]
    B -->|Error| Z([Fin con error])

    C --> D[["copiaRemota<br/><a href='https://www.plantuml.com/plantuml/svg/XSvDJeD06CRn_PpYjM416p-sa4Qm9OQ4WaAxdaoPgPs4cPUy3AWXR3s0z_0KtiIJ65ouSU7sbt-UF77l1Bd1jD1WfqMb33h1Vf25EJx1YfeEQj7o0essekVPABWtsGT56YNEb-x5hI8MBfatRGvfiKzubUxAVJB7thHB7WzPyIkXDsspYfTtUNRFwoJFjibyzSzwn9W-WRz1MIa75skulWt0dPK5l_xy21X0cDfH2u86YHI2LA28aC3ljJP2jq6qHFrpkkZw9cBAIdrYB2n9AYi8Na6gRY118AWvwn4Z5bRAeZakzlNs3dXi__xg7NOiLbOEflq6'>Ver subflujo</a>"]]
    D --> E[["mismoLargo<br/><a href='https://www.plantuml.com/plantuml/svg/HOun2W9134NxEKKAYxNn06wXe7OMWlOIdRW6PXD9CYA8HzfJU35n2ot_ux_FNtgWHUqBzEozRj4wJIDByvLAe45HwJXgXanGteCGEf20difnyfGT6MlMromUqIQ-GBDc3vP0_vdaYod4bGIQ_NkO9e3vLZiWCxNscpPoPpGugndfdtleBL5nWkQW6HsugrZ8nuNlEvQArYQIp9SqjfSakVRb0m00'>Ver subflujo</a>"]]
    E --> F[["obligadoSinF29<br/><a href='https://www.plantuml.com/plantuml/svg/JOr12i8m44NtESLONEWcQC55BSM2jYiHqGD8J4ORIJCoJQiW7ibJU36fRjnztkVnyYOe3ctjW8xEdfMXlVLbd8Wl5_CrdI5QeNQAgOmJqEH1iQviHxrn63xy5jcIeQSCzn2bObvSKBT1CVnfKagOmIOLzWIZ9PaT1XXaC5cC8LJeORH_lyO2uDShbNFqfqTfVnM-iuf14pCI83FnbpUtej_PD1NeZJs99j1LvEXDMxiF'>Ver subflujo</a>"]]
    F --> G[["copiaHaciaPluton<br/><a href='https://www.plantuml.com/plantuml/svg/ROizReD044RxESN4ee0cFot8YbS9IYn1S32kqGZMyKhiBfbTd0BHvW2vGGwGK_WcEKc4tQPyxtlVodbYF-WE6zihUgP6qQORl3LmNY3Ex1ikkEdHwxusLYj3jIPttRWZ7kOSzUdxVL26aAMsdXO9n7CVZEMk4bkHJJV_N7y_lp0OS_6wMx-8kappeX9J78oFw_92HLsb-QOeHJOb43yDn2qnFjYsb3u1K7iCBu1NIxozZz0VfC5mU_g9035EpL4HOsEPfSLMecIsZA5JIfFgecIEt4Sws-LT0jAqQW_WlErX9KqxwEuF'>Ver subflujo</a>"]]
    G --> H[["ejecutaRemotoAtrib<br/><a href='https://www.plantuml.com/plantuml/svg/HSjDYi9040NWVPsYb2nqeUWsZMYG88A_6LrBcovDIz8brPsPHV18diAB3T65k_U-nvlve2NKLObqexmEEgEA0oT1x1dU6yGhlc9NV87MsTpgSkYBheAubQXP9_lZSfESidIzFIGF79GODVDZkZbyxVl3g74x4ik67mhYHQt5QC4vcuo20h0Nx7qATYOuclOn5EImz_DwzW4nJjslrO8vYn0ZYR2erlrVskR9M04vOo_W0zzXHixKLVaF)'>Ver subflujo</a>"]]
    H --> I[["recuperaAnotados<br/><a href='https://www.plantuml.com/plantuml/svg/TOvBQW91443tTOeAk508-ModaIXXo2wAqNKefahIu5HDggir81uc1yWfl5XGiitkyTxcpKgGH-rtwDBLGPpcQa5i1Qu56ky6f3_tFZhgKZmRs-aklW9P2Wlsv-_FcfNGfRUW17cBusVZbGJUJF7XQOBn8OhZj_FF112RLlUP73jp5qDnDqyNNmxjXQUF2KGvRm6QXRCe-Iso3DN94pGlbPp9KHH7nzLcFMzVrwVx_nuJbB01Pg9S-zql'>Ver subflujo</a>"]]
    I --> J[["recuperaAtributos<br/><a href='https://www.plantuml.com/plantuml/svg/TOv1IWD144NtTOeIiaX0D6wd2IR8uCw46DTIJbL8GwPx_5qTXP33U01FaOj919Vk7kzjthoum6k_PrXN1uCi7F6jUYxqcwX1Dx3yoTVHCQqCCMi-tVYdirfHu_xyzLvZ4eRrsILGtFBu8UlQdAzcFBsViEyiyVZv_3qXvgPDXoZWBWEMsO2CSF7bextmx2wG9OrRecO9jIIuPhMXGX2eUQm25R0b7XtNBvj5-xGvtVux6QXu7cXkIMk__m40'>Ver subflujo</a>"]]
    J --> K{Escenario}
    K -->|10| L[["escenario10<br/><a href='https://www.plantuml.com/plantuml/svg/jP11IiH044NtVOelk9ZPXCIT2OC36bSYek1MokwAbcIwfBgY0-AHF8KN4sS654HtxehFvxz7BOkJ-RGQmILo9XDjwh09GtlD9eD4Cl1QYdEEGg2iJadBpVvBlc0JJVfQ-Tgx80Dcvxhh7itXzvmnktf_cmUWxVEJa26g6IlOJAqBG75z39oJ3E4te9lSJlu_nFw1u-HaEE4uakdfmI6gglhw1ffwopdMTCcElGNg7wGplTlkVvlf_b1eotF_UI-QRcUoaLfoJjDg_000'>Ver subflujo</a>"]]
    K -->|7| M[["escenario7<br/><a href='https://www.plantuml.com/plantuml/svg/VOwnQW9H44NxznKtdJPBj97i8X5qKuKK4TAFRsTrP7qJvisg-QXyXJyMeW458Ttb5kUSMNOoxtSTE4TEPAAJSFv2-S4chKGoaCMDx3M3aZercl45SfDLxvgh82q6Rme-IdPEpqFuXXC6ozFtC01bdVP2XgXch60pjIe0sVKpS6ga3Q6ijnnx9yE2OqUcB-Cd54LnhSBaufbhyywEXoaUxqIlkhxWRoZLFmLbFjI_Upgg_aBEJJDEJR_hVW00'>Ver subflujo</a>"]]
    K -->|Otros| N[["escenarioVarios<br/><a href='https://www.plantuml.com/plantuml/svg/VOv1IWDH44Jt_nJbBjaCnfqp10DnN8aBXUmxVtfCo-HtwEuPzL2Umej94a51S5CK5DHxAm-o6FS3s3CNCj7DCJoTXbHlsAINJ0Qol9D97LGqg5F7EoXCjcEeDqbwp1uK_2OUN6xcY1qNp9u-F-O9gDio2Hcoch62pTIQ17Ze8N7ff4-fRbyuZq66Myu3cTvTNQEggXyrJ6H2su7FkBLsZnouMEBo3-zUdy-KNsVDFoArlxR7lbmqtpudjHMNRjmFNm00'>Ver subflujo</a>"]]

    L --> O[["rcpPlutonAnotar<br/><a href='https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0'>Ver subflujo</a>"]]
    M --> O
    N --> O

    O --> P[Respaldo archivos]
    P --> Q[Enviar correos OK/ERROR]
    Q --> R([Fin])


# 📊 Flujo de Proceso: Anotación 4310

Nombre Shell: proce4310.sh

Descripcion: El proceso 4310 Permite crear un archivo con contribuyentes con la anotacion 4310 de acuerdo a un periodo tributario. Estos contribuyetes anotados con la 4310 se forman a apartir del listado de obligados generados en el proceso anterior bajaObligado.sh.
Se exceptuan de la anotacion 4310 aquellos contribuyente que tuvieron una anotacion (73), (543) o si declaro un F29 en el periodo de procesamiento de los obligados o si tiene una declaracion F29 vigente. Estos filtros bajan el universo de anotyados con la 4310
La salida del proceso es un archivo de anotados que se envia a la mauina de docminio RIAC(PLUTON), para el procesamiento posterior de esas anotaciones en el dominio RIAC. 

Tanto para obtener los contribuyentes obligados como para anotar los contribuynetes obligados con la anotacion 4310 esto se ejecuta en la mauina pluton (dominIo de RIAC) 

Este documento describe el **flujo principal** y permite navegar hacia los **subflujos auxiliares** del script `proce4310`.




