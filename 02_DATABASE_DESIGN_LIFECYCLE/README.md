# DATABASE DESIGN LIFECYCLE

## Definición

El Database Design Lifecycle (Ciclo de Vida del Diseño de Bases de Datos) es el proceso utilizado para transformar necesidades de negocio en una base de datos funcional, escalable y mantenible.

Su objetivo es garantizar que la base de datos represente correctamente la realidad del negocio antes de implementar tablas, relaciones o consultas SQL.

---

## ¿Por qué es importante?

Muchos proyectos fracasan porque comienzan creando tablas sin comprender completamente los requerimientos.

Un buen diseño:

* Reduce errores.
* Facilita el mantenimiento.
* Mejora el rendimiento.
* Disminuye costos futuros.
* Facilita la escalabilidad.

---

# Etapas del Diseño de una Base de Datos

```text
Recolección de Requerimientos
↓
Modelo Conceptual
↓
Modelo Lógico
↓
Modelo Físico
↓
Implementación
↓
Optimización y Mantenimiento
```

---

# 1. Recolección de Requerimientos

## Definición

Es la etapa donde se identifica qué necesita el negocio.

Antes de diseñar cualquier tabla debemos comprender:

```text
Qué datos existen.
Quién utilizará los datos.
Cómo serán utilizados.
```

---

## Preguntas clave

### ¿Qué datos necesita almacenar?

Ejemplos:

```text
Clientes
Cuentas
Transacciones
Productos
Facturas
Empleados
```

---

### ¿Quién utilizará la base de datos?

Ejemplos:

```text
Administradores
Analistas
Clientes
Aplicaciones
Sistemas externos
```

---

### ¿Qué consultas y reportes se necesitan?

Ejemplos:

```text
Saldo por cliente
Ventas mensuales
Transacciones diarias
Ranking de productos
```

---

### ¿Qué volumen de datos se espera?

Ejemplos:

```text
100 registros
10,000 registros
10 millones de registros
```

---

### ¿Qué nivel de seguridad se requiere?

Ejemplos:

```text
Datos públicos
Datos internos
Datos financieros
Datos personales
```

---

### ¿SQL o NoSQL?

La decisión depende de los requerimientos.

#### SQL

Ideal para:

```text
Datos estructurados
Relaciones complejas
Consistencia
Transacciones
```

Ejemplos:

```text
SQL Server
PostgreSQL
MySQL
Oracle
```

---

#### NoSQL

Ideal para:

```text
Datos flexibles
Alta escalabilidad
Documentos
Eventos
Logs
```

Ejemplos:

```text
MongoDB
Cassandra
Redis
```

---

# 2. Modelo Conceptual

## Definición

Representa el negocio sin pensar todavía en tablas o tecnología.

Pregunta principal:

> ¿Qué objetos existen en el negocio?

---

## Ejemplo bancario

Entidades:

```text
Cliente
Cuenta
Transacción
Sucursal
Empleado
```

---

## Relaciones

```text
Cliente posee Cuenta

Cuenta registra Transacciones

Sucursal administra Cuentas
```

---

## Objetivo

Comprender el negocio.

No diseñar tablas.

---

# 3. Modelo Lógico

## Definición

Transforma entidades y relaciones en estructuras relacionales.

Aquí aparecen:

```text
Tablas
Columnas
Primary Keys
Foreign Keys
```

---

## Ejemplo

Entidad:

```text
Cliente
```

Se convierte en:

```text
Tabla Clientes
```

---

Entidad:

```text
Cuenta
```

Se convierte en:

```text
Tabla Cuentas
```

---

Relación:

```text
Cliente posee Cuenta
```

Se convierte en:

```text
Clientes
↓
Cuentas
```

mediante una Foreign Key.

---

# 4. Modelo Físico

## Definición

Representa la implementación específica en un motor de base de datos.

Ahora pensamos en:

```text
Tipos de datos
Índices
Restricciones
Particiones
```

---

## Ejemplo

```sql
CREATE TABLE Clientes
(
    IdCliente INT PRIMARY KEY,
    Nombre VARCHAR(100),
    FechaNacimiento DATE
);
```

---

## Decisiones físicas

```text
INT o BIGINT
VARCHAR o NVARCHAR
Índices
Constraints
```

---

# 5. Implementación

## Definición

Consiste en construir físicamente la base de datos.

---

## Actividades

```text
Crear tablas
Crear relaciones
Crear índices
Crear vistas
Crear procedimientos almacenados
```

---

## Ejemplo

```sql
CREATE TABLE Clientes
(
    IdCliente INT PRIMARY KEY,
    Nombre VARCHAR(100)
);
```

---

# 6. Optimización y Mantenimiento

## Definición

Una base de datos nunca termina después de ser creada.

Debe mantenerse continuamente.

---

## Actividades

```text
Optimización de consultas
Índices
Backups
Monitoreo
Particionamiento
Auditoría
```

---

## Preguntas frecuentes

### ¿Por qué una consulta es lenta?

Posibles causas:

```text
Falta de índices
Diseño deficiente
Consultas ineficientes
```

---

### ¿Por qué crece la base de datos?

```text
Más usuarios
Más transacciones
Más información histórica
```

---

# Caso Bancario Completo

## Requerimiento

Un banco necesita almacenar:

```text
Clientes
Cuentas
Transacciones
Sucursales
```

---

## Modelo Conceptual

```text
Cliente
↓
Cuenta
↓
Transacción
```

---

## Modelo Lógico

```text
Clientes

Cuentas
- FK Cliente

Transacciones
- FK Cuenta
```

---

## Modelo Físico

```sql
Clientes
(
    IdCliente INT
)

Cuentas
(
    IdCuenta INT,
    IdCliente INT
)

Transacciones
(
    IdTransaccion INT,
    IdCuenta INT
)
```

---

## Implementación

```sql
CREATE TABLE Clientes ...
CREATE TABLE Cuentas ...
CREATE TABLE Transacciones ...
```

---

## Optimización

```text
Índices
Execution Plans
Particionamiento
```

---

# Error común

❌ Crear tablas inmediatamente.

```text
Sin comprender el negocio.
```

---

✔ Correcto

```text
Requerimientos
↓
Modelo Conceptual
↓
Modelo Lógico
↓
Modelo Físico
↓
Implementación
```

---

# Error conceptual frecuente

Muchos principiantes creen que:

```text
Diseñar una base de datos es crear tablas.
```

Incorrecto.

Crear tablas es únicamente una pequeña parte del proceso.

El verdadero diseño comienza entendiendo el negocio.

---

# Pensamiento de Arquitectura de Datos

Antes de diseñar una base de datos pregúntate:

1. ¿Qué problema estoy resolviendo?
2. ¿Qué información necesita el negocio?
3. ¿Qué entidades existen?
4. ¿Cómo se relacionan?
5. ¿Cómo crecerán los datos?
6. ¿Qué tecnología es la adecuada?

---

# Relación con los siguientes módulos

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
```

---

# Resumen

El ciclo de vida del diseño de bases de datos permite transformar necesidades de negocio en sistemas de información bien estructurados.

Etapas fundamentales:

1. Recolección de Requerimientos
2. Modelo Conceptual
3. Modelo Lógico
4. Modelo Físico
5. Implementación
6. Optimización y Mantenimiento

Comprender este proceso es fundamental para convertirse en:

* Database Engineer
* Data Architect
* DBA
* Data Engineer
* Analytics Engineer
