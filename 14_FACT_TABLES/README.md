# FACT TABLES

## Definición

Una Fact Table (Tabla de Hechos) almacena los eventos o métricas del negocio que deseamos analizar.

Contiene:

- Medidas numéricas.
- Claves hacia dimensiones.
- Eventos de negocio.

Ejemplos:

```text
Ventas
Pedidos
Transacciones
Pagos
Reservaciones
Clicks
```

---

# ¿Por qué existen?

Las organizaciones necesitan responder preguntas como:

```text
¿Cuánto vendimos?

¿Cuántos pedidos recibimos?

¿Cuál fue la ganancia total?

¿Cuántas transacciones ocurrieron?
```

Las respuestas provienen de las Fact Tables.

---

# Estructura básica

Una Fact Table contiene:

## Foreign Keys

Referencias a dimensiones.

Ejemplo:

```text
FechaKey
ProductoKey
ClienteKey
SucursalKey
```

---

## Medidas

Valores numéricos.

Ejemplo:

```text
Cantidad
Ventas
Costo
Ganancia
```

---

# Ejemplo

## FactVentas

| FechaKey | ProductoKey | ClienteKey | Cantidad | Ventas |
|-----------|------------|------------|----------|---------|
| 1 | 100 | 10 | 2 | 1500 |
| 1 | 101 | 20 | 1 | 500 |

---

# ¿Qué representa una fila?

Cada fila representa:

```text
Un evento de negocio.
```

---

Ejemplo:

```text
Venta de un producto
a un cliente
en una fecha específica.
```

---

# Granularidad

## Definición

La granularidad define el nivel de detalle almacenado en una Fact Table.

Es una de las decisiones más importantes del diseño.

---

# Ejemplo

Pregunta:

```text
¿Qué representa exactamente una fila?
```

---

## Granularidad diaria

| Fecha | Producto | Ventas |
|---------|----------|---------|
| 2024-01-01 | Laptop | 5000 |

---

Cada fila representa:

```text
Ventas diarias por producto.
```

---

## Granularidad por transacción

| Fecha | Producto | Ventas |
|---------|----------|---------|
| 2024-01-01 | Laptop | 1500 |
| 2024-01-01 | Laptop | 2000 |
| 2024-01-01 | Laptop | 1500 |

---

Cada fila representa:

```text
Una venta individual.
```

---

# Regla importante

Antes de crear una Fact Table debes definir:

```text
La granularidad.
```

---

# Tipos de Fact Tables

## Transaction Fact Table

Registra eventos individuales.

---

Ejemplo:

```text
FactVentas
FactPagos
FactTransacciones
```

---

Cada fila:

```text
Una transacción.
```

---

## Periodic Snapshot Fact Table

Captura el estado en intervalos.

---

Ejemplo:

```text
Saldo diario.
Inventario mensual.
```

---

## Ejemplo

| Fecha | Saldo |
|---------|--------|
| 2024-01-01 | 1000 |
| 2024-01-02 | 1500 |

---

## Accumulating Snapshot Fact Table

Registra procesos con múltiples etapas.

---

Ejemplo:

```text
Pedido
↓
Envío
↓
Entrega
```

---

## FactPedidos

| Pedido | FechaPedido | FechaEnvio | FechaEntrega |
|----------|-------------|------------|--------------|
| 100 | 01-01 | 02-01 | 05-01 |

---

# Fact Table en Star Schema

```text
              DimCliente
                    |
                    ▼

DimFecha → FactVentas ← DimProducto
                    ▲
                    |
                    ▼

              DimSucursal
```

---

La Fact Table es el centro del modelo.

---

# Medidas aditivas

Se pueden sumar en todas las dimensiones.

Ejemplo:

```text
Ventas
Cantidad
Costos
```

---

## SQL

```sql
SELECT
    SUM(Ventas)
FROM FactVentas;
```

---

# Medidas semi-aditivas

Se pueden sumar parcialmente.

Ejemplo:

```text
Saldo de cuenta.
```

---

No siempre tiene sentido sumar:

```text
Saldo de Enero + Saldo de Febrero
```

---

# Medidas no aditivas

No deben sumarse.

Ejemplo:

```text
Porcentajes.
Promedios.
Ratios.
```

---

# Caso Retail

## FactVentas

| FechaKey | ProductoKey | ClienteKey | Ventas |
|-----------|------------|------------|---------|
| 1 | 100 | 10 | 1500 |

---

Preguntas que responde:

```text
Ventas por producto.

Ventas por cliente.

Ventas por mes.

Ventas por región.
```

---

# Caso Bancario

## FactTransacciones

| FechaKey | CuentaKey | SucursalKey | Monto |
|-----------|-----------|-------------|--------|
| 1 | 100 | 10 | 500 |

---

Preguntas:

```text
Monto total movido.

Transacciones por sucursal.

Transacciones por mes.

Clientes más activos.
```

---

# Buenas prácticas

## Definir la granularidad primero

Nunca después.

---

## Utilizar claves sustitutas

```text
Surrogate Keys
```

para dimensiones.

---

## Mantener solo métricas relevantes

Evitar columnas innecesarias.

---

## Utilizar nombres claros

```text
FactVentas
FactTransacciones
FactPedidos
```

---

# Error común

Diseñar una Fact Table sin definir la granularidad.

---

Resultado:

```text
Datos inconsistentes.
Agregaciones incorrectas.
Consultas ambiguas.
```

---

# Error conceptual frecuente

Muchos creen:

```text
Fact Table = Tabla grande.
```

Incorrecto.

Una Fact Table:

```text
Representa eventos medibles.
```

---

El tamaño es consecuencia del negocio.

---

# Fact Table vs Dimension Table

| Fact Table | Dimension Table |
|------------|-----------------|
| Métricas | Contexto |
| Números | Descripciones |
| Crece rápido | Crece lentamente |
| Centro del Star Schema | Alrededor de la Fact Table |

---

# Pensamiento de Data Engineering

Antes de diseñar una Fact Table pregúntate:

1. ¿Cuál es el proceso de negocio?
2. ¿Qué evento estoy midiendo?
3. ¿Cuál es la granularidad?
4. ¿Qué métricas necesito?
5. ¿Qué dimensiones describen esas métricas?

---

# Relación con los siguientes módulos

```text
STAR SCHEMA
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

Las Fact Tables almacenan los eventos y métricas del negocio.

Características:

- Contienen medidas numéricas.
- Referencian dimensiones.
- Son el centro del Star Schema.
- Permiten análisis y agregaciones.

Concepto más importante:

```text
Granularidad
```

Antes de diseñar una Fact Table siempre debes responder:

```text
¿Qué representa exactamente una fila?
```
