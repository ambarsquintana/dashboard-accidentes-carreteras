# Mapeo fuente-destino

| | |
|---|---|
| **Proyecto** | Seguimiento de accidentes en carreteras federales |
| **Responsable** | Equipo de Analytics |
| **Versión** | 1.0 |
| **Fecha** | 2026-10-06 |

Describe cómo cambia cada columna entre capas. Las reglas de silver salen de los hallazgos de [`exploration/01_perfilado_bronze.ipynb`](../exploration/01_perfilado_bronze.ipynb).

## Fuente a bronze

Proceso: `etl/01_bronze.ipynb`

Las 20 columnas de la hoja `registro_acidente` se copian sin cambios. Se agregan dos columnas de auditoría:

| Columna | Tipo | Regla |
|---|---|---|
| `_fecha_carga` | Fecha y hora | Momento de la ejecución |
| `_archivo_origen` | Texto | Nombre del archivo fuente |

## Bronze a silver

Proceso: `etl/02_silver.ipynb`

### Columnas

| Columna en bronze | Columna en silver | Tipo | Regla |
|---|---|---|---|
| `id` | `id` | Entero | Sin cambio. Llave de la tabla |
| `Fecha`, `hora` | `fecha_accidente` | Fecha y hora | Se combinan en una sola columna; las originales se eliminan |
| `uf` | `estado` | Texto | Renombrada |
| `municipio` | `municipio` | Texto | Sin cambio |
| `causa_accidente` | `causa_accidente` | Texto | Reemplazo de valores y unificación |
| `tipo_acidente` | `tipo_accidente` | Texto | Renombrada. Reemplazo de valores |
| `clasificación_accidente` | `clasificacion_accidente` | Texto | Renombrada |
| `sentido_via` | `sentido_via` | Texto | Reemplazo de valores |
| `tipo_pista` | `tipo_carril` | Texto | Renombrada. Reemplazo de valores |
| `Personas` | `personas` | Entero | Renombrada |
| `Muertos` | `muertos` | Entero | Renombrada |
| `Heridos` | `heridos` | Entero | Renombrada |
| `Herido_Leves` | `heridos_leves` | Entero | Renombrada |
| `Heridos_graves` | `heridos_graves` | Entero | Renombrada |
| `ilesos` | `ilesos` | Entero | Sin cambio |
| `ignorados` | `ignorados` | Entero | Sin cambio |
| `vehículos` | `vehiculos` | Entero | Renombrada |
| `latitude` | `latitud` | Decimal | Renombrada |
| `longitude` | `longitud` | Decimal | Renombrada |
| `_fecha_carga` | `_fecha_carga` | Fecha y hora | Sin cambio |
| `_archivo_origen` | `_archivo_origen` | Texto | Sin cambio |

Bronze tiene 22 columnas y silver 21.

## Silver a gold

Se documenta con la entrega de `etl/03_gold.ipynb`.

## Control de cambios

| Versión | Fecha | Cambio |
|---|---|---|
| 1.0 | 2026-10-06 | Versión inicial: fuente a bronze y bronze a silver |
