# DATA WAREHOUSE DESIGN

## Definición

Un Data Warehouse (DW) es un repositorio centralizado diseñado para almacenar datos históricos provenientes de múltiples fuentes con fines analíticos y de toma de decisiones.

Su objetivo principal es:

```text
Transformar datos operacionales
en información estratégica.
```

---

# ¿Por qué existe un Data Warehouse?

Las empresas generan datos en múltiples sistemas:

```text
ERP
CRM
E-commerce
POS
Aplicaciones móviles
APIs externas
```

---

Cada sistema responde preguntas operacionales.

Pero la organización necesita responder preguntas globales:

```text
¿Cuáles fueron las ventas del último año?

¿Cuál es el cliente más rentable?

¿Qué región crece más rápido?

¿Cuál es la tendencia histórica?
```

---

Un Data Warehouse centraliza la información para responder estas preguntas.

---

# Características

## Orientado al negocio

Los datos se organizan alrededor de procesos de negocio.

Ejemplos:

```text
Ventas
Inventario
Pagos
Clientes
Pedidos
```

---

## Integrado

Combina información de múltiples sistemas.

---

## Histórico

Conserva años de información.

---

## No volátil

Los datos generalmente se insertan.

Raramente se actualizan o eliminan.

---

# Arquitectura General

```text
Sistemas Fuente
        │
        ▼

     ETL / ELT
        │
        ▼

 Data Warehouse
        │
        ▼

 Data Marts
        │
        ▼

 Dashboards
 Reportes
 Analytics
 BI
```

---

# Sistemas Fuente

Origen de los datos.

Ejemplos:

```text
SQL Server
PostgreSQL
Oracle
SAP
Salesforce
APIs
Archivos CSV
```

---

# ETL

## Extract

Extraer datos.

---

## Transform

Limpiar y transformar.

---

## Load

Cargar en el Data Warehouse.

---

## Ejemplo

```text
ERP
↓
ETL
↓
Data Warehouse
```

---

# ELT

Variante moderna.

```text
Extract
↓
Load
↓
Transform
```

---

Muy común en:

```text
Snowflake
BigQuery
Databricks
Synapse
```

---

# Modelado Dimensional

La mayoría de los Data Warehouses utilizan:

```text
Star Schema
```

o

```text
Snowflake Schema
```

---

# Componentes

## Fact Tables

Contienen:

```text
Ventas
Ingresos
Costos
Cantidad
```

---

## Dimension Tables

Contienen:

```text
Clientes
Productos
Fechas
Sucursales
```

---

# Ejemplo

## FactVentas

| FechaKey | ProductoKey | ClienteKey | Ventas |
|-----------|------------|------------|---------|
| 1 | 100 | 10 | 1500 |

---

## DimCliente

| ClienteKey | Nombre |
|------------|---------|
| 10 | Pedro |

---

## DimProducto

| ProductoKey | Producto |
|-------------|-----------|
| 100 | Laptop |

---

# Flujo Completo

```text
OLTP
↓
ETL / ELT
↓
Data Warehouse
↓
Power BI
```

---

# Caso Bancario

## Sistemas Operacionales

```text
Clientes
Cuentas
Transacciones
```

---

## ETL

Transforma datos.

---

## Data Warehouse

```text
FactTransacciones

DimCliente
DimCuenta
DimFecha
DimSucursal
```

---

## Reportes

```text
Transacciones por mes

Ingresos por sucursal

Clientes más rentables
```

---

# Data Marts

## Definición

Subconjuntos especializados del Data Warehouse.

---

Ejemplos:

### Ventas

```text
Sales Mart
```

---

### Finanzas

```text
Finance Mart
```

---

### Recursos Humanos

```text
HR Mart
```

---

Beneficio:

```text
Acceso simplificado.
```

---

# Buenas prácticas

## Definir procesos de negocio

Antes de diseñar tablas.

---

## Diseñar la granularidad

Antes de construir Fact Tables.

---

## Utilizar Surrogate Keys

Especialmente en dimensiones.

---

## Implementar SCD

Para mantener historial.

---

## Crear DimFecha

Prácticamente obligatoria.

---

# Errores comunes

## Copiar el modelo OLTP

Muchos principiantes construyen:

```text
Data Warehouse = OLTP gigante
```

---

Resultado:

```text
Consultas lentas.
Modelos complejos.
```

---

## Ignorar la granularidad

Genera problemas analíticos.

---

## No gestionar historial

Pérdida de contexto temporal.

---

# Error conceptual frecuente

Muchos creen:

```text
Data Warehouse = Base de Datos
```

---

Incorrecto.

Un Data Warehouse es:

```text
Una arquitectura.
```

---

Incluye:

```text
Fuentes
ETL/ELT
Modelado
Almacenamiento
BI
Gobierno de datos
```

---

# Data Warehouse Moderno

Arquitectura típica:

```text
APIs
ERP
CRM
Archivos
       │
       ▼

   Data Lake
       │
       ▼

  ETL / ELT
       │
       ▼

 Data Warehouse
       │
       ▼

 Power BI
 Tableau
 Looker
```

---

# Herramientas comunes

## Data Warehouse

- Snowflake
- BigQuery
- Redshift
- Synapse Analytics

---

## Integración

- Azure Data Factory
- SSIS
- Airflow
- dbt
- Fivetran

---

## BI

- Power BI
- Tableau
- Looker

---

# Pensamiento de Data Engineering

Antes de diseñar un Data Warehouse pregúntate:

1. ¿Qué preguntas de negocio debo responder?
2. ¿Cuáles son los procesos principales?
3. ¿Cuál será la granularidad?
4. ¿Qué dimensiones necesito?
5. ¿Cómo gestionaré el historial?
6. ¿Qué estrategia ETL/ELT utilizaré?
7. ¿Quién consumirá los datos?

---

# Roadmap Completado

```text
DATABASE FUNDAMENTALS
↓
DATABASE DESIGN LIFECYCLE
↓
ENTITIES AND ATTRIBUTES
↓
PRIMARY KEYS
↓
FOREIGN KEYS
↓
CARDINALITY
↓
ER DIAGRAMS
↓
NORMALIZATION
↓
DENORMALIZATION
↓
OLTP DESIGN
↓
OLAP DESIGN
↓
STAR SCHEMA
↓
SNOWFLAKE SCHEMA
↓
FACT TABLES
↓
DIMENSION TABLES
↓
SCD TYPES
↓
DATA WAREHOUSE DESIGN
```

---

# Resumen

Un Data Warehouse es una plataforma diseñada para análisis empresarial y toma de decisiones.

Componentes principales:

- Sistemas Fuente
- ETL / ELT
- Fact Tables
- Dimension Tables
- SCD Types
- Star Schema
- Data Marts
- Herramientas BI

Su objetivo es convertir datos operacionales en información estratégica para el negocio.

Comprender Data Warehouse Design es uno de los conocimientos más importantes para:

- Data Engineers
- Analytics Engineers
- BI Developers
- Data Architects
