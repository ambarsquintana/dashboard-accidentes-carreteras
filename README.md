# 🚗 Dashboard de accidentes en carreteras

![Status](https://img.shields.io/badge/Status-En%20construcci%C3%B3n-orange) ![Power BI](https://img.shields.io/badge/%F0%9F%93%8A%20Power%20BI-F2C811) ![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white) ![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white) ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?logo=jupyter&logoColor=white) ![Parquet](https://img.shields.io/badge/Parquet-50ABF1?logo=apacheparquet&logoColor=white) ![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white)

Este proyecto nació en la inmersión «Acelerador de Carrera con Power BI» de [DaxusLatam](https://www.daxus.com/), donde se construyó un dashboard para analizar los accidentes en carreteras federales de Brasil entre 2018 y 2020. Aquí lo convierto en una solución de datos end-to-end, con fines demostrativos para mi portafolio.

## 🎯 Sobre este proyecto

**Material original de DaxusLatam**

- Caso de negocio
- Conjunto de datos en Excel
- Template visual
- Dashboard de una página en Power BI

**Lo que agrega este repositorio**

- ETL Medallion (bronze, silver, gold) con Python y pandas
- Perfilado del dato y validaciones que detienen el proceso si una regla falla
- Modelo estrella en lugar de una sola tabla
- Reporte en formato PBIP, legible como código
- Documentación de requerimientos, arquitectura, mapeo fuente-destino y diccionario de datos
- Todo el proyecto versionado en Git

---

## ⚙️ Estructura del proyecto

```
├── docs/        # Requerimientos, arquitectura, mapeo, diccionario y business case
├── data/
│   ├── raw/     # Archivo fuente, no se modifica
│   ├── bronze/  # Copia fiel de la fuente en Parquet (no versionado)
│   ├── silver/  # Datos limpios y tipados (no versionado)
│   └── gold/    # Modelo estrella para Power BI (no versionado)
├── etl/         # Notebooks de cada capa
├── exploration/ # Perfilado del dato, fuera del pipeline
├── powerbi/     # Proyecto .pbip: modelo semántico (TMDL) y reporte
├── assets/      # Template y recursos visuales
├── requirements.txt  # Dependencias de Python
└── README.md    # Documentación del proyecto
```

## 🏗️ Arquitectura

| Capa | Contenido | Formato |
|---|---|---|
| 📥 Raw | Archivo fuente tal como se recibió | Excel |
| 🥉 Bronze | Copia fiel de la fuente con metadatos de carga | Parquet |
| 🥈 Silver | Datos limpios, tipados y validados | Parquet |
| 🥇 Gold | Modelo estrella: hecho de accidentes y dimensiones | Parquet |
| 📊 Reporte | Modelo semántico y dashboard | Power BI (PBIP) |

El perfilado de bronze define las reglas de limpieza que aplica silver. Cada capa valida sus datos antes de escribir.

## 📚 Documentación

| Documento | Contenido |
|---|---|
| [Requerimientos](docs/01_requerimientos.md) | Objetivo, usuarios, requerimientos, alcance y criterios de aceptación |
| [Arquitectura](docs/02_arquitectura.md) | Flujo de datos, capas, herramientas y decisiones de diseño |
| [Mapeo fuente-destino](docs/03_mapeo_fuente_destino.md) | Cómo cambia cada columna entre capas |
| [Diccionario de datos](docs/04_diccionario_datos.md) | Tablas y columnas de la capa gold |
| [Perfilado de bronze](exploration/01_perfilado_bronze.ipynb) | Análisis de calidad del dato y hallazgos |

## 🚀 Instalación y ejecución

**Requisitos:** Python 3.10 o superior, Power BI Desktop y VS Code con las extensiones Python y Jupyter.

1. Clonar el repositorio:

   ```
   git clone https://github.com/ambarsquintana/dashboard-accidentes-carreteras.git
   cd dashboard-accidentes-carreteras
   ```

2. Instalar las dependencias:

   ```
   pip install -r requirements.txt
   ```

3. Ejecutar los notebooks de `etl/` en orden: `01_bronze` y luego `02_silver`. Cada uno genera su capa en `data/`, que no se versiona porque se reconstruye desde la fuente.
4. Abrir `powerbi/accidentes-carreteras.pbip` en Power BI Desktop.

## 📌 Estado

- [x] Estructura del repositorio y formato .pbip
- [x] Business case
- [x] Requerimientos y arquitectura
- [x] Capa bronze
- [x] Perfilado del dato
- [x] Capa silver y mapeo fuente-destino
- [x] Capa gold y diccionario de datos
- [ ] Definición de métricas
- [ ] Modelo semántico
- [ ] Reporte
- [ ] Validación contra cifras de control

## 🙌 Créditos

El conjunto de datos, el business case, el template y la versión original del dashboard provienen de la inmersión «Acelerador de Carrera con Power BI» de [DaxusLatam](https://www.daxus.com/), una clase abierta en YouTube, impartida por la [Profe Zaira Hurtado](https://www.instagram.com/profe.zaki). Este repositorio es un trabajo independiente, sin vínculo con DaxusLatam ni con su equipo, creado solo con fines demostrativos.
