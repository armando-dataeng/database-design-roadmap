# OLAP DESIGN

## Definición

OLAP significa:

```text
Online Analytical Processing
```

Es un tipo de sistema diseñado para analizar grandes volúmenes de datos con fines de negocio.

Su objetivo principal es:

```text
Transformar datos en información.
```

---

## ¿Por qué existe OLAP?

Los sistemas OLTP están optimizados para:

```text
Insertar
Actualizar
Eliminar
```

Pero las empresas también necesitan responder preguntas como:

```text
¿Cuánto vendimos este año?

¿Cuál es nuestro producto más rentable?

¿Qué sucursal genera más ingresos?

¿Cuál es la tendencia de ventas mensual?
```

Estas consultas son analíticas.

---

# Ejemplos de sistemas OLAP

## Business Intelligence

```text
Power BI
Tableau
Looker
Qlik
```

---

## Data Warehouses

```text
SQL Server Data Warehouse
Snowflake
BigQuery
Redshift
Synapse Analytics
```

---

## Analytics

```text
Dashboards
KPIs
Reportes ejecutivos
Análisis históricos
```

---

# Características de OLAP

## Lecturas masivas

Ejemplo:

```sql
SELECT
    SUM(Ventas)
FROM FactVentas;
```

---

## Consultas complejas

Incluyen:

```text
JOINs
GROUP BY
Window Functions
Agregaciones
```

---

## Grandes volúmenes

Ejemplos:

```text
Millones
Miles de millones
Billones de registros
```

---

## Datos históricos

OLAP analiza:

```text
Meses
Años
Décadas
```

---

## Pocas escrituras

Normalmente:

```text
ETL
ELT
Carga nocturna
Carga programada
```

---

# Ejemplo

## Pregunta de negocio

```text
¿Cuáles fueron las ventas por región durante 2024?
```

---

## Consulta

```sql
SELECT
    Region,
    SUM(Ventas) AS TotalVentas
FROM FactVentas
GROUP BY Region;
```

---

# Diseño OLAP

A diferencia de OLTP:

```text
OLTP → Normalización

OLAP → Desnormalización
```

---

## ¿Por qué?

Porque OLAP prioriza:

```text
Velocidad de lectura.
```

---

No:

```text
Velocidad de escritura.
```

---

# Arquitectura típica

```text
OLTP
   ↓
ETL / ELT
   ↓
Data Warehouse
   ↓
OLAP
   ↓
Dashboards
```

---

# Caso Bancario

## Sistema Operacional

```text
Clientes
Cuentas
Transacciones
```

---

Genera:

```text
Millones de transacciones
```

---

## Sistema Analítico

Permite responder:

```text
Transacciones por mes

Ingresos por sucursal

Clientes más rentables

Tendencias históricas
```

---

# Métricas y Dimensiones

## Métricas

Datos numéricos.

Ejemplos:

```text
Ventas
Monto
Cantidad
Ganancia
```

---

## Dimensiones

Contexto de negocio.

Ejemplos:

```text
Cliente
Producto
Fecha
Sucursal
```

---

# Ejemplo

## FactVentas

| Fecha | Producto | Ventas |
|---------|----------|---------|
| 2024-01-01 | Laptop | 1000 |

---

Consulta:

```sql
SELECT
    Producto,
    SUM(Ventas)
FROM FactVentas
GROUP BY Producto;
```

---

# Diferencias entre OLTP y OLAP

| Característica | OLTP | OLAP |
|---------------|------|------|
| Objetivo | Operaciones | Análisis |
| Consultas | Simples | Complejas |
| Escrituras | Muchas | Pocas |
| Lecturas | Individuales | Masivas |
| Históricos | Limitados | Amplios |
| Normalización | Alta | Baja |
| Usuarios | Operativos | Analistas |

---

# Modelos comunes en OLAP

## Star Schema

```text
Fact Table
+
Dimension Tables
```

---

## Snowflake Schema

```text
Star Schema
+
Normalización parcial
```

---

# Ventajas

## Consultas rápidas

Diseñado para agregaciones.

---

## Análisis histórico

Permite comparar años y tendencias.

---

## Business Intelligence

Alimenta dashboards y KPIs.

---

## Escalabilidad

Preparado para grandes volúmenes.

---

# Desventajas

## No ideal para transacciones

Operaciones como:

```sql
INSERT
UPDATE
DELETE
```

no son su punto fuerte.

---

## Mayor almacenamiento

La desnormalización aumenta redundancia.

---

# Error común

Muchos equipos ejecutan reportes complejos directamente sobre OLTP.

Resultado:

```text
Bloqueos
Lentitud
Problemas de rendimiento
```

---

# Error conceptual frecuente

Muchos creen:

```text
OLAP es una base de datos.
```

Incorrecto.

OLAP es:

```text
Un patrón de diseño orientado al análisis.
```

---

# Pensamiento de Data Engineering

Antes de diseñar una solución OLAP pregúntate:

1. ¿Qué preguntas de negocio debo responder?
2. ¿Qué métricas necesito analizar?
3. ¿Qué dimensiones describen esas métricas?
4. ¿Qué volumen histórico almacenaré?
5. ¿Necesito Star Schema o Snowflake Schema?

---

# Relación con los siguientes módulos

```text
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
DATA WAREHOUSE DESIGN
```

---

# Resumen

OLAP (Online Analytical Processing) es un modelo diseñado para analizar grandes volúmenes de datos.

Características:

- Consultas complejas.
- Grandes agregaciones.
- Datos históricos.
- Desnormalización.
- Business Intelligence.

Se utiliza en:

- Data Warehouses
- Power BI
- Tableau
- Analytics
- Reporting

Su objetivo principal es:

```text
Transformar datos en conocimiento para la toma de decisiones.
```
