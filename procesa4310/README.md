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
    B -->|No válidos| C["Mostrar uso (modo_uso)<br/><a href='https://www.plantuml.com/plantuml/svg/HSgv3O0m3030tbDu0HQ0XfQQ0H0aGJAouyZF_aWqr7UhnscHmYXQzKXN20fkkETrSpwAqo_mPPWt6KP2XjGzB4iXxSsnDapN1Jnq0AojrnH-0G00'>Ver subflujo</a>"] --> STOP1([Stop])
    B -->|Sí válidos| D[Conectar a BD<br/><a href='https://www.plantuml.com/plantuml/svg/bLRRRkCs47tNLmpGXqs1tK2I9LdERXUh2_aKj5ku1VfAKsE52KLwIQgfM-HZ-Wtx2VcnGf83I7A4EdhacJbdT7Wmu1Vhc75j8u5hXTonlFISS19Xs-xsihtNy644UU_Wf__vl7UG6Nud_jGtODrHehq-j8syfDC-27LWXZMmxHh1EYEu6vgfLfM68w1rGcgeKQ5XSjIoO_oXDhfLLQ6bDl03xRzHXRrZbNuKgWPdMXm1fowZq40GZu0IzwoLZchbVcODGcR4H7E4RyNV246u0FQ_izEo6k6PCVhnjpl17nHQ2-5rE0TFFr8RThpKUUwqGGj7A9ZL5Yg4twr-c_UiunWcPezeTODp4Fxn0FAvtsL44XfqY3OLcjDfcAwZBF6Wkq1tEWlYQ9NutjE8jxN8cSNNcMb1LmMTC-VhJUpdK-PrcIH-wZrTQ5SfM6rOmtgZjiXRL5omjzbbyLlNDem-lhQGH7wyyW1knHvlXSB9z2SFHkYPdmd9QEe1V6N62IuEJBafHHxHTJWhcBEGdCQqSwbaZksOdKwnpiCeACRecVTPcPUTenSPMaXc-_Zzihj7f-tRhEIIMRiGWGt9IJQFm2OCyp2OHY290X8aat3ftJrojq0SqeX6S-8uYBCu6t94b1Fk25UDhb3gBYaLSzh-E1_yqoViApz_Vbs9f3IXgxbIaEN5fXYKygwQcIDS2UNGx1d7FfcjRPaH-XN5tQbZIPEMf2J5NBFmLvim7pGBhPpH4gxay_TQSDRfAQmrVrMF3zMBSeHko7ekLqPPuPSlSb8YTq8h2rTIMCViUs36O2srVG-SkUT_fQwdzWxtrwc_D2zw_9BswGxQf7w-kNWh5BevQ8NAzKakqHwamBh5DuRvXMKn3IcDpz8GhDCacWRQp-DL54y2pQLkgoK7IaBzEMzIhA9qDU7OQrcXMOnDNfwH55b20p8X-TPYkx2qovZ6v3pkPRgAqWb7TLez2wCC-sT6SzfRJvxdUVqBnhl9TaOOOCFJ0woehW-FrKVlfj3AEjCA0vnLg5Z_clbBF7zN0zYzR0paPNSEv0zImFRNsu-UTVhWVK5LjOty3m00'>Ver subflujo</a>]

    %% Conexión a BD
    D -->|Error| ERR[Error de conexión] --> STOP2([Stop])
    D -->|OK| E{"Escenario (1,2,3)"}

    %% Escenario 1
    E -->|1| F1["Leer archivo desde Riac (7503 y 73)<br/><a href='https://www.plantuml.com/plantuml/svg/ZLBRQjj047tVhpZueRQe8-o6aiPYqxYHMWH11Zd9Yp5certR2zAkkxjI6kZFz0Fw3ONcnuekCGbsInzdvioPCsVcqZfcN5dao8KmKvDjPQL3aKgMaQP4o2GkTaOMqg0NpQ-YP9h6Cuonu9BXtVaGIXTICTGja4fcaYrx0PceL6oaTKRRQo6vjg0O1OGyR6KkCFZzQxqHpWvogGGROhtxh7EfhOVgwKSkkVxeGLeCvay_FG9Cec_EC65G2n56Mtn0jcN6ukG2l2oAnw16LSoiJEb0mPnU3vg2jw_m2XJDlCNviidkc5cTdOAYd_G3GW2vnY0Kz-K6bA8_xtjmMw7sCe0NNjn9eGIuQ1S_UpywXIcTx_kzcbieBjVFbFPhFhlFvOPndPPkqCaSlh6HCTfub8unJKBKSdI7MwWe5uLGJYyfFQea0KM2jnW7RSoPMoJBaujgTHl7uIgzlG55D-eu9Bph4Bmw3fXzkew_JCFPOhG4_PkyWzQRE4gYLHXTNK_RnlwyTVS__7tbS5ew-BwFxtXshmlRk_NQoQtJBnm_zda7gSOteNZtZedsNZrwSrorl-uZdAwxCgtQIxFCoOhvlZyveAv__nz4Z8k2sVr6jk58UW4XrkaTkHIAbqN-1m00'>Ver subflujo</a>"]

     F1 --> F2["Filtrar con Obligados<br/><a href='https://www.plantuml.com/plantuml/svg/RL7HQjim57tNLvm5HcteGhf76vScjh8A4fivzlhG5QF6SgVYIDwr36DZdxIlw8yLfmbBj-f1GhhdddFFqLNl9BbXrwBHhID9iJNPVQiVP6rxjYyo5WYZjrgs-gSa6Fv3zquXmYnaGIUfei4X0WtkSBU7_jlP7IASVPsTXOm5iJMDVXX84cwkUSg_y1nfLYopCatmuHAAg1gLyy6bo_1j_ERpYkTvbl-3NvIZ07zKsy59meQlU5oW52AfiiLAV9ed6HYEQvbdQsn4KfMhGgpdbKYNMIKIdXPYAU9vBBBqB_ZcckVyXIel2qGu60uPqmsytb6hZ7VgsiSbBcO-t3Tbu6sU_lWC24YvWGmkGdZ7UFsG0Rsp7LDjh-2bzXGv2ySNsF_1fjODOvqafvss1fErDEfHrfPKZrgDmLYQu1S3MdclsjV9daXu_VTsAwVZRck5Tz6ORtNy4pzaRp4iof51x3hIEqqlOb06JJrE6FGTQUCQh-TZuHoJ_OdtTN0xdKxl9kTu9RgtTPpdOyX-ixt7AsNgOTS-0m00'>Ver subflujo</a>"]




    F2 --> F3["Filtra_anotar<br/><a href='https://www.plantuml.com/plantuml/svg/jPD1RnCn48Nl_XNlk16b8BLHfLrLD4f26obGgP6uhgRhoTR1iSDuDl2dE77ZWjJyCUIDe8AcXo9nyS5-VkyR-VaYAObsQu-tpgjGJI4gYL6ddh7eRfU-MqLCMCbxiX4l_nAQti2KSsO1INFdjX6MmK65BA58xBdHsgwathgMWt8wzaa7bJ7bWZSa911kNLA92OdRtVS0TPjO6UEMAEv_Z7VVh6iZpd4sV7toPW2zuu1YiViwC41voO6poQ_mKGQpCTLPVQnVj3B0tcag4WNq-UD19w2SnpRX1JXi7GdMv3mutwdwuwHnOm0ErYtDVdsC-1p0f_7-3zpmz1bqmzCdyGxu_1DVEOuXHUzitu7K-JuPHNwT8voT7EMamKCHg4laynuiApTAbXxDCrrnqoa9qYS_2wcUSDfNjJBi4wDu7m_f6d6ttCzU_QQxx4Wi_L7hH9aM771r_MxwQdGplffzkAuNe_biCgfCURDlCacM-DXM-OF4ZRdWOBkr_ma0'>Ver subflujo</a>"]

    %% Escenario 2
    E -->|2| G1["Leer Obligados desde BD"]
    G1 --> G2["Cruzar con archivo de Riac"]
    G2 --> G3["obligadoYcompararTG<br/><a href='https://www.plantuml.com/plantuml/svg/bPBDIWCn4CVlUOfXGMWF5Tk3XrsebLfxKOIs2fvaTfDjKv9CcIIY3-Kp2FfYafLsMzoBjoJp__WnPE83SeZM09L6hr7ISqLsXuoycekWWr6mZ6LjufPWq2aIJOGG-PIS3nmrWoDRil8W5I1N6_rAkMZD_kNiujB8y_0MEbw9fHW0np0bjvgVI6jjGjFPlXP2vDSbQzuNTRL0GWNbAzOXCYRFGbN4h1ZSmrvVY7oM9ALcM3oku1rkda2vly79FrNCs9PATJgURLKL0p9KPD590f5vuW23sEeQil7HdLXcXH2wXjxNvuoPEDKdtrKVmaOvw2s_F_e28B-ZDMItQ0o1CMXH8Y1uxOEo2CEi4Cf9NNU3L6Gj38QZmuuRa1CC6BUxJjCEh9JoFwpH4TOz-PIU4F2mnDzAIR1MJgL3aVuMxSH4EHcj-G40'>Ver subflujo</a>"]
    G3 --> F3

    %% Escenario 3
    E -->|3| H1["Leer nómina de anotados<br/><a href='https://www.plantuml.com/plantuml/svg/RP5DRjim48NtFCM3DvRGn4YHHPiOoWzg5H0GQ64dsHY6CHL7zW0KQP2KsXwd1-WP2ZGNAoGBGNww8Zdp-6RmlfiGoSUsCJ3CfMl4qgrraRGBQcWfgP6OF5HioOj3bk7yEaNSiqMoUlgTAk2oQ0vU6l6O55OgSJXG80y2X-ZRAhQUGACjQh5aECnciycy_soNl9CGlGjtBBqWmzbSAU3xNWmZ-Vkdtd4CYH7BT8BwyDKPSU7JUOhkwPSHxQvJI7ZU1hZCVqHFxD5lnTu5V4Qr9nzmUWNTDitF-L7NaT_wDY83HLSdGojzqTCTCWnprnURiLuYGuaF-3Y-DSLrkJczwhOFHR7OBX_kaM4q_hzayJWgTFTES5_aPRvTv5_kRjTd6sIObjCX3A07iU1lxQvdC5rDtq0OZ9v1BDi8qyTvdC1MIws6SqXLlQQsuYCnPrypgyXgqHHTJmlbPAxO14PIkdvYYEwWZix3zOQjRXlp3m00'>Ver subflujo</a>"]

    H1 --> H2["Verificar existencia F29<br/><a href='https://www.plantuml.com/plantuml/svg/bP7TIiD048NlzoaElJ09QgczQsgqsgOGa22cWb1AMPEj7KXswsvIW-_abO_G5vFy2GLHl1jsPi_vpip4v5pdHPPYBpHjAEP-IIONCYO-7uvOtMRC3IJ5n5DwvnebF5oC6NlRKYfWbxZq45ux80CxEdmu3A0Dx9buBbxWUR0Yoq6-5VAx3RX1jjEKaKRljZ0nrvWFHtXuNFJx_TwO0K8cj66jb7bD6wpvS6INPqZlXIQLg3ES65zhfPtAPz2vX0gY7c-y_eGvmWaLSX9I815noZMFwV0fAxeQgmEhFoKyNvQhywlzUX7ueR-U-TExc-LW1GzMQ3NZhen8LjayTDLfjJr0f4RK44Umluf6hUZ_4aK1_ASWMlW_fv1JrG6sLGVOdS2jBbuspq8cxTr3vJ1cShLZ4o6J8ak_0000'>Ver subflujo</a>"]

    H2 --> H3["sqlExisteF29<br/><a href='https://www.plantuml.com/plantuml/svg/RL7HRjCm57ttLnpUKebENHz0JPMnqZWGgKs6ay83Gf7NE9chDEviPq92V0mVm3SWiHz39ilQ8bui-vnpZ-yzzzfOhcstRs3k6_fL6YkYwOnOQHk1hBkjccwdC3vdoTyYGlo5aNNBDGvSF_xO2wkLySdOFGlTMGGekVryeyoNyTL3iOdZi62R_4bm45ggKY70JN-R4-9dmkAsB2hLICTC7BPKRINhJdEDJ-zfGZzIXYJDetIJX1XVGMXT65dpQ3gR_r-TVLXHnb8sgDzsPjlBYKztOjjPhf7H5Ltc41UYqlk-0uA8fMjaSLZGB5-4QH6bRBrPBLYS4cVFA8vZd0n502oI47q8Jt4CO1wnTR5Cm_XTYW3JsJDE8pRWieLt-VBLwz6S45d1-_thc4g0oPiHx9reuMMFFqS4y9cmIhjDJEO4C5OTY6YCW9UeS_xooBUbh0WvS6sbbQezpH7VpeeySzzi-OKxLIdm8d295iCEHi-Mt_-r6uBk_LQgTgZI42sutjx91uMgTEN-akkQQ-n5Q_XEE86XJZe_QsHw-jMrQCjkt_m1'>Ver subflujo</a>"]

    H3 --> H4["Si aplica, desanotar<br/><a href='https://www.plantuml.com/plantuml/svg/VP3HJeCm58Rl-nGdIymWQZDlGNH4k20nc0nsjIoaevqxIIdO5YM-aq_XYncODdAXlMfp_l__Jl-riKpRlf5WCEuarYmHXgdMCasc4I51fh169l6TQHWWWfkGaBSJIW7U0BSHvFS-e06l-Fpm2G0UmUFCxeRzzTrhLMPfdbP9-l0OxrPxY29O5aiVx4aevpXx4d7ed_yI00HPqsbiKCCY4GS1ILh4-LCPRueKDjkIKhe89wbG78_4nPeNcIbJkMzvb59_nAp-XsJAr1fjwq1p2a2WVZ9vQo22sVDoR6csZRi4OuV3MI4K_suoR_snQeV_dKQd4rpmnTMC4X9YRDkHjL2yR-GN'>Ver subflujo</a>"]

    H4 --> H5["sqlIns_Desanotar<br/><a href='https://www.plantuml.com/plantuml/svg/RLBBZjem5DtxAsvN0rA8fjDk6jHgtDZCMA8nTHAwZ3p4KACaPcuSf57LZ-ctzCUg42ZGpiRttCSvllBnVUir-gwke7skHDCMpBIwSLuZyTPN1jBkQLrrMmUJ_oV8WKn8fCpAFbc4dSRVlshZqRKHcVHfWPq_ed9F9h0mQ5tfo0HQZkXmIaWKksPjDnrgX6-FFE5BhY2HsKpc2OF99p28_QL5QpTwTlTX-ZeZ_JhdIabroVZSjQk1GYA-DQlEQmIHf5nb899CGYfOGHEPqOBnz008m8Wch8Wb4myoW1whF1i0MmwHnh6GoO1ZcgTqW3Cv5qTAdWX6MK00XZJDgJhr64zZ9HPd2PvcbCahrHcF7scX-8D8CoN_wWnbdYm5PV94Zdbo5kyVxchvRAQ-N1KMN0d9v9W0BEayvocCmZ0C83hQTKJbFe0RTXF0-tTlRmE8Ziu548OXdFFnzE2_TzXeXDif8JkDtdhhcd-DWny4u3mxQf-hbGxxqvK6tdpiBInEne-d1A3rRaT-lYPvSdRG5FKERMsnRpi4qy1EDrvNbOQNFjEu-cxt3jPbhnh56ZSQeJPDgxUc7pXznilzxYutECHxqvHTNVq1'>Ver subflujo</a>"]

    %% Flujo común después de escenarios
    F3 --> I["Recorrer candidatos a anotar"]
    H5 --> I
    I --> I2["Debe_anotar<br/><a href='https://www.plantuml.com/plantuml/svg/bLVRRjj647tdLqnTD9PHnH0bIjObTiDhAi2G4abE2nI5i297z3ghNNbtwTWf_37zW3xb4_nZ1I-oHLf2R3v816Vcd9cp1oFglT94wcJ5mCC5pWaNcaX3KyqGfibYoP8h0MzBmKCu_S5b788jmqjw8_gWz1r3TRnELkmbbUeBvMiYoGgcQI4eBMcey-90y4Z07Q3Ib0c8aQCaRAjaGS8liHG9Zrp1X8IVW-pQob2N919VAOz1omIt0aMLv2Z1R6y5F5oIXEb0S3qYAmHRqXBdLdnAlo6OpJt1R9o5OD5Mt9PIV9rTql0BHwMWUToi1ej1OadkZ1Sg7seXKS4Tk4G91H72XHAlqvwa67d7v2igiS9g4Fun09ogtfxbTm8pZGWPeIoUDhidbjqn83r0NJmpsrQhqp3kjt0JXI5Hk1ivS8EM6rIHdPDUk-6KaK-yJgVHDUvVA9T7IIp9YcH2JJ5Ca8UKl4ukXTTfMTxwzh4rVQlHRXa0vtI9vvHZgVj2WwteCpqxlXrq3O2FH6eQqZNXkWpXMC59iv9GHV6Te1saAdb4amLHvIvEdAPbkjlHPzhRdkEbYhv8K9SHbTbllBX2BTJhf0mPKMgF1Ng-uzjL2_IQJQTfbYtGiKpVx9JC9HPN6EezmCt02gmgSDjissqxzv7FDTLtK5k929b8dH8HBTHHjV5txp3BF3lRpUHtWqxGgZAPjkFst9p9IRE9l8CQvHhbaeIOEJDH2P5Kx61S51NxE0FFztotokasMhscatEwWcif6DJOm_UOXYJbunYBS2TVc6VlfVE3ddzIfVCissru6ph6CDHKS0KrHfKcgWv4IeoPK7K8YNxubucuB6z-VYdxfdYlnXktbtTGhzjmUY_U2gvOhGL7hZCdUwZMZ6ASu2lDl47PwuPkq7xc1lEasx7AXcuuxPRLBXawP2A9zYdW-K6ZYjjnMrQtLS9O2XQXt6iRnti6ujgTmFHB8DS99dkMjjSEslvpktlTbjKjOKJ5wjdJIhv_AZ35thet3CF8NcAC_WH3ka3W4uofqZ9rqqSYvskKL4IY3igNKiY1qHzo6bB2w3S2t4xVQYAXu1GQ0yDOfuiqzHSSE4d846xX5CpZuz51rbpA8QH42I692CY2QM00q2NK3YAY_xhz--tPpVnYEFJcO-Ty-C7snd1w2eVJGtZp1fuoPaD_vCyztpsti_ZeyBU38z2NoA4sVVZlo00eK3rS9761iIC7e3zShILTKGcJYrdgsC-3B88yeiid77NDXbo5aYum6xjMQNToCQj8LadmFjVXJIxZKTfFOtStsw8-tVyAvk17_JA5K1k9vtDXofbk9feDi0xfmtTU7dBpdOrw2x-0sMWqzdNvXBoM8fQe1AIB9P5ay0XrRnXFQI7XcaOaWYNbXAMTa6AmWQ6qM6zRfwfpPftSfB1nwPh8kKnq7Jvkj4wVH3TxREhVKgMnC6dV5Nn9uqGIM16ELzbFKgOGAfX-EXyON6W4IUDBRVX_-cxw4FxutH_vd_q9ZCQpO7mnyk3jMLer7t8rLpGcGREt8tlwwToVJCQJxMmdKM6MZZo2bCim-luLXeacC1nD_SaCXgFP6AP3RswFnZDxxldJx2ORIw7K16u8ongkFKgnKU1H4hiELijir05rU7mqC8piR0i6lALQAF7iSFiITI9vgjIsdxBIpUYx756KrTGr2ybn-YaYX9zEKmNccyAZp1uPR7PCQR3ggDoho47fI2GQxe3aVuTol_RLMbAkbxNyeEkmGgx85JuUuj6Wr53poP4RYsU6kpVU8u-I5ViV'>Ver subflujo</a>"]

    I2 --> J["Generar archivos de salida"]
    J --> J2["FCreaArchivo<br/><a href='./FCreaArchivo.svg'>Ver subflujo</a>"]

    J2 --> K["Enviar notificación por correo"]
    K --> K2["iEnviaMail<br/><a href='https://www.plantuml.com/plantuml/svg/bLPjRkCs4FslKmpG7vi2sy2I9LdERXUhBnO5jXz0sWECgR72X2Az99N0BNAOdg57s8iLaXn0aYFKqK-zcVU6Zmy3VhOEZMiR2Q9KZm9_GI4z9vmak6rtUzdUQ_XXZ7dluCV_-Rnta1f-9nxr3LXtb6Il3sqZB-cq3q8Tq603jrqZM6S4TqCpqwhIS0IoJaWDDIaoA4SjE-GFjT6jgd8jjO7lMF-DAkmTLlf9g1gSQMa4dBgC8WD-D08AscCh7TFA_OeDGMh4H7E4tug_2FnW0UoFizEo6k6fCVhfZpl17nHP2y5rC0TF1waD7YzrdZjjoC8HShJQGaNmfzLlynuxZc5YV2Ah6vg3yBS7aCtzBi8oPdw7Q5EHEVqDaasOnXvq5-XE__meNCShxtd4srhYQEbrPfQpTSxcpDbc6wsoAVEcYEDLuZrVQ5SXi3ROO6_KBV6M51VuDhiiVUtQXj77rnQKuIfQUm1Vn9w-24MJwKyUZD0pF-CoPOa7y3iQ9xWue79JYYnacs1MC6SfCnQnpgK27UxGJgVOP47evsFqpFkqo8hEqOiCpINQFdw_xUx9QVisAxb4QnSYi2spCfr7O1i4MU1F8n27Vkd7at3ftJrnjq0Si925S-B8Zz8e7N9KAYVS4QuQNP7KNL8gTDf-Fn_yuqVgApzzUbsfJ5ZCrdCbFytoRJuePLqrcYDS2UN8x95JdypMjcY4VaLnT-fOqcH5MPJvN3DVhRT1DcZcMZcZ9Lp9R__MWcEdfwZM_5KzFbGlofLiMsxcSaMOvglYHKvAuavePU5A2klGlWSqXcgfxNlWwBxz8tKzjNUulqxzfNdHuvUqJtVGDbbbsuktGgwRWrQaN9_aWkn12gfRUcEONrWMqv2mw2mD_YQ9mscWLrcq3gD9eBdKRRNaG56orPmtpjTXifvmxBMio2p69YlEIF8qPduv8VdQKhkmj8k8HULvt8ja7IOJZkgqUXP66VRFZEQqjvuzp_FwDuntyrF_8Z20m-C3U4lceA518JzuDp-hHytHWEL671nqBnhTlMYkxTq7ppfzy3wJgjf6_WS0'>Ver subflujo</a>"]

    K2 --> END([Fin])



