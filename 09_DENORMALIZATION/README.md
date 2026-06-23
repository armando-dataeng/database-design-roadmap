# DENORMALIZATION

## Definición

La Desnormalización (Denormalization) es el proceso de introducir redundancia controlada en una base de datos para mejorar el rendimiento de lectura.

Mientras que la normalización busca:

```text
Reducir redundancia.
```

la desnormalización busca:

```text
Reducir JOINs.
Reducir tiempo de consulta.
Mejorar rendimiento.
```

---

## ¿Por qué existe la desnormalización?

Supongamos una base de datos altamente normalizada.

---

## Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |

---

## Ciudades

| IdCiudad | NombreCiudad |
|-----------|--------------|
| 10 | Madrid |

---

## Direcciones

| IdDireccion | IdCliente | IdCiudad |
|-------------|------------|----------|
| 100 | 1 | 10 |

---

Para obtener:

```text
Pedro vive en Madrid
```

debemos realizar varios JOINs.

---

## SQL

```sql
SELECT
    c.Nombre,
    ci.NombreCiudad
FROM Clientes c
INNER JOIN Direcciones d
    ON c.IdCliente = d.IdCliente
INNER JOIN Ciudades ci
    ON d.IdCiudad = ci.IdCiudad;
```

---

## Problema

En sistemas con:

```text
Millones de registros
Miles de consultas
```

los JOINs pueden ser costosos.

---

# Solución

Guardar información repetida.

---

## Tabla desnormalizada

| IdCliente | Nombre | Ciudad |
|------------|---------|---------|
| 1 | Pedro | Madrid |

---

Consulta:

```sql
SELECT Nombre, Ciudad
FROM Clientes;
```

---

## Beneficio

```text
Menos JOINs.
Consultas más rápidas.
```

---

# Diferencia entre Normalización y Desnormalización

## Normalización

Objetivo:

```text
Eliminar redundancia.
```

---

Ventajas:

- Integridad.
- Consistencia.
- Menor almacenamiento.

---

## Desnormalización

Objetivo:

```text
Mejorar rendimiento.
```

---

Ventajas:

- Menos JOINs.
- Consultas rápidas.
- Mejor experiencia analítica.

---

# Caso Bancario

## Modelo normalizado

### Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |

---

### Sucursales

| IdSucursal | NombreSucursal |
|------------|----------------|
| 10 | Centro |

---

### Cuentas

| IdCuenta | IdCliente | IdSucursal |
|-----------|------------|------------|
| 100 | 1 | 10 |

---

Consulta:

```text
Cliente + Cuenta + Sucursal
```

requiere varios JOINs.

---

# Modelo desnormalizado

| IdCuenta | Cliente | Sucursal |
|-----------|----------|-----------|
| 100 | Pedro | Centro |

---

Consulta mucho más simple.

---

# ¿Cuándo utilizar desnormalización?

## Sistemas OLAP

Ejemplos:

```text
Power BI
Tableau
Looker
```

---

## Data Warehouses

Ejemplos:

```text
Fact Tables
Dimension Tables
```

---

## Reporting

Reportes ejecutados constantemente.

---

## Dashboards

Consultas de lectura intensiva.

---

# ¿Cuándo NO utilizarla?

## Sistemas OLTP

Ejemplos:

```text
Banco
ERP
CRM
E-commerce
```

---

Porque:

```text
La consistencia es más importante.
```

---

# Ejemplo de redundancia controlada

## Normalizado

### Productos

| IdProducto | Nombre |
|------------|---------|
| 1 | Laptop |

---

### Ventas

| IdVenta | IdProducto |
|----------|------------|
| 100 | 1 |

---

Consulta requiere JOIN.

---

## Desnormalizado

### Ventas

| IdVenta | Producto |
|----------|----------|
| 100 | Laptop |

---

Beneficio:

```text
Consulta directa.
```

---

Costo:

```text
Información duplicada.
```

---

# Star Schema

Uno de los modelos más utilizados en Data Warehousing.

---

## Características

Utiliza:

```text
Desnormalización controlada.
```

---

Ejemplo:

```text
FactVentas

DimCliente
DimProducto
DimFecha
```

---

Objetivo:

```text
Consultas analíticas rápidas.
```

---

# Ventajas

## Mejor rendimiento

Menos JOINs.

---

## Consultas más simples

SQL más sencillo.

---

## Mejor experiencia analítica

Dashboards más rápidos.

---

# Desventajas

## Redundancia

Información repetida.

---

## Más almacenamiento

Se duplican datos.

---

## Mayor mantenimiento

Los cambios deben propagarse.

---

# Error común

Muchos principiantes creen:

```text
Desnormalizar es un error.
```

---

Incorrecto.

En Data Warehousing:

```text
Es una práctica habitual.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Normalización y desnormalización son opuestas.
```

---

Realmente:

```text
Son herramientas.
```

---

La decisión depende del objetivo.

---

## OLTP

Prioridad:

```text
Consistencia.
```

---

## OLAP

Prioridad:

```text
Velocidad de consulta.
```

---

# Comparación

| Aspecto | Normalización | Desnormalización |
|----------|---------------|------------------|
| Redundancia | Baja | Alta |
| Integridad | Alta | Menor |
| JOINs | Más | Menos |
| Rendimiento lectura | Menor | Mayor |
| Rendimiento escritura | Mayor | Menor |
| OLTP | Ideal | No recomendado |
| OLAP | Menos común | Ideal |

---

# Caso real

## Banco

Sistema transaccional:

```text
OLTP
```

Utiliza:

```text
3NF
```

---

## Data Warehouse

Sistema analítico:

```text
OLAP
```

Utiliza:

```text
Star Schema
```

que incorpora desnormalización.

---

# Pensamiento de Arquitectura de Datos

Antes de desnormalizar pregúntate:

1. ¿Cuál es el problema de rendimiento?
2. ¿Cuántos JOINs existen?
3. ¿Es un sistema OLTP u OLAP?
4. ¿La redundancia es aceptable?
5. ¿Vale la pena el costo de mantenimiento?

---

# Relación con los siguientes módulos

```text
NORMALIZATION
↓
DENORMALIZATION
↓
OLTP_DESIGN
↓
OLAP_DESIGN
↓
STAR_SCHEMA
↓
DATA_WAREHOUSE
```

---

# Resumen

La Desnormalización consiste en introducir redundancia controlada para mejorar el rendimiento de lectura.

Objetivos:

- Reducir JOINs.
- Mejorar velocidad de consulta.
- Facilitar análisis y reporting.

Se utiliza principalmente en:

- Data Warehouses
- Business Intelligence
- Analytics
- OLAP

La normalización busca consistencia.

La desnormalización busca rendimiento.

Un arquitecto de datos debe saber cuándo utilizar cada enfoque.
