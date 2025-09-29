# Diagrama de Flujo - bajaObligados

```mermaid
flowchart TD
    A[Inicio] --> B[Validar parámetros]
    B -->|OK| C[ejecutaRemoto]
    B -->|Error| Z[Fin con error]

    C --> D[copiaRemota]
    D --> E[mismoLargo]
    E --> F[obligadoSinF29]
    F --> G[copiaHaciaPluton]
    G --> H[ejecutaRemotoAtrib]
    H --> I[recuperaAnotados]
    I --> J[recuperaAtributos]

    J --> K{Escenario}
    K -->|10| L[escenario10]
    K -->|7| M[escenario7]
    K -->|Otros| N[escenarioVarios]

    L --> O[rcpPlutonAnotar]
    M --> O
    N --> O

    O --> P[Respaldo archivos]
    P --> Q[Enviar correos OK/ERROR]
    Q --> R[Fin]


```markdown
- [ejecutaRemoto](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [copiaRemota](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [mismoLargo](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [obligadoSinF29](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [copiaHaciaPluton](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [ejecutaRemotoAtrib](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [recuperaAnotados](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [recuperaAtributos](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [rcpPlutonAnotar](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [escenario10](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [escenario7](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
- [escenarioVarios](![rcpPlutonAnotar](https://www.plantuml.com/plantuml/svg/hOy_JiCm5CPtd-9HPMYNqWgcH1Mr81ALcWQIT8uinoL6gL_qR0DIb9K3S0zEmKqu2KhAmD2HxTFtH_fzQ-i4ENziW6Jxq7Y7XXjqWjWOi72BJp0XsS9e9yfOBvhhg-LYxjuSr49g0QVT96BXK0owR5_md6_xoxERx_SF2BgxJLPcSP8MQPdbzoNVfGNl8wOFCBt5AbCEBbQmk9c1gvM1QVxrEMC0OMnUj22GIAGG515IDFZsDHxqQXanPIfzOB_ayREItWaG0udKQA0bbCgAkQr7O5j3q2NySR_PyHCGx_zqpjx-Hqphi6LhPIf_R7u0 "rcpPlutonAnotar"))
