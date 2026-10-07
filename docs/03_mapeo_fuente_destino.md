# Mapeo fuente-destino

| | |
|---|---|
| **Proyecto** | Seguimiento de accidentes en carreteras federales |
| **Responsable** | Equipo de Analytics |
| **Versión** | 1.2 |
| **Fecha** | 2026-10-07 |

Describe cómo cambia cada columna entre capas. Las reglas de silver salen de los hallazgos de [`exploration/01_perfilado_bronze.ipynb`](../exploration/01_perfilado_bronze.ipynb).

## Fuente a bronze

Proceso: `etl/01_bronze.ipynb`

Las 20 columnas de la hoja `registro_acidente` se copian sin cambios. `Fecha` es una fecha en la fuente, pero queda almacenada como fecha y hora (00:00) porque pandas no tiene un tipo de solo fecha; el tipo se corrige en silver.

Se agregan dos columnas de auditoría:

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
| `Fecha` | `fecha` | Fecha | Renombrada. Se devuelve al tipo fecha de la fuente |
| `hora` | `hora` | Hora | Sin cambio. Conserva el tipo hora de la fuente |
| `uf` | `estado_sigla` | Texto | Renombrada |
| `uf` | `estado` | Texto | Columna nueva: nombre del estado según la sigla |
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

Bronze tiene 22 columnas y silver 23.

### Nombres de estado

| `estado_sigla` | `estado` |
|---|---|
| ES | Espírito Santo |
| MG | Minas Gerais |
| RJ | Río de Janeiro |
| SP | São Paulo |

## Silver a gold

Se documenta con la entrega de `etl/03_gold.ipynb`.

## Control de cambios

| Versión | Fecha | Cambio |
|---|---|---|
| 1.0 | 2026-10-06 | Versión inicial: fuente a bronze y bronze a silver |
| 1.1 | 2026-10-06 | Silver conserva `fecha` y `hora` como columnas separadas; se elimina `fecha_accidente` |
| 1.2 | 2026-10-07 | `uf` pasa a `estado_sigla`; se agrega `estado` con el nombre del estado |
