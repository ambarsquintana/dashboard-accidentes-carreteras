# Requerimientos

| | |
|---|---|
| **Proyecto** | Seguimiento de accidentes en carreteras federales |
| **Solicitante** | Dirección |
| **Responsable** | Equipo de Analytics |
| **Versión** | 1.2 |
| **Fecha** | 2026-10-07 |

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
| RF-04 | Total de fallecidos y de heridos | Solicitud de la Dirección |
| RF-05 | Mapa con la geolocalización de los eventos | Solicitud de la Dirección |
| RF-06 | Top 5 de causas de accidentes | Solicitud de la Dirección |
| RF-07 | Filtros por año y clasificación del accidente | Solicitud de la Dirección |
| RF-08 | Toda la información en una sola página | Solicitud de la Dirección |
| RF-09 | Eventos por estado, con su participación sobre el total | Propuesta de Analytics |
| RF-10 | Tendencia mensual de eventos y heridos | Propuesta de Analytics |
| RF-11 | Eventos por tipo de carril | Propuesta de Analytics |

## Requerimientos no funcionales

| ID | Requerimiento |
|---|---|
| RNF-01 | El proyecto se reconstruye completo desde el repositorio: ningún paso lee rutas locales fijas |
| RNF-02 | Las cifras del reporte coinciden con las de la capa gold y con las cifras de control |
| RNF-03 | El reporte se versiona en formato PBIP |
| RNF-04 | El reporte sigue la plantilla visual definida en `assets/Template.png` |

## Alcance

**Incluido**

- Accidentes en carreteras federales de los estados ES (Espírito Santo), MG (Minas Gerais), RJ (Río de Janeiro) y SP (São Paulo), de 2018 a 2020
- ETL por capas a partir del archivo fuente
- Modelo estrella y medidas en Power BI
- Reporte de una página

**Fuera de alcance**

- Fuentes adicionales o años posteriores a 2020
- Detalle por persona o por vehículo
- Análisis por estación del año, por municipio, por tipo de accidente y por número de víctimas por accidente
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
| 1.1 | 2026-10-07 | Se alinean los requerimientos funcionales con el reporte entregado: se retiran eventos por estación del año y accidentes con más de 3 víctimas, y el filtro por mes. Se renumeran los requerimientos y se cierran las definiciones pendientes |
| 1.2 | 2026-10-07 | RF-06 pasa de top 7 a top 5 de causas |
