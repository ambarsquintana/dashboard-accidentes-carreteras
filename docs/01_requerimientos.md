# Requerimientos

| | |
|---|---|
| **Proyecto** | Seguimiento de accidentes en carreteras federales |
| **Solicitante** | Dirección |
| **Responsable** | Equipo de Analytics |
| **Versión** | 1.0 |
| **Fecha** | 2026-10-06 |

## Contexto

EmpowerLogistics evalúa expandir su operación a la región sudeste de Brasil. Un estudio inicial del equipo de seguridad sobre las principales rutas de transporte concluyó que la mayor concentración de accidentes está en las carreteras federales. A partir de ese resultado, la Dirección solicitó al área de Analytics un dashboard para profundizar en el análisis.

## Objetivo

Dar a la Dirección una vista única de los accidentes en carreteras federales entre 2018 y 2020, para identificar cuándo, dónde y por qué ocurren antes de definir las rutas de la expansión.

## Usuarios

| Usuario | Uso |
|---|---|
| Dirección | Decisión sobre la expansión |
| Área estratégica | Seguimiento de los puntos de análisis definidos con la Dirección |
| Equipo de seguridad | Estudio de las rutas |

## Requerimientos funcionales

| ID | Requerimiento | Origen |
|---|---|---|
| RF-01 | Total de eventos ocurridos | Solicitud de la Dirección |
| RF-02 | Eventos por hora del día | Solicitud de la Dirección |
| RF-03 | Eventos por día de la semana | Solicitud de la Dirección |
| RF-04 | Eventos por estación del año | Solicitud de la Dirección |
| RF-05 | Total de fallecidos y de heridos | Solicitud de la Dirección |
| RF-06 | Mapa con la geolocalización de los eventos | Solicitud de la Dirección |
| RF-07 | Top 7 de causas de accidentes | Solicitud de la Dirección |
| RF-08 | Accidentes con más de 3 víctimas | Solicitud de la Dirección |
| RF-09 | Filtros por mes, año y clasificación del accidente | Solicitud de la Dirección |
| RF-10 | Toda la información en una sola página | Solicitud de la Dirección |
| RF-11 | Eventos por estado, con su participación sobre el total | Propuesta de Analytics |
| RF-12 | Tendencia mensual de eventos y heridos | Propuesta de Analytics |
| RF-13 | Eventos por tipo de carril | Propuesta de Analytics |

## Requerimientos no funcionales

| ID | Requerimiento |
|---|---|
| RNF-01 | El proyecto se reconstruye completo desde el repositorio: ningún paso lee rutas locales fijas |
| RNF-02 | Las cifras del reporte coinciden con las de la capa gold y con las cifras de control |
| RNF-03 | El reporte se versiona en formato PBIP |
| RNF-04 | El reporte sigue la plantilla visual definida en `assets/Template.png` |

## Definiciones pendientes

| Tema | Pregunta | Responsable | Estado |
|---|---|---|---|
| Víctimas (RF-08) | ¿Se cuentan solo los fallecidos, o fallecidos más heridos? Con fallecidos son 44 accidentes; con fallecidos y heridos, 2.231 | Área estratégica | Abierta |
| Estación del año (RF-04) | Las estaciones corresponden al hemisferio sur. ¿Se usan las fechas astronómicas o trimestres de meses completos? | Área estratégica | Abierta |

## Alcance

**Incluido**

- Accidentes en carreteras federales de los estados ES (Espírito Santo), MG (Minas Gerais), RJ (Río de Janeiro) y SP (São Paulo), de 2018 a 2020
- ETL por capas a partir del archivo fuente
- Modelo estrella y medidas en Power BI
- Reporte de una página

**Fuera de alcance**

- Fuentes adicionales o años posteriores a 2020
- Detalle por persona o por vehículo
- Modelos predictivos y alertas
- Seguridad por filas: los datos no contienen información personal

## Fuente de datos

| Fuente | Contenido | Actualización |
|---|---|---|
| `data/raw/BD-Accidentes-Carreteras.xlsx`, hoja `registro_acidente` | 60.531 accidentes, 20 columnas | Estática |
| Misma fuente, hoja `diccionario_datos` | Descripción de las columnas | Estática |

Los registros provienen de los datos abiertos de la policía de carreteras de Brasil (PRF) y se recibieron traducidos al español.

## Supuestos

- Cada fila de la fuente es un accidente.
- La fuente es un extracto estático de 2018 a 2020; no hay cargas periódicas previstas.
- Todos los usuarios ven la totalidad de los datos.

## Criterios de aceptación

| Cifra de control | Valor |
|---|---|
| Total de eventos 2018-2020 | 60.531 |
| Eventos por año | 2018: 20.799 · 2019: 20.545 · 2020: 19.187 |
| Eventos por estado | MG: 26.160 · RJ: 13.417 · SP: 12.936 · ES: 8.018 |
| Total de heridos | 71.260 |
| Total de fallecidos | 4.062 |

Además:

- Los porcentajes del reporte suman 100 % con cualquier combinación de filtros.
- El reporte abre y se actualiza desde un clon limpio del repositorio.

## Control de cambios

| Versión | Fecha | Cambio |
|---|---|---|
| 1.0 | 2026-10-06 | Versión inicial |
