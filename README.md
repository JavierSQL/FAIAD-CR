# FAIAD-CR — Material del taller *Fabric Analyst in a Day* (4 h)

Material propio del **Grupo de Usuarios de Power BI Costa Rica** para la versión de 4 horas del taller *Fabric Analyst in a Day* (FAIAD).

Este repositorio contiene **solo material original del grupo**. No incluye los PDFs, PBIX, PQT, SQL ni datos del FAIAD oficial, que son propiedad intelectual de Microsoft y se entregan por su canal oficial.

## Contenido

| Archivo | Descripción |
|---------|-------------|
| `Notebook_CapaOro_FIAD.ipynb` | Notebook SparkSQL que construye una **capa Oro** (tablas Delta) a partir de la capa Bronze del lakehouse, lista para un modelo semántico en **Direct Lake**. |

## El notebook "Capa Oro"

Reemplaza el laboratorio de pipelines con un enfoque de **arquitectura medallion**:

- **Bronze** → tablas del *shortcut* a ADLS (esquema `dbo`).
- **Gold** → tablas materializadas por el notebook (esquema `gold`), con tipos corregidos y columnas listas para consumo.

Es **full process** (`CREATE OR REPLACE TABLE … AS SELECT`): cada corrida recrea las tablas completas. No es incremental — es simple y limpio, ideal para el taller.

Genera las tablas Gold: `Geo`, `Product`, `Reseller`, `Sales`, `Dates` (con `StartOfMonth`, `Year`, `MonthName`). Las celdas para `Customer`, `People`, `PO`, `Supplier` e `Invoices` quedan como plantilla para completar según las fuentes del taller.

## Requisitos

- Un lakehouse de Microsoft Fabric llamado **`lh_FAIAD`**, creado **con esquemas habilitados**.
- Un *shortcut* a la capa Bronze dentro del esquema `dbo` (folder `Delta-Parquet-Format-FY25`).

## Cómo usarlo

1. Descargá `Notebook_CapaOro_FIAD.ipynb` de este repositorio.
2. En Fabric: **Import notebook → from this computer**.
3. **Adjuntá el lakehouse `lh_FAIAD`** al notebook (panel izquierdo → *Add lakehouse*).
4. Ejecutá las celdas en orden: `CREATE SCHEMA gold` → `Geo` → `Product` → `Reseller` → `Sales` → `Dates`.
5. Construí el modelo semántico **seleccionando el esquema `gold`** (Direct Lake) y marcá `Dates` como tabla de fechas.

> Si los calificadores `dbo.` / `gold.` no resuelven en tu ambiente, ajustá el prefijo según cómo exponga el catálogo el lakehouse adjunto.

## Licencia

[MIT](LICENSE).
