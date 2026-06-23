# SNOWFLAKE SCHEMA

## Definición

Snowflake Schema (Esquema Copo de Nieve) es una extensión del Star Schema donde las tablas de dimensiones se normalizan.

Su objetivo es:

- Reducir redundancia.
- Mejorar consistencia.
- Facilitar mantenimiento.

Recibe su nombre porque su estructura se asemeja a un copo de nieve.

---

# ¿Por qué existe?

En Star Schema las dimensiones suelen estar desnormalizadas.

Ejemplo:

## DimProducto

| ProductoKey | Producto | Categoria | Departamento |
|------------|-----------|------------|--------------|
| 1 | Laptop | Computadoras | Tecnología |
| 2 | Mouse | Accesorios | Tecnología |

---

Problema:

```text
Tecnología
Tecnología
Tecnología
```

se repite muchas veces.

---

# Solución

Normalizar las dimensiones.

---

## DimProducto

| ProductoKey | Producto | CategoriaKey |
|------------|-----------|--------------|
| 1 | Laptop | 10 |
| 2 | Mouse | 20 |

---

## DimCategoria

| CategoriaKey | Categoria | DepartamentoKey |
|-------------|-----------|------------------|
| 10 | Computadoras | 100 |
| 20 | Accesorios | 100 |

---

## DimDepartamento

| DepartamentoKey | Departamento |
|-----------------|-------------|
| 100 | Tecnología |

---

Ahora:

```text
Tecnología
```

se almacena una sola vez.

---

# Visualización

## Star Schema

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

## Snowflake Schema

```text
                  DimCategoria
                        |
                        ▼

DimDepartamento ← DimProducto
                        |
                        ▼

DimFecha ---- FactVentas ---- DimCliente
```

---

# Componentes principales

## Fact Table

Contiene:

```text
Métricas
Medidas
Indicadores
```

Ejemplos:

```text
Ventas
Ingresos
Cantidad
Costos
```

---

## Dimension Tables

Contienen:

```text
Información descriptiva.
```

---

## Dimensiones Normalizadas

A diferencia de Star Schema:

```text
DimProducto
↓
DimCategoria
↓
DimDepartamento
```

---

# Ejemplo completo

## FactVentas

| FechaKey | ProductoKey | Ventas |
|-----------|------------|---------|
| 1 | 100 | 1500 |
| 2 | 101 | 3000 |

---

## DimProducto

| ProductoKey | Producto | CategoriaKey |
|-------------|-----------|--------------|
| 100 | Laptop | 10 |
| 101 | Mouse | 20 |

---

## DimCategoria

| CategoriaKey | Categoria |
|-------------|-----------|
| 10 | Computadoras |
| 20 | Accesorios |

---

# Consulta

```sql
SELECT
    c.Categoria,
    SUM(f.Ventas) AS TotalVentas
FROM FactVentas f
INNER JOIN DimProducto p
    ON f.ProductoKey = p.ProductoKey
INNER JOIN DimCategoria c
    ON p.CategoriaKey = c.CategoriaKey
GROUP BY c.Categoria;
```

---

# Ventajas

## Menor redundancia

Información almacenada una sola vez.

---

## Mayor integridad

Menor riesgo de inconsistencias.

---

## Menor almacenamiento

Comparado con Star Schema.

---

## Mejor mantenimiento

Cambios realizados en un único lugar.

---

# Desventajas

## Más JOINs

Las consultas son más complejas.

---

## Menor rendimiento

Comparado con Star Schema.

---

## Más difícil de entender

Especialmente para usuarios de negocio.

---

# Star Schema vs Snowflake Schema

| Característica | Star Schema | Snowflake Schema |
|---------------|-------------|------------------|
| Dimensiones | Desnormalizadas | Normalizadas |
| JOINs | Menos | Más |
| Rendimiento | Mayor | Menor |
| Redundancia | Mayor | Menor |
| Complejidad | Baja | Alta |
| Mantenimiento | Medio | Alto |
| Facilidad BI | Alta | Media |

---

# Caso de negocio

## Empresa Retail

Pregunta:

```text
¿Cuáles fueron las ventas por departamento?
```

---

### Star Schema

```text
FactVentas
↓
DimProducto
```

Departamento incluido dentro de DimProducto.

---

### Snowflake Schema

```text
FactVentas
↓
DimProducto
↓
DimCategoria
↓
DimDepartamento
```

Departamento almacenado separadamente.

---

# ¿Cuándo utilizar Star Schema?

Cuando la prioridad es:

```text
Rendimiento.
Simplicidad.
Business Intelligence.
```

---

Ejemplos:

- Power BI
- Tableau
- Dashboards Ejecutivos

---

# ¿Cuándo utilizar Snowflake Schema?

Cuando la prioridad es:

```text
Reducir redundancia.
Mejorar mantenimiento.
Modelos complejos.
```

---

Ejemplos:

- Grandes Data Warehouses
- Modelos corporativos
- Arquitecturas empresariales

---

# Error común

Muchos principiantes creen:

```text
Snowflake siempre es mejor.
```

---

Incorrecto.

Más normalización no significa mejor diseño.

---

# Error conceptual frecuente

Muchos creen:

```text
Star Schema está mal diseñado.
```

---

Incorrecto.

La redundancia en Star Schema es:

```text
Intencional.
```

Su objetivo es mejorar rendimiento.

---

# Pensamiento de Data Engineering

Antes de elegir entre Star y Snowflake pregúntate:

1. ¿Qué es más importante: rendimiento o almacenamiento?
2. ¿Quién consumirá los datos?
3. ¿Habrá muchas consultas analíticas?
4. ¿Las dimensiones son muy grandes?
5. ¿Qué tan complejo será el mantenimiento?

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

Snowflake Schema es una versión normalizada del Star Schema.

Características:

- Menor redundancia.
- Más tablas.
- Más JOINs.
- Mayor consistencia.
- Menor rendimiento analítico.

Se utiliza cuando la organización prioriza mantenimiento e integridad sobre simplicidad y velocidad.

Star Schema prioriza rendimiento.

Snowflake Schema prioriza normalización.
