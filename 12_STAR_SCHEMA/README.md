# STAR SCHEMA

## Definición

Star Schema (Esquema Estrella) es un modelo de diseño utilizado en sistemas OLAP y Data Warehouses.

Recibe su nombre porque visualmente se asemeja a una estrella:

```text
        DimCliente
             |
             |
DimFecha -- FactVentas -- DimProducto
             |
             |
        DimSucursal
```

---

## Objetivo

Optimizar consultas analíticas.

Permitir:

- Reportes rápidos.
- Agregaciones eficientes.
- Dashboards.
- Business Intelligence.

---

## ¿Por qué existe?

Los sistemas OLTP están altamente normalizados.

Ejemplo:

```text
Clientes
Pedidos
Productos
Sucursales
Categorías
```

Para responder preguntas analíticas suelen requerirse muchos JOINs.

---

## Problema

Pregunta:

```text
¿Cuánto vendimos por producto durante 2024?
```

En un modelo OLTP podrían requerirse múltiples JOINs.

---

## Solución

Crear un modelo optimizado para análisis.

---

# Componentes principales

Un Star Schema tiene dos tipos de tablas:

```text
Fact Tables
Dimension Tables
```

---

# Fact Table

Contiene métricas del negocio.

Ejemplos:

```text
Ventas
Ingresos
Cantidad
Costos
Ganancias
```

---

## Ejemplo

### FactVentas

| FechaKey | ClienteKey | ProductoKey | Ventas |
|-----------|------------|-------------|---------|
| 1 | 10 | 100 | 1500 |
| 1 | 20 | 101 | 2000 |

---

# Dimension Tables

Contienen contexto descriptivo.

---

## DimCliente

| ClienteKey | Nombre |
|------------|---------|
| 10 | Pedro |
| 20 | Ana |

---

## DimProducto

| ProductoKey | Producto |
|-------------|-----------|
| 100 | Laptop |
| 101 | Mouse |

---

## DimFecha

| FechaKey | Año | Mes |
|-----------|-----|-----|
| 1 | 2024 | Enero |

---

# Visualización

```text
                DimCliente
                     |
                     |
                     ▼

DimFecha ---> FactVentas <--- DimProducto
                     ▲
                     |
                     |
                DimSucursal
```

---

# Características

## Tabla central

Existe una única tabla de hechos.

---

## Dimensiones alrededor

Las dimensiones rodean la tabla de hechos.

---

## Modelo desnormalizado

Las dimensiones suelen contener redundancia controlada.

---

## Optimizado para lectura

No para transacciones.

---

# Caso de negocio

## E-commerce

Pregunta:

```text
¿Cuáles fueron las ventas por categoría durante 2024?
```

---

Fact Table:

```text
FactVentas
```

---

Dimensiones:

```text
DimProducto
DimFecha
DimCliente
```

---

Consulta:

```sql
SELECT
    d.Año,
    p.Categoria,
    SUM(f.Ventas) AS TotalVentas
FROM FactVentas f
INNER JOIN DimFecha d
    ON f.FechaKey = d.FechaKey
INNER JOIN DimProducto p
    ON f.ProductoKey = p.ProductoKey
GROUP BY
    d.Año,
    p.Categoria;
```

---

# Ventajas

## Simplicidad

Fácil de entender.

---

## Rendimiento

Menos JOINs que modelos altamente normalizados.

---

## Ideal para BI

Compatible con:

- Power BI
- Tableau
- Looker
- Excel

---

## Escalabilidad

Permite almacenar grandes volúmenes históricos.

---

# Desventajas

## Redundancia

Existe duplicación controlada.

---

## Más almacenamiento

Comparado con modelos normalizados.

---

## No ideal para OLTP

No está diseñado para:

```sql
INSERT
UPDATE
DELETE
```

frecuentes.

---

# Ejemplo Bancario

## FactTransacciones

| FechaKey | CuentaKey | SucursalKey | Monto |
|-----------|-----------|-------------|-------|
| 1 | 100 | 10 | 500 |

---

## DimFecha

Información temporal.

---

## DimSucursal

Información de sucursales.

---

## DimCuenta

Información de cuentas.

---

Pregunta:

```text
¿Cuánto dinero se movió por sucursal durante el último año?
```

---

# Error común

Muchos principiantes intentan copiar directamente un modelo OLTP dentro del Data Warehouse.

Resultado:

```text
Demasiados JOINs.
Consultas lentas.
Reportes complejos.
```

---

# Error conceptual frecuente

Muchos creen que:

```text
Star Schema = Base de Datos
```

Incorrecto.

Star Schema es:

```text
Un patrón de modelado.
```

---

# Pensamiento de Data Engineering

Antes de diseñar un Star Schema pregúntate:

1. ¿Cuál es el proceso de negocio?
2. ¿Cuál es la métrica principal?
3. ¿Qué dimensiones describen esa métrica?
4. ¿Qué preguntas de negocio debo responder?
5. ¿Qué granularidad tendrá la Fact Table?

---

# Relación con los siguientes módulos

```text
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

Star Schema es el modelo más utilizado en Data Warehouses.

Está compuesto por:

- Fact Tables.
- Dimension Tables.

Su objetivo es:

- Mejorar rendimiento analítico.
- Simplificar consultas.
- Facilitar Business Intelligence.

Es uno de los conceptos fundamentales para cualquier Data Engineer o Data Architect.
