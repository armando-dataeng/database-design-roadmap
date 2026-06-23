# OLTP DESIGN

## Definición

OLTP significa:

```text
Online Transaction Processing
```

Es un tipo de sistema diseñado para gestionar transacciones operacionales en tiempo real.

Su objetivo principal es:

```text
Registrar operaciones de negocio
de forma rápida, segura y consistente.
```

---

## Ejemplos de sistemas OLTP

### Banco

```text
Transferencias
Depósitos
Retiros
Pagos
```

---

### E-commerce

```text
Pedidos
Pagos
Carritos de compra
```

---

### Hospital

```text
Citas
Pacientes
Recetas
```

---

### Universidad

```text
Inscripciones
Calificaciones
Matrículas
```

---

# Características de OLTP

## Muchas transacciones

Ejemplo:

```text
Miles de operaciones por minuto.
```

---

## Consultas pequeñas

Generalmente afectan pocos registros.

Ejemplo:

```sql
SELECT *
FROM Clientes
WHERE IdCliente = 100;
```

---

## Escrituras frecuentes

Operaciones comunes:

```sql
INSERT
UPDATE
DELETE
```

---

## Consistencia alta

Los datos deben ser correctos.

Ejemplo:

```text
Una transferencia bancaria
no puede perder dinero.
```

---

## Tiempo de respuesta bajo

Los usuarios esperan respuestas en:

```text
Milisegundos.
```

---

# Objetivos de diseño

Un sistema OLTP busca:

```text
Integridad
Consistencia
Disponibilidad
Rapidez
```

---

# Normalización en OLTP

La mayoría de los sistemas OLTP utilizan:

```text
3NF
```

o

```text
BCNF
```

---

## ¿Por qué?

Porque minimizan:

```text
Duplicación de datos
Errores
Inconsistencias
```

---

# Ejemplo Bancario

## Clientes

| IdCliente | Nombre |
|------------|---------|
| 1 | Pedro |

---

## Cuentas

| IdCuenta | IdCliente | Saldo |
|-----------|-----------|--------|
| 100 | 1 | 5000 |

---

## Transacciones

| IdTransaccion | IdCuenta | Monto |
|---------------|-----------|--------|
| 1 | 100 | 500 |

---

Características:

```text
Normalizado
Consistente
Escalable
```

---

# Diseño OLTP típico

```text
Clientes
    │
    ▼
Cuentas
    │
    ▼
Transacciones
```

---

## Relaciones

```text
1:N
```

---

Uso intensivo de:

```text
Primary Keys
Foreign Keys
Constraints
```

---

# Transacciones ACID

Todo sistema OLTP debe proteger:

```text
ACID
```

---

## Atomicity

```text
Todo o nada.
```

---

## Consistency

```text
Los datos permanecen válidos.
```

---

## Isolation

```text
Las transacciones no interfieren.
```

---

## Durability

```text
Los cambios sobreviven a fallos.
```

---

# Ejemplo de Transacción

```sql
BEGIN TRANSACTION;

UPDATE Cuentas
SET Saldo = Saldo - 100
WHERE IdCuenta = 1;

UPDATE Cuentas
SET Saldo = Saldo + 100
WHERE IdCuenta = 2;

COMMIT;
```

---

# Índices en OLTP

Los índices son fundamentales.

---

## Ejemplo

```sql
CREATE INDEX IX_Clientes_Id
ON Clientes(IdCliente);
```

---

Beneficio:

```text
Consultas rápidas.
```

---

# Consultas típicas

## Buscar cliente

```sql
SELECT *
FROM Clientes
WHERE IdCliente = 1;
```

---

## Buscar cuenta

```sql
SELECT *
FROM Cuentas
WHERE IdCuenta = 100;
```

---

## Registrar transacción

```sql
INSERT INTO Transacciones
VALUES (...);
```

---

# Qué evitar en OLTP

## Grandes agregaciones

Evitar:

```sql
SELECT
    SUM(Monto)
FROM Transacciones;
```

sobre millones de registros.

---

## Reportes complejos

OLTP no está diseñado para análisis masivo.

---

## Consultas históricas pesadas

Para eso existe:

```text
OLAP
```

---

# Caso real

## Sistema Bancario

Usuarios:

```text
Clientes
Cajeros
Aplicaciones móviles
```

---

Operaciones:

```text
Transferencias
Consultas de saldo
Pagos
Depósitos
```

---

Prioridad:

```text
Consistencia
```

No:

```text
Análisis
```

---

# Ventajas

## Alta integridad

Datos consistentes.

---

## Actualizaciones rápidas

Diseñado para escritura.

---

## Menor redundancia

Normalización.

---

## Seguridad

Permisos y auditoría.

---

# Desventajas

## Muchos JOINs

Consultas complejas.

---

## Reportes más lentos

No optimizado para análisis.

---

## Escalabilidad analítica limitada

Para eso existe OLAP.

---

# OLTP vs OLAP

| Característica | OLTP | OLAP |
|---------------|------|------|
| Objetivo | Operaciones | Análisis |
| Consultas | Cortas | Complejas |
| Escrituras | Muchas | Pocas |
| Lecturas | Individuales | Masivas |
| Normalización | Alta | Baja |
| Rendimiento | Transaccional | Analítico |

---

# Error común

Muchos principiantes utilizan la misma base de datos para:

```text
Operaciones
+
Reportes masivos
```

---

Resultado:

```text
Rendimiento deficiente.
```

---

# Error conceptual frecuente

Muchos creen que:

```text
OLTP significa SQL.
```

Incorrecto.

OLTP es:

```text
Un patrón de diseño.
```

Puede implementarse en:

- SQL Server
- PostgreSQL
- Oracle
- MySQL

---

# Pensamiento de Arquitectura de Datos

Antes de diseñar un sistema OLTP pregúntate:

1. ¿Cuántas transacciones por segundo existirán?
2. ¿Qué nivel de consistencia necesito?
3. ¿Qué tablas son críticas?
4. ¿Qué índices necesito?
5. ¿El sistema es operacional o analítico?

---

# Relación con los siguientes módulos

```text
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
DATA WAREHOUSE DESIGN
```

---

# Resumen

OLTP (Online Transaction Processing) es un modelo diseñado para gestionar operaciones de negocio en tiempo real.

Características:

- Muchas transacciones.
- Consultas rápidas.
- Alta consistencia.
- Diseño normalizado.
- Uso intensivo de ACID.

Se utiliza en:

- Bancos
- E-commerce
- ERP
- CRM
- Hospitales
- Universidades

Su prioridad es:

```text
Procesar operaciones correctamente.
```

No:

```text
Realizar análisis masivos.
```
