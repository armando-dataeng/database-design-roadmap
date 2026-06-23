# DIMENSION TABLES

## Definición

Una Dimension Table (Tabla de Dimensión) almacena información descriptiva que proporciona contexto a los datos almacenados en una Fact Table.

Las dimensiones permiten responder preguntas como:

- ¿Quién realizó la compra?
- ¿Qué producto se vendió?
- ¿Cuándo ocurrió?
- ¿Dónde ocurrió?
- ¿Qué sucursal participó?

---

# ¿Por qué existen?

Una Fact Table almacena métricas.

Ejemplo:

| FechaKey | ClienteKey | ProductoKey | Ventas |
|-----------|------------|-------------|---------|
| 1 | 10 | 100 | 1500 |

---

Sin dimensiones únicamente sabemos:

```text
Cliente 10
Producto 100
Fecha 1
```

No conocemos su significado.

---

# Solución

Agregar tablas descriptivas.

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

## DimFecha

| FechaKey | Año | Mes |
|-----------|-----|-----|
| 1 | 2024 | Enero |

---

Ahora podemos interpretar:

```text
Pedro compró una Laptop
en Enero de 2024.
```

---

# Fact Table vs Dimension Table

## Fact Table

Contiene:

```text
Eventos
Métricas
Medidas
```

---

Ejemplos:

```text
Ventas
Costos
Cantidad
Ganancias
```

---

## Dimension Table

Contiene:

```text
Descripción
Contexto
Atributos
```

---

Ejemplos:

```text
Cliente
Producto
Sucursal
Fecha
Empleado
```

---

# Ejemplo Star Schema

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

## Contienen atributos descriptivos

Ejemplo:

### DimCliente

| ClienteKey | Nombre | Ciudad | País |
|------------|---------|---------|------|
| 10 | Pedro | Madrid | España |

---

## Crecen lentamente

Comparadas con Fact Tables.

---

## Utilizan claves sustitutas

Generalmente:

```text
Surrogate Keys
```

---

Ejemplo:

```text
ClienteKey
ProductoKey
FechaKey
```

---

# Tipos comunes de dimensiones

## DimCliente

Información del cliente.

---

Ejemplo:

| ClienteKey | Nombre | Ciudad |
|------------|---------|---------|
| 10 | Pedro | Madrid |

---

## DimProducto

Información de productos.

---

| ProductoKey | Producto | Categoría |
|-------------|-----------|------------|
| 100 | Laptop | Computadoras |

---

## DimFecha

Una de las dimensiones más importantes.

---

| FechaKey | Año | Mes | Trimestre |
|-----------|-----|-----|------------|
| 1 | 2024 | Enero | Q1 |

---

Permite responder preguntas como:

```text
Ventas por mes.

Ventas por trimestre.

Ventas por año.
```

---

## DimSucursal

Información geográfica.

---

| SucursalKey | Sucursal | Ciudad |
|-------------|-----------|---------|
| 10 | Centro | Madrid |

---

# Caso Retail

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

Consulta:

```sql
SELECT
    p.Producto,
    SUM(f.Ventas) AS TotalVentas
FROM FactVentas f
INNER JOIN DimProducto p
    ON f.ProductoKey = p.ProductoKey
GROUP BY p.Producto;
```

---

# Caso Bancario

## FactTransacciones

| FechaKey | CuentaKey | SucursalKey | Monto |
|-----------|-----------|-------------|--------|
| 1 | 100 | 10 | 500 |

---

## DimSucursal

| SucursalKey | NombreSucursal |
|-------------|----------------|
| 10 | Centro |

---

Pregunta:

```text
¿Cuánto dinero se movió
por sucursal?
```

---

Las dimensiones permiten responder esa pregunta.

---

# Dimensiones Conformadas

## Definición

Son dimensiones compartidas por múltiples Fact Tables.

---

Ejemplo:

```text
DimFecha
```

puede utilizarse en:

```text
FactVentas
FactPagos
FactInventario
FactPedidos
```

---

Beneficio:

```text
Consistencia.
```

---

# Buenas prácticas

## Utilizar Surrogate Keys

✔ Correcto

```text
ClienteKey
ProductoKey
```

---

## Mantener atributos descriptivos

✔ Correcto

```text
Nombre
Ciudad
Categoría
```

---

## Crear una DimFecha

Prácticamente obligatoria en todo Data Warehouse.

---

## Diseñar dimensiones reutilizables

Facilita crecimiento futuro.

---

# Error común

Muchos principiantes almacenan atributos descriptivos dentro de la Fact Table.

---

Ejemplo:

| Fecha | Cliente | Producto | Ventas |
|---------|----------|-----------|---------|
| 01-01-2024 | Pedro | Laptop | 1500 |

---

Problema:

```text
Redundancia.
Mayor almacenamiento.
Menor mantenimiento.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Las dimensiones son opcionales.
```

---

Incorrecto.

Sin dimensiones:

```text
No existe contexto de negocio.
```

---

Solo existen números.

---

# Pensamiento de Data Engineering

Antes de crear una dimensión pregúntate:

1. ¿Qué contexto necesita el negocio?
2. ¿Qué atributos describen el evento?
3. ¿La dimensión será reutilizada?
4. ¿Necesito una clave sustituta?
5. ¿Cambiarán estos atributos con el tiempo?

---

# Relación con los siguientes módulos

```text
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

Las Dimension Tables proporcionan contexto a las métricas almacenadas en las Fact Tables.

Características:

- Contienen atributos descriptivos.
- Utilizan claves sustitutas.
- Crecen lentamente.
- Rodean a las Fact Tables.

Ejemplos:

- DimCliente
- DimProducto
- DimFecha
- DimSucursal

Sin dimensiones existen datos.

Con dimensiones existe información de negocio.
